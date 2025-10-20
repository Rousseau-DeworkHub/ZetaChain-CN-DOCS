| 标题                                      | 描述                                        |
| :---------------------------------------- | :------------------------------------------ |
| 在 Google Compute Engine 上创建核心验证器 | 在 Google Compute Engine 上托管核心验证器。 |

本指南介绍如何在 **Google Compute Engine (GCE)** 上快速部署一个 ZetaChain 验证人节点。本文旨在帮助工程师快速搭建并运行节点，可作为基础模板，根据实际需求进行调整。

## 概述

你将需要：

- 一个独立的 **服务账号（Service Account）**
- 一个 **GCE 虚拟机实例**
- 推荐：一个用于缓存关键文件的 **Cloud Storage 存储桶（buget）**
- 推荐：两个 **Secret Manager 密钥**，一个用于密钥环（keyring）密码，一个用于助记词（seed phrase）

### 服务账号

服务账号需要具备以下项目级权限：

- roles/storage.objectAdmin  
- roles/secretmanager.secretAccessor  
- roles/secretmanager.viewer  
- roles/secretmanager.secretVersionManager  

建议使用专用服务账号以提升安全性，而不是使用默认账户。

### GCE 实例

推荐的 VM 配置如下：

- 类型：`n2-standard-4`（4 核，16GB 内存）  
- 操作系统：Ubuntu 24.04  
- 启动盘：20GB（“balanced” 永久磁盘）  
- 本地磁盘：2 个 NVME（稍后配置为 RAID 阵列）  
- 配置 [服务账号](https://cloud.google.com/compute/docs/access/service-accounts) 为验证人节点使用的账号  
- 设置访问范围为“允许访问所有 Cloud API”  
- 启用 `enable-oslogin` 元数据并设置为 `true`，以启用 [OS 登录](https://cloud.google.com/compute/docs/oslogin/set-up-oslogin)  
- 启用 [Shielded VM](https://cloud.google.com/compute/shielded-vm/docs/modifying-shielded-vm)

以下是我们用于部署节点的 **Terraform 配置** 示例（请根据自己的环境调整）。其中的 `cloud-init` 配置文件需要参数，例如：

- **chain_id:** athens_7001-1  
- **network:** athens3  
- **snapshot_host:** https://testnet-fullnode.snapshots.zetachain.com/  
- **snapshot:** fullnode-snapshot-v20-H7341468-2024-10-22_20-03.tar  
- **protocol_version:** v22  
- **node_version:** v22.0.0  

```hcl
# Terraform 节选
resource "google_compute_instance" "zetachain_node" {
  name         = var.name
  project      = var.project
  machine_type = "n2-standard-4"
  zone         = var.zone
  ...
}
```

我们使用 **cloud-init** 来自动进行节点初始化，具体步骤将在下文说明。

### Cloud Storage

我们使用 Cloud Storage 缓存二进制文件（binaries）以避免依赖外部资源，同时缓存快照文件以便在遭遇宕机时加快节点恢复速度。

为了提高可用性，建议创建一个 [双区域（dual-region）](https://cloud.google.com/storage/docs/locations) 存储桶（budget），并选择包含 VM 部署区域的地区。

### Secret Manager

验证人的助记词必须进行备份，以便在恢复时使用。推荐将其存储在 **Secret Manager** 中。  此外，节点磁盘上的 keyring 由密码保护，将该密码存储在 Secret Manager 中可以实现自动化访问。

## Cloud Init

[cloud-init](https://cloud-init.io/) 用于在实例启动时自动化安装和配置区块链节点。验证人密钥的创建与质押操作仍需人工完成。

cloud-init 执行以下步骤脚本：

1. 配置磁盘阵列（RAID）  
2. 安装 Go  
3. 构建并安装 Cosmovisor  
4. 配置系统资源限制  
5. 安装 zetacored  
6. 配置 zetacored 节点  

cloud-init 还会编写 `zetacored` 的 systemd 服务文件，使其在启动时自动运行，并创建运行节点的 `zetachain` 用户。

```yaml
#cloud-config
# 以下省略若干配置...
runcmd:
- sudo /usr/local/bin/setup-disk-array.sh
- sudo /usr/local/bin/install-go.sh
- sudo /usr/local/bin/install-cosmovisor.sh
- sudo /usr/local/bin/configure-system-limits.sh
- sudo /usr/local/bin/install-zetacored.sh
- sudo /usr/local/bin/configure-zetacored.sh
```

## 验证人配置

当节点部署完成并运行后，需要手动执行验证人创建操作。**在创建验证人之前，请确保节点已完全同步。** 可通过节点日志中的区块高度与区块浏览器（例如 [ZetaScan](https://zetascan.com/)）的高度进行比较。

关键步骤如下：

1. 检查节点同步状态  
2. 创建密钥  
3. 备份助记词到 Secret Manager  
4. 转入验证人资金  
5. 执行验证人质押交易  

### 检查节点是否同步

使用以下命令查看节点日志：

```bash
sudo -u zetachain journalctl -f -u zetacored.service
```

日志示例：

```
Nov 06 22:32:53 ... "height":7559702,"num_txs":4,...,"message":"committed state"
```

表示当前节点同步到区块高度 7559702。

### 创建或恢复密钥

使用以下命令创建验证人私钥：

```bash
sudo /var/lib/zetacored/cosmovisor/current/bin/zetacored --home /var/lib/zetacored keys add operator --algo secp256k1
```

该命令会提示输入密钥环密码，请妥善记录。命令执行后会输出公钥和助记词。

### 备份助记词

可将助记词写入文件并通过 `gcloud` 命令上传至 Secret Manager。在创建文件前执行：

```bash
umask 077
```

然后保存助记词为 `seed_phrase.txt`，并上传：

```bash
gcloud secrets versions add my-secret --data-file=seed_phrase.txt
```

### 转入资金

获取刚生成的账户地址：

```bash
sudo /var/lib/zetacored/cosmovisor/current/bin/zetacored --home /var/lib/zetacored keys list
```

将验证人资金转入该地址，并使用以下命令验证余额：

```bash
sudo /var/lib/zetacored/cosmovisor/current/bin/zetacored --home /var/lib/zetacored query bank balances $(/var/lib/zetacored/cosmovisor/current/bin/zetacored keys show operator -a)
```

### 质押创建验证人

最后一步是发送质押交易，创建验证人。首先提取 ED25519 公钥（注意：不是上面创建密钥时输出的公钥）：

```bash
sudo -u mantrachain mantrachaind --home /var/lib/mantrachain tendermint show-validator | jq .key
```

然后使用以下命令创建验证人（替换 `<KEY>` 与 `<MONIKER>`）：

```bash
sudo /var/lib/zetacored/cosmovisor/current/bin/zetacored --home /var/lib/zetacored tx staking create-validator   --amount=1000000000000000000azeta   --pubkey="{"@type":"/cosmos.crypto.ed25519.PubKey","key":"<KEY>"}"   --moniker="<MONIKER>"   --chain-id=athens_7001-1   --commission-rate="1.00"   --commission-max-rate="1.00"   --commission-max-change-rate="0.01"   --min-self-delegation="1000000"   --gas="auto"   --gas-adjustment=1.15   --gas-prices="1.0azeta"   --from=operator
```

执行后系统会提示输入密钥环密码，并确认交易。成功后，验证人将正式在链上注册生效。
