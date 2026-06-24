# Tangram Navigation

Tangram Navigation 是一个面向技术研究者和信息分析人员的结构化互联网资源导航项目。本项目的核心目标是对特定领域的在线资源进行系统性采集、分类归档与可用性跟踪，解决信息分散、链接失效、归类混乱等常见问题。项目定位为个人与小型团队使用的可维护资源索引工具，强调目录组织的逻辑性、条目信息的完整性以及更新流程的规范化。

Tangram Navigation 本身不托管或分发任何第三方内容，仅提供公开可访问的 URL 元数据与组织视图。项目以 Markdown 格式维护资源清单，并辅以自动化脚本进行链接状态检查与格式校验，适用于需要长期维护特定主题资源集合的技术人员、内容策展人与研究助理。

## 功能概览

- 多级分类目录体系：支持按主题、地域、语种、文件类型等维度建立分层导航结构，每个条目可归属多个分类标签。
- 链接状态监测：内置基于 HTTP 状态码的可用性检查脚本，定期输出失效链接报告，便于及时更新或剔除资源。
- 元数据扩展字段：每条资源记录支持标题、描述、维护状态、更新日期、备选链接等自定义字段，满足精细化管理需求。
- 快速检索与过滤：通过命令行工具或简单 Web 界面（可选）对资源列表进行关键词搜索、标签筛选与排序操作。
- 变更历史追踪：利用 Git 版本控制记录每次增删改操作，支持回滚、对比与协作审核，保证资源库的可审计性。
- 批量导入导出：支持从 CSV、JSON、OPML 等常见格式批量导入外部资源列表，亦可导出为标准格式用于迁移或备份。
- 自定义视图生成：根据用户配置生成面向不同受众的简化视图（如仅显示核心资源、按字母索引等），满足多样化展示需求。
- 协作审核机制：提供基于分支的提案流程，允许贡献者提交资源增删改请求，由维护者合并前进行可用性与内容相关性复核。

## 应用场景

- 个人技术书签库的规范化管理：开发者可将长期积累的零散浏览器书签导出后，按 Tangram Navigation 的目录结构重新组织，补充描述与标签，并通过状态监测功能定期清理失效链接，构建个人专属的高质量资源仓库。
- 团队内部知识共享门户：研究小组或项目团队可使用本项目搭建私有资源导航，统一收录行业报告、数据平台、开发文档等常用链接，配合变更历史与审核机制，确保团队成员始终访问到经过验证的最新资源。
- 公开主题资源合集发布：内容策展人可围绕特定主题（如开源 GIS 工具、古典乐数字档案、编程语言学习材料）构建公开导航站，利用自定义视图生成不同详细程度的展示页面，并以标准格式导出供其他平台引用。
- 学术文献与数据集索引维护：科研人员可将论文中引用的数据源、代码仓库、在线附录等链接集中管理，通过元数据记录访问日期与存档信息，有效应对学术资源网址变更频繁的问题，提升研究可复现性。

## 快速开始

以下命令序列将完成项目克隆、依赖安装与初始资源库构建，适用于 Linux/macOS 及 Windows WSL 环境。

```bash
# 克隆项目仓库
git clone https://github.com/tangram-navigation/tangram-nav.git
cd tangram-nav

# 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

# 初始化资源数据库并运行首次链接检查
python scripts/init_db.py --sample-data
python scripts/check_links.py --report-dir reports/
```

执行完成后，`reports/` 目录下将生成当前资源列表的可用性报告。用户可通过编辑 `data/sources/` 下的 Markdown 或 YAML 文件来增删资源条目，随后重新运行 `check_links.py` 更新状态。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心脚本运行环境，用于链接检查、格式校验与视图生成 |
| Git | 2.25 及以上 | 版本控制，用于追踪资源列表变更及协作提交管理 |
| pip | 21.0 及以上 | Python 包管理工具，用于安装 requirements.txt 中列出的第三方库 |
| curl | 7.68 及以上 | 链接状态检查的后备请求工具，当 Python requests 库不可用时使用 |
| GNU Make | 3.81 及以上 | 可选，用于自动化常见任务（如更新、测试、打包）的快捷命令封装 |
| markdownlint-cli | 0.31 及以上 | 可选，用于校验资源描述文档的 Markdown 语法规范性 |
| yamllint | 1.26 及以上 | 可选，用于校验 YAML 格式的元数据配置文件的语法正确性 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|---|---|---|
| 用户入门 | `docs/quick-start.md` | 如何快速建立第一个资源索引？如何运行链接检查？如何生成静态视图？ |
| 目录结构设计 | `docs/catalog-schema.md` | 分类层级如何定义？标签命名规范是什么？元数据字段有哪些？如何扩展自定义字段？ |
| 维护与更新流程 | `docs/maintenance-guide.md` | 新增资源需要哪些步骤？如何处理失效链接？版本更新记录如何撰写？ |
| 贡献与审核 | `CONTRIBUTING.md` | 如何提交资源增删改提案？提案审核标准是什么？如何解决合并冲突？ |
| 自动化脚本 API | `docs/script-api.md` | 各个 Python 脚本的输入输出参数说明，如何编写自定义插件或挂钩脚本？ |
| 常见问题 | `docs/faq.md` | 链接检查超时怎么办？如何处理 SSL 证书错误？如何迁移已有书签到本项目？ |

## 资源列表

以下 URL 为 Tangram Navigation 当前收录的原始数据条目，按主题归类展示。所有链接均原样列出，不附加任何 HTML 标签或 Markdown 超链接语法。

影视与流媒体资源

www.fanqiefilm.top
www.flyu.asia
www.heizhutv.fit
www.hengxingv.site
www.hongchatv.lol

## 项目结构

```
tangram-nav/
├── data/
│   ├── sources/                   # 原始资源条目，按分类存放为 .md 或 .yaml
│   │   ├── entertainment/         # 影视、音乐、游戏等娱乐类资源
│   │   ├── academics/             # 学术数据库、期刊索引、预印本平台
│   │   ├── devtools/              # 开发工具、API 文档、代码托管平台
│   │   └── misc/                  # 未归类或跨分类的通用资源
│   ├── tags/                      # 标签体系定义，每个标签一个 .yaml 文件
│   ├── schemas/                   # 资源记录结构的 JSON Schema 校验定义
│   └── archive/                   # 已移除或失效链接的归档记录，供审计参考
├── scripts/
│   ├── check_links.py             # 批量 HTTP/HTTPS 可用性检查主脚本
│   ├── init_db.py                 # 初始化资源库结构及生成样例数据
│   ├── export_formats.py          # 导出为 CSV、JSON、OPML 等格式
│   ├── generate_static.py         # 根据当前数据生成静态 HTML 导航页
│   └── utils/
│       ├── http_client.py         # 自定义超时与重试逻辑的请求封装
│       └── validators.py          # URL 格式、日期、标签合法性校验函数
├── reports/                       # 存放 check_links.py 生成的可用性报告 .json/.html
├── docs/                          # 用户手册、设计文档、API 说明
├── tests/                         # 单元测试与集成测试用例
│   ├── test_check_links.py
│   ├── test_validators.py
│   └── fixtures/                  # 测试用的固定样例数据
├── Makefile                       # 常用任务快捷命令 (make check, make update, make view)
├── requirements.txt               # Python 运行时依赖列表
├── .markdownlint.yaml             # Markdown 语法检查配置
├── .yamllint.yaml                 # YAML 语法检查配置
└── README.md                      # 项目总览与入口文档（本文档）
```

## 贡献指南

1. 阅读 `CONTRIBUTING.md` 文件，了解项目的分类规范、元数据字段定义及链接收录标准（包括内容相关性、合法性、稳定性等方面的基本门槛）。
2. 在 GitHub 上 Fork 本仓库，并在您的 Fork 中创建一个新的分支，分支命名建议为 `add-<category>-<resource-name>` 或 `update-<existing-resource>`，以便清晰标识变更目的。
3. 按照 `docs/catalog-schema.md` 中的指引，在 `data/sources/` 对应目录下新增或修改资源条目。请务必填写所有必需元数据字段，并确保 URL 格式正确、描述信息简洁准确。
4. 本地运行 `make check` 或手动执行 `python scripts/check_links.py` 验证新添加链接的可访问性，同时执行 `make test` 运行单元测试以保证未破坏现有功能。
5. 提交 Pull Request，并在描述中简要说明变更动机、所涉及资源的价值评估以及任何特殊注意事项。维护者将在 5 个工作日内进行审核，必要时会联系您补充信息或调整格式。

## 常见问题

**Q: 链接检查脚本报告大量超时或 SSL 错误，如何处理？**

A: 超时通常由目标服务器响应缓慢或网络环境不稳定造成，建议调整 `scripts/utils/http_client.py` 中的 `DEFAULT_TIMEOUT` 参数（单位秒）并适当增加重试次数。SSL 证书错误可先尝试更新本地 CA 证书包，或在检查脚本中为特定域名添加 `verify=False` 选项（仅限测试环境，生产环境请优先解决证书问题）。也可使用 `curl -v <url>` 手动测试以获取更详细的错误信息。

**Q: 如何批量迁移我现有的浏览器书签或 Pocket 收藏夹？**

A: 大多数浏览器支持将书签导出为 HTML 文件（通常为 Netscape Bookmark 格式）。您可以使用社区维护的转换脚本（参见 `docs/community-tools.md`）将该 HTML 转换为本项目接受的 CSV 或 YAML 格式。对于 Pocket 等第三方服务，可先导出为 CSV 文件，再通过 `scripts/import_from_csv.py` 进行映射导入。导入后请务必运行链接检查并对分类标签进行人工复核。

**Q: 项目是否提供在线演示或托管服务？**

A: Tangram Navigation 本身为静态资源管理工具，不提供云端托管服务。但您可以使用 `scripts/generate_static.py` 生成本地静态 HTML 页面，然后部署到任意 Web 服务器或 GitHub Pages、Cloudflare Pages 等平台。演示站点及部署参考模板请见 `docs/hosting-examples.md`。

## 许可证

MIT

> 外链数量: 5 | 生成时间: 2026-06-24 15:55:30
