# NetIndex

NetIndex 是一个面向技术研究人员、网络分析爱好者与内容聚合开发者的外部资源导航与元数据索引项目。本项目不存储、不托管、不转发任何第三方内容，仅以目录化方式整理并公开可用网络资源入口，供用户自行访问与评估。NetIndex 适用于需要快速定位特定类型内容站点、进行网络可访问性观测或构建个人研究素材库的场景，通过结构化索引降低信息筛选成本。

## 功能概览

- **站点目录分级索引**：按内容类型与运营特征对资源进行一级分类，支持快速筛选。
- **原始地址透明展示**：所有收录资源均以原始域名或 URL 原样呈现，不做隐含跳转或短链封装。
- **可用性状态标记**：结合外部检测数据，对每个资源入口提供基础可访问性提示（理论判定，非实时探测）。
- **分类标签系统**：为每个资源赋予类型标签（影视、素材、工具等），便于多维度检索。
- **版本化更新记录**：每批次索引变更附带更新日志，保持目录可追溯性。
- **外部参考信息聚合**：关联公共备案查询与 WHOIS 信息入口，辅助判断资源背景。
- **纯净只读输出**：所有资源链接以纯文本或代码块形式输出，不植入追踪参数或外链权重干扰。
- **机器可读格式支持**：提供 JSON 与 YAML 格式的索引导出，适配自动化脚本或二次开发需求。

## 应用场景

- **网络资源归档与观察**：研究人员可利用本索引定期记录特定类型域名的存活与变更情况，用于网络生态趋势分析。
- **内容聚合工具数据源**：开发者可将本索引作为外部数据源之一，用于构建自定义导航页或内容发现工具的前置入口列表。
- **运维与安全测试**：运维人员可通过索引快速获取测试用域名集合，用于网络策略验证、CDN 效果对比或延迟探测。
- **个人学习素材收集**：学生或爱好者可通过分类标签快速找到特定领域的公开资源站点，减少盲目搜索时间。
- **第三方服务集成测试**：需要外部视频或素材站作为集成测试样本时，可参考本索引获取稳定可用的测试入口。

## 快速开始

以下步骤适用于克隆本项目并运行本地索引服务或导出静态目录。

```bash
# 克隆仓库
git clone https://github.com/netindex/netindex.git

# 进入项目目录
cd netindex

# 安装依赖（基于 Python 3.10+）
pip install -r requirements.txt

# 生成静态索引页面（输出到 dist/ 目录）
python build.py --output dist/
```

## 安装要求

| 依赖 | 必需 | 说明 |
|------|------|------|
| Python 3.10 或更高版本 | 是 | 运行构建脚本与本地服务器的解释器环境 |
| pip 22.0+ | 是 | Python 包管理工具，用于安装依赖项 |
| Git 2.30+ | 是 | 克隆仓库及版本管理 |
| virtualenv（推荐） | 否 | 隔离 Python 环境，避免包冲突 |
| make 或 gnumake | 否 | 使用 Makefile 快捷执行构建任务 |
| curl / wget | 否 | 用于测试导出 API 或远程拉取更新包 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide.md | 如何浏览索引、使用分类筛选、导出数据格式？ |
| 维护手册 | docs/maintainer-guide.md | 如何提交新资源、更新状态、处理失效链接？ |
| API 参考 | docs/api-reference.md | 如何通过 HTTP 接口获取 JSON/YAML 索引数据？ |
| 架构设计 | docs/architecture.md | 索引存储结构、构建流程、缓存策略是怎样的？ |
| 变更日志 | CHANGELOG.md | 每个版本新增、移除或修正了哪些资源条目？ |

## 资源列表

以下为本批次（第 37/48 批）收录的全部外部资源入口。所有 URL 均按照原始来源原样列出，未做任何格式修改、协议补全或路径调整。

影视内容类

www.huashi1.skin
www.hyfilm.skin
www.lanhutv.site
www.liminyy.shop
www.liyavideo.autos

## 项目结构

```
netindex/
├── build.py                 # 主构建脚本，负责解析源数据并生成静态页面
├── config.yaml              # 全局配置文件（输出目录、分类映射、缓存TTL）
├── requirements.txt         # Python 依赖清单
├── Makefile                 # 常用任务快捷命令（build, serve, test）
├── README.md                # 项目说明文档（当前文件）
├── CHANGELOG.md             # 版本更新历史
├── LICENSE                  # MIT 许可证文本
├── src/                     # 核心源码目录
│   ├── parser/              # 资源列表解析模块
│   │   ├── __init__.py
│   │   └── list_loader.py   # 从 YAML/CSV 加载原始条目
│   ├── validator/           # URL 格式与基础可用性校验
│   │   ├── __init__.py
│   │   └── check_dns.py     # DNS 解析预检（非侵入）
│   ├── exporter/            # 多格式导出器
│   │   ├── __init__.py
│   │   ├── html_gen.py      # 生成静态 HTML 导航页
│   │   └── json_gen.py      # 输出 JSON 格式索引
│   └── utils/               # 通用工具函数
│       ├── __init__.py
│       └── log_helper.py    # 日志格式化与分级输出
├── data/                    # 数据源目录
│   ├── batch_37.yaml        # 第 37 批次原始条目（含分类标签）
│   ├── batch_38.yaml        # 第 38 批次原始条目（占位）
│   └── category_map.yaml    # 分类与标签映射表
├── dist/                    # 构建输出目录（默认，可配置）
│   ├── index.html           # 主导航页面
│   ├── index.json           # 机器可读 JSON 索引
│   └── index.yaml           # 机器可读 YAML 索引
├── tests/                   # 单元测试与集成测试
│   ├── test_parser.py
│   ├── test_validator.py
│   └── test_exporter.py
└── docs/                    # 详细文档
    ├── user-guide.md
    ├── maintainer-guide.md
    ├── api-reference.md
    └── architecture.md
```

## 贡献指南

我们欢迎社区提交资源新增、更新或移除建议。所有贡献需遵循以下流程：

1. 复刻本项目仓库，并在本地新建一个以 `batch-<编号>-<用户名>` 格式命名的分支。
2. 在 `data/` 目录下找到或创建对应批次的 YAML 文件，按照既定格式（名称、原始URL、分类标签、备注）添加或修改条目。对于已失效资源，请在备注中标注 `[unreachable]` 并保留原 URL。
3. 提交前运行 `make test` 确保所有单元测试通过，且构建脚本 `python build.py` 可正常生成 dist 目录。
4. 发起 Pull Request，并在描述中说明本次变更的动机、新增资源数量以及是否涉及失效链接清理。
5. 等待维护者审核。审核通过后，变更将合并至主分支并随下一批次更新发布。

## 常见问题

**问：NetIndex 是否代理或缓存外部资源的内容？**  
答：否。NetIndex 仅提供原始 URL 的文本索引，不代理任何请求，不缓存任何页面内容或媒体文件。所有访问行为均由用户端直接发起，与本站无关。

**问：收录的资源链接失效了怎么办？**  
答：您可以通过 GitHub Issues 提交失效反馈，或按照贡献指南提交 Pull Request 更新备注状态。我们会在每批次维护窗口统一复核并修正。

**问：是否可以申请移除某个资源链接？**  
答：可以。若您认为某个链接涉及侵权、违规或隐私问题，请通过项目邮箱（netindex@example.com）提交书面说明及身份证明材料，我们会在核实后于下一个版本中移除相关条目。

## 许可证

MIT License

Copyright (c) 2026 NetIndex Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 5 | 生成时间: 2026-06-24 15:55:30
