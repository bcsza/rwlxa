# Tangram Navigation

Tangram Navigation 是一个面向中文互联网用户的开源技术资源聚合与导航工具，定位于高质量影视、动漫及泛娱乐内容站点的结构化收录与健康状态监测。项目目标用户包括自部署爱好者、资源检索需求者以及网络可达性研究人员。通过定期更新的链接库与简洁的呈现层，帮助用户在复杂网络环境中快速定位可用入口，降低信息筛选成本。

本项目不提供任何流媒体内容、下载服务或盗版资源，仅作为公开 URL 的整理与可达性验证层。所有收录站点均来源于公开渠道，项目维护者不对第三方内容的合法性、可用性及持续性作任何担保。用户在使用任何目标站点时，应自行遵守当地法律法规及网站服务条款。

## 功能概览

- 多维度资源分类：按内容类型、语言、地区等标签对收录站点进行二级分类，支持快速筛选。
- 链接存活检测：内置基于 HTTP 状态码与响应时长的定时探测任务，对失效链接自动标记并延迟重试。
- 自定义导航页生成：根据用户配置的偏好分类，动态生成轻量级静态导航首页，适合自部署于 Nginx 或 CDN。
- 结构化数据导出：支持将收录库导出为 JSON、YAML 及 CSV 格式，便于二次开发或迁移至其他导航系统。
- 标签与全文检索：提供基于 Lunr.js 的离线全文检索引擎，支持按站点名称、描述、标签及 URL 关键词搜索。
- 浏览器书签同步：生成符合 Chrome 与 Firefox 导入规范的 HTML 书签文件，支持一键导入主流浏览器。
- 容器化部署支持：提供 Dockerfile 与 docker-compose 示例，适配 x86_64 与 ARM64 架构，满足私有化部署场景。

## 应用场景

- 个人自部署导航站：用户可在自己的 VPS 或家用服务器上部署 Tangram Navigation，将常用影视资源站、工具站、文档站统一收纳为个人起始页，避免每次手动输入或翻阅浏览器书签。
- 小型团队内部资源共享：技术团队或兴趣小组可使用本项目维护一份共享的在线资源清单，成员可提交新增建议，通过 Pull Request 合并后自动更新导航页，减少口头传递 URL 的沟通成本。
- 网络可达性辅助观测：运维人员或网络研究者可借助定时探测功能，观察特定域名在不同时间段的 HTTP 可达率与响应趋势，辅助判断网络服务质量或 DNS 解析稳定性。
- 内容聚合二次开发基础：开发者可将本项目的结构化数据作为上游数据源，在其基础上开发移动端 App、RSS 订阅机器人或 Telegram 通知服务，实现个性化提醒与推送。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL2 环境，需预先安装 Git、Node.js 18.x 及 npm。

```bash
# 克隆仓库
git clone https://github.com/tangram-nav/tangram-navigation.git
cd tangram-navigation

# 安装依赖
npm install

# 构建静态导航页并启动开发服务器
npm run build
npm run start
```

构建完成后，静态文件输出至 `dist/` 目录，可直接部署至任意 Web 服务器。开发服务器默认监听 `http://localhost:3000`，访问即可查看导航首页。

若需启用定时探测功能，请单独运行监测服务：

```bash
npm run monitor
```

监测服务会每 30 分钟执行一次全量链接检查，并将结果写入 `data/status.json`。

## 安装要求

| 依赖 | 必需 | 说明 |
|------|------|------|
| Node.js 18.x 或更高 | 是 | 核心运行时，用于构建、检索及监测服务 |
| npm 9.x 或更高 | 是 | 包管理工具，用于安装依赖项 |
| Git 2.25+ | 是 | 用于克隆仓库及版本控制操作 |
| 内存 512 MB 及以上 | 是 | 构建过程及监测服务的内存最低要求 |
| 磁盘空间 200 MB | 是 | 存放源码、依赖及生成静态文件 |
| 可选：Docker Engine 20.10+ | 否 | 如需容器化部署，需安装 Docker 及 Compose |
| 可选：Python 3.9+（仅监测扩展） | 否 | 若使用高级网络质量分析脚本，需额外安装 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | `docs/quick-start.md` | 如何最快从零开始部署并访问导航页？ |
| 配置手册 | `docs/configuration.md` | 如何修改分类、添加自定义站点、调整探测间隔？ |
| API 参考 | `docs/api-reference.md` | 数据接口格式、监测状态字段定义及导出方法 |
| 部署方案 | `docs/deployment.md` | 分别介绍 Nginx、Docker、Vercel 等部署方式的详细配置模板 |

## 资源列表

影视类站点

www.fanqiefilm.top

www.flyu.asia

www.heizhutv.fit

www.hengxingv.site

www.hongchatv.lol

## 项目结构

```
tangram-navigation/
├── config/                         # 全局配置目录
│   ├── categories.json             # 分类与标签映射定义
│   └── probe-settings.json         # 探测超时、重试次数、并发数
├── data/                           # 数据存储目录
│   ├── sources.json                # 核心资源库（所有收录站点）
│   ├── status.json                 # 定时探测结果的缓存
│   └── user-bookmarks.json         # 用户自定义书签（非覆盖合并）
├── src/                            # 源代码目录
│   ├── builder/                    # 静态页生成器模块
│   │   ├── index.js                # 入口调度
│   │   └── template-engine.js      # 模板渲染逻辑
│   ├── monitor/                    # 链接存活监测模块
│   │   ├── checker.js              # HTTP 请求封装与状态判断
│   │   └── scheduler.js            # 定时任务编排
│   ├── search/                     # 检索相关
│   │   ├── index-builder.js        # Lunr 索引构建
│   │   └── query-parser.js         # 查询语法解析
│   └── utils/                      # 通用工具函数
│       ├── logger.js               # 日志级别控制
│       └── validator.js            # URL 格式校验
├── static/                         # 静态资源目录
│   ├── css/                        # 基础样式与主题
│   ├── js/                         # 前端交互脚本
│   └── fonts/                      # 字体文件
├── dist/                           # 构建输出目录（自动生成）
├── docs/                           # 文档目录
├── Dockerfile                      # 容器构建文件
├── docker-compose.yml              # 容器编排示例
├── package.json                    # npm 依赖清单
└── README.md                       # 项目主文档
```

## 贡献指南

1. 提交资源新增或更新建议时，请先阅读 `docs/contribution-criteria.md` 中的收录标准，确保站点内容合法、稳定且不涉及恶意代码。
2. 在 `data/sources.json` 中按 JSON Schema 格式添加或修改条目，并确保 `url` 字段值为完整且可访问的链接。提交前请运行 `npm run validate` 进行格式校验。
3. 若需调整分类或标签结构，请同步更新 `config/categories.json`，并在 Pull Request 描述中说明改动原因及影响范围。
4. 所有 Pull Request 需通过 GitHub Actions 的构建与探测测试（包含对新增 URL 的实时可达性检查），合并后会自动触发静态页重新构建并部署至预览环境。
5. 文档更新请直接修改 `docs/` 目录下的对应 Markdown 文件，保持与代码实现一致。涉及架构变动的较大改动，建议先开 Issue 讨论后再提交代码。

## 常见问题

Q: 为什么某些站点在探测结果中显示为失效，但浏览器中可以直接访问？

A: 探测服务默认使用无头 HTTP 客户端，不执行 JavaScript 重定向，且超时阈值设置为 5000 毫秒。部分站点可能依赖前端跳转或响应较慢，导致探测判定为超时。您可在 `config/probe-settings.json` 中调整 `timeout` 与 `followRedirects` 参数后重新运行监测。同时，探测结果仅代表服务端网络出口的可达性，不代表终端用户实际访问情况。

Q: 如何更新收录的链接列表？是否需要重新构建整个项目？

A: 您可以直接编辑 `data/sources.json` 文件，增加或删除站点条目。编辑保存后，运行 `npm run build` 即可重新生成导航页。若您同时运行了监测服务，监测进程会自动检测到 `sources.json` 的变更并在下一轮探测中更新目标列表，无需重启进程。

Q: 能否将本项目部署到不支持 Node.js 的纯静态托管环境（如 GitHub Pages）？

A: 可以。您只需在本地或 CI 环境中执行 `npm run build`，然后将 `dist/` 目录下的所有文件上传至任何静态托管服务即可。需要注意的是，监测服务需要长期运行的后端环境，因此若您只部署静态页，链接状态字段将保持为构建时的快照，不会自动更新。建议配合 GitHub Actions 定时任务构建，以实现半自动刷新。

## 许可证

MIT

> 外链数量: 5 | 生成时间: 2026-06-24 15:55:29
