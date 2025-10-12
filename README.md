# 1️⃣ 项目背景与目标

ZetaChain 是首个能够在所有区块链生态之间实现原生互联的通用区块链。其官方文档涵盖内容广泛，包括系统架构与原理说明、开发者指南、工具使用教程、节点部署与运维、链上应用与使用方式、社区/支持资源等多个模块，全面支撑用户与开发者理解和使用 ZetaChain。

为了帮助中文开发者和节点运营者更好地理解这些内容，并参与到 ZetaChain 的生态建设中，ZetaDAO 以社区协作的方式开展官方文档汉化工作，以构建高质量、长期可维护的中文技术资料体系。

## 本轮工作的目标
- 将 [ZetaChain Docs](https://www.zetachain.com/docs/) 的英文内容完整的、恰当的翻译为简体中文；
- 保持与英文版本的结构、格式、更新同步；
- 通过 Github + Markdown 的方式实现社区协作；
- 构建一套可长期维护的多语言文档体系。

# 2️⃣ 项目组织结构

|角色|职责|责任人|
|:-|:-|:-|
|汉化组组长|负责整体规划、质量审查与合并|@Rousseau|
|技术校对|负责审核技术准确性|@clearsky, @ivy, @Rousseau|
|翻译贡献|负责章节翻译、润色与格式统一|所有小组成员|
|校对与排版|错别字、语法与排版规范的检查|@clearsky, @ivy|

# 3️⃣ 文档结构

```bash
zetachain-docs-zh/
├── README.md                 ← 项目说明文档（当前文件）
├── CONTRIBUTING.md           ← 贡献指南与提交流程
├── GLOSSARY.md               ← 专有名词表与统一术语
├── /docs                     ← 汉化文档主目录
│   ├── welcome               ← 「欢迎」页面
│   ├── GetStarted/           ← 「开始」子目录
│   ├── Build/                ← 「构建」子目录
│   ├── Tools/                ← 「工具」子目录
│   ├── RunNode/              ← 「运行节点」子目录
│   ├── Use/                  ← 「使用」子目录
│   ├── About/                ← 「关于」子目录
│   └── Other/                ← 「其他」子目录
└── /scripts                  ← 同步、检测与格式化脚本
```

# 4️⃣ 任务分配

所有任务按章节划分，如：

|模块|文件路径|负责人|状态|
|:-|:-|:-|:-|
|欢迎|`docs/welcome.md`|@somebody|✅ 完成|
|运行节点|`docs/RunNode/`|@somebody|🚧 翻译中|
|开始|`docs/GetStarted/`|@somebody|🔍 待认领|

*提交前请阅读 `CONTRIBUTING.md`*

# 5️⃣ 翻译规范

- 风格一致
  - 使用简体中文；
  - 技术词汇保持英文原文（如 “Node”、“Validator”、“Bridge”）；
  - 句式流畅自然，不机械翻译；
  - 段落保持与英文原文一致。
- 格式规则
  - 所有文档使用 Markdown (.md);
  - 使用一级标题 # 表示章节名称；
  - 使用代码块 ``` 语法标记示例；
  - 中英文之间加空格（如：ZetaChain 是一个 EVM 兼容的链）。
- 术语对照
  - 所有专业名词请参考 *`GLOSSARY.md`*

# 6️⃣ 协作流程

1. fork 主仓库 https://github.com/Rousseau-DeworkHub/ZetaChain-CN-DOCS 到个人账户；
2. git clone 到本地；
3. 在 docs/ 目录中添加或修改对应文件；
4. 提交 Pull Request；
5. 组长审核合并；
6. 同步到 ZetaDAO 中文站点。

# 其他备注
- 每周一次组内电话会议，时间待定