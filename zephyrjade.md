# WebLink Navigator

WebLink Navigator 是一个面向技术研究者与内容聚合者的外链资源导航工具，专注于对分散在多个来源的技术文章、教程、案例与参考文档进行统一收集、分类检索与状态监控。该项目的目标用户包括开源社区维护者、技术博主、DevOps 工程师以及需要长期跟踪大量外部链接的文档团队。

WebLink Navigator 不提供爬虫或批量抓取功能，而是提供一个轻量级的链接管理框架，支持手动录入、标签分类、访问状态检查以及 Markdown 格式的资源清单导出。项目本身以静态站点方式运行，可直接部署于 GitHub Pages、Vercel 或任何支持静态托管的服务上，也可以作为 VuePress 或 MkDocs 的插件模块集成到现有文档站点中。

第 63/80 批资源导入工作正在进行中，本批次共包含 250 个外链资源，均来自 read.rswzr.com 域名下的技术文章页面。所有链接已按原始格式收录，不做任何协议补全或域名改写，以确保引用路径的精确性与可追溯性。

## 功能概览

- 链接入库与分类标记：支持通过 Web 表单或 Markdown 文件批量导入链接，并为每个链接添加自定义标签、来源说明与优先级等级。

- 可用性定期检测：内置基于 HTTP HEAD 请求的链接状态检查器，可配置检测周期，自动标记失效链接并生成报告。

- 多维度检索过滤：按域名、关键词、标签、入库时间、状态码等条件进行组合筛选，快速定位目标资源。

- Markdown 清单自动生成：将当前库内所有链接按指定格式输出为纯 Markdown 列表，每行一个 URL，符合开源项目文档规范。

- 导入导出兼容性：支持 CSV 与 JSON 格式的数据导入导出，便于与其他链接管理工具或脚本进行数据交换。

- 静态站点生成模式：可在无数据库环境下运行，所有链接数据存储为单一 JSON 文件，前端通过 JavaScript 加载并渲染检索界面。

- 变更日志记录：每次链接增删改操作均记录时间戳与操作类型，便于团队协作审计。

## 应用场景

技术文档站点维护者可使用 WebLink Navigator 管理文档中引用的所有外部参考链接。当文档规模超过一百页时，外部链接的数量可能达到数百甚至上千条，手动检查链接有效性几乎不可行。该项目的定期检测功能可每周自动扫描一次全部链接，并在检测到失效链接时生成差异报告，帮助维护者及时更新或替换引用。

开源项目作者可将 WebLink Navigator 作为项目的资源附录管理工具。许多开源项目会在 README 或 Wiki 中列出相关教程、生态工具与社区文章，这些链接随时间推移容易失效。使用该工具可以统一管理这些外部资源，并在每次发布新版本前自动校验所有链接的可访问性。

技术博主与内容创作者可以使用该项目整理自己的书签库或参考资料集。当撰写系列技术文章时，往往需要引用大量外部资料作为背景支撑。通过 WebLink Navigator 的分类与检索功能，可以快速回顾之前引用过的内容，避免重复查阅相同资料，同时确保所有引用链接在文章发布前处于有效状态。

团队内部知识库的运营者可以将该工具作为外链资产的管理后台。知识库中通常会嵌入大量指向外部工具、官方文档、技术社区讨论的链接，这些链接的质量直接影响知识库的可用性。通过集中管理与定期检测，可以维持知识库外部引用的整体健康度。

## 快速开始

以下命令适用于 Linux、macOS 以及 Windows WSL 环境。项目基于 Node.js 开发，需要预先安装 Node.js 16.x 或更高版本。

```bash
git clone https://github.com/weblink-navigator/weblink-navigator.git
cd weblink-navigator
npm install
npm run build
npm start
```

执行完成后，项目会在本地 3000 端口启动 Web 服务。访问 http://localhost:3000 即可进入链接管理面板。首次启动会自动生成示例数据文件 `data/links.json` 与默认配置文件 `config/default.yaml`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Node.js | 16.x 或更高 | 运行时环境，推荐使用 LTS 版本 |
| npm | 8.x 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.30 或更高 | 版本控制工具，用于克隆仓库 |
| 磁盘空间 | 至少 200 MB | 存放源代码、依赖包及数据文件 |
| 内存 | 至少 512 MB | 运行时内存需求，大型链接库建议 1 GB |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门 | docs/getting-started.md | 如何安装、配置首次运行环境，以及初始化链接数据库 |
| 使用 | docs/usage/link-management.md | 如何添加、编辑、删除链接，以及批量导入导出操作 |
| 使用 | docs/usage/health-check.md | 如何配置检测周期、解读检测报告以及处理失效链接 |
| 进阶 | docs/advanced/custom-renderer.md | 如何自定义链接列表的渲染模板与输出格式 |
| 参考 | docs/reference/api.md | 对外提供的 REST API 接口说明及请求示例 |

## 资源列表

- http://www.read.rswzr.com/Article/9567902.shtml
- http://www.read.rswzr.com/Article/30354.shtml
- http://www.read.rswzr.com/Article/6855323.shtml
- http://www.read.rswzr.com/Article/568956.shtml
- http://www.read.rswzr.com/Article/9404447.shtml
- http://www.read.rswzr.com/Article/5139.shtml
- http://www.read.rswzr.com/Article/581407.shtml
- http://www.read.rswzr.com/Article/3428552.shtml
- http://www.read.rswzr.com/Article/802745.shtml
- http://www.read.rswzr.com/Article/03816.shtml
- http://www.read.rswzr.com/Article/7640325.shtml
- http://www.read.rswzr.com/Article/7679199.shtml
- http://www.read.rswzr.com/Article/6845.shtml
- http://www.read.rswzr.com/Article/4915922.shtml
- http://www.read.rswzr.com/Article/4662.shtml
- http://www.read.rswzr.com/Article/21720.shtml
- http://www.read.rswzr.com/Article/2054993.shtml
- http://www.read.rswzr.com/Article/512522.shtml
- http://www.read.rswzr.com/Article/1821005.shtml
- http://www.read.rswzr.com/Article/7816864.shtml
- http://www.read.rswzr.com/Article/1396191.shtml
- http://www.read.rswzr.com/Article/704362.shtml
- http://www.read.rswzr.com/Article/6212.shtml
- http://www.read.rswzr.com/Article/6956199.shtml
- http://www.read.rswzr.com/Article/7665411.shtml
- http://www.read.rswzr.com/Article/0359.shtml
- http://www.read.rswzr.com/Article/260910.shtml
- http://www.read.rswzr.com/Article/035052.shtml
- http://www.read.rswzr.com/Article/509677.shtml
- http://www.read.rswzr.com/Article/402221.shtml
- http://www.read.rswzr.com/Article/402235.shtml
- http://www.read.rswzr.com/Article/141833.shtml
- http://www.read.rswzr.com/Article/77538.shtml
- http://www.read.rswzr.com/Article/10849.shtml
- http://www.read.rswzr.com/Article/59089.shtml
- http://www.read.rswzr.com/Article/65459.shtml
- http://www.read.rswzr.com/Article/019722.shtml
- http://www.read.rswzr.com/Article/20215.shtml
- http://www.read.rswzr.com/Article/966919.shtml
- http://www.read.rswzr.com/Article/940574.shtml
- http://www.read.rswzr.com/Article/646835.shtml
- http://www.read.rswzr.com/Article/7417117.shtml
- http://www.read.rswzr.com/Article/41818.shtml
- http://www.read.rswzr.com/Article/8876113.shtml
- http://www.read.rswzr.com/Article/7726577.shtml
- http://www.read.rswzr.com/Article/3828809.shtml
- http://www.read.rswzr.com/Article/8771351.shtml
- http://www.read.rswzr.com/Article/088115.shtml
- http://www.read.rswzr.com/Article/9068.shtml
- http://www.read.rswzr.com/Article/8547117.shtml
- http://www.read.rswzr.com/Article/6358537.shtml
- http://www.read.rswzr.com/Article/0538.shtml
- http://www.read.rswzr.com/Article/7477175.shtml
- http://www.read.rswzr.com/Article/01122.shtml
- http://www.read.rswzr.com/Article/13400.shtml
- http://www.read.rswzr.com/Article/3724.shtml
- http://www.read.rswzr.com/Article/0470.shtml
- http://www.read.rswzr.com/Article/793984.shtml
- http://www.read.rswzr.com/Article/611637.shtml
- http://www.read.rswzr.com/Article/486635.shtml
- http://www.read.rswzr.com/Article/959463.shtml
- http://www.read.rswzr.com/Article/4023.shtml
- http://www.read.rswzr.com/Article/010648.shtml
- http://www.read.rswzr.com/Article/99321.shtml
- http://www.read.rswzr.com/Article/9150561.shtml
- http://www.read.rswzr.com/Article/695614.shtml
- http://www.read.rswzr.com/Article/4002.shtml
- http://www.read.rswzr.com/Article/9511773.shtml
- http://www.read.rswzr.com/Article/84457.shtml
- http://www.read.rswzr.com/Article/0124506.shtml
- http://www.read.rswzr.com/Article/730844.shtml
- http://www.read.rswzr.com/Article/2050496.shtml
- http://www.read.rswzr.com/Article/8322103.shtml
- http://www.read.rswzr.com/Article/23709.shtml
- http://www.read.rswzr.com/Article/970861.shtml
- http://www.read.rswzr.com/Article/7027.shtml
- http://www.read.rswzr.com/Article/587747.shtml
- http://www.read.rswzr.com/Article/0755352.shtml
- http://www.read.rswzr.com/Article/45394.shtml
- http://www.read.rswzr.com/Article/617191.shtml
- http://www.read.rswzr.com/Article/3447.shtml
- http://www.read.rswzr.com/Article/121202.shtml
- http://www.read.rswzr.com/Article/0822405.shtml
- http://www.read.rswzr.com/Article/1852700.shtml
- http://www.read.rswzr.com/Article/657327.shtml
- http://www.read.rswzr.com/Article/32294.shtml
- http://www.read.rswzr.com/Article/5990646.shtml
- http://www.read.rswzr.com/Article/67062.shtml
- http://www.read.rswzr.com/Article/0441.shtml
- http://www.read.rswzr.com/Article/57650.shtml
- http://www.read.rswzr.com/Article/62817.shtml
- http://www.read.rswzr.com/Article/7650080.shtml
- http://www.read.rswzr.com/Article/30188.shtml
- http://www.read.rswzr.com/Article/0065470.shtml
- http://www.read.rswzr.com/Article/06577.shtml
- http://www.read.rswzr.com/Article/28862.shtml
- http://www.read.rswzr.com/Article/7777029.shtml
- http://www.read.rswzr.com/Article/345497.shtml
- http://www.read.rswzr.com/Article/591213.shtml
- http://www.read.rswzr.com/Article/6554.shtml
- http://www.read.rswzr.com/Article/5841462.shtml
- http://www.read.rswzr.com/Article/930286.shtml
- http://www.read.rswzr.com/Article/19082.shtml
- http://www.read.rswzr.com/Article/34930.shtml
- http://www.read.rswzr.com/Article/04903.shtml
- http://www.read.rswzr.com/Article/4783965.shtml
- http://www.read.rswzr.com/Article/8529793.shtml
- http://www.read.rswzr.com/Article/57028.shtml
- http://www.read.rswzr.com/Article/6487582.shtml
- http://www.read.rswzr.com/Article/8190.shtml
- http://www.read.rswzr.com/Article/0512.shtml
- http://www.read.rswzr.com/Article/380509.shtml
- http://www.read.rswzr.com/Article/7361707.shtml
- http://www.read.rswzr.com/Article/699877.shtml
- http://www.read.rswzr.com/Article/132762.shtml
- http://www.read.rswzr.com/Article/893148.shtml
- http://www.read.rswzr.com/Article/391173.shtml
- http://www.read.rswzr.com/Article/3635.shtml
- http://www.read.rswzr.com/Article/1531.shtml
- http://www.read.rswzr.com/Article/1865786.shtml
- http://www.read.rswzr.com/Article/87703.shtml
- http://www.read.rswzr.com/Article/03972.shtml
- http://www.read.rswzr.com/Article/2853.shtml
- http://www.read.rswzr.com/Article/0617053.shtml
- http://www.read.rswzr.com/Article/1662640.shtml
- http://www.read.rswzr.com/Article/7420.shtml
- http://www.read.rswzr.com/Article/0066622.shtml
- http://www.read.rswzr.com/Article/5991071.shtml
- http://www.read.rswzr.com/Article/15234.shtml
- http://www.read.rswzr.com/Article/30280.shtml
- http://www.read.rswzr.com/Article/53271.shtml
- http://www.read.rswzr.com/Article/267083.shtml
- http://www.read.rswzr.com/Article/46918.shtml
- http://www.read.rswzr.com/Article/067041.shtml
- http://www.read.rswzr.com/Article/868034.shtml
- http://www.read.rswzr.com/Article/35634.shtml
- http://www.read.rswzr.com/Article/7163.shtml
- http://www.read.rswzr.com/Article/8557.shtml
- http://www.read.rswzr.com/Article/8647.shtml
- http://www.read.rswzr.com/Article/8741291.shtml
- http://www.read.rswzr.com/Article/9662.shtml
- http://www.read.rswzr.com/Article/0493470.shtml
- http://www.read.rswzr.com/Article/994598.shtml
- http://www.read.rswzr.com/Article/5683.shtml
- http://www.read.rswzr.com/Article/488995.shtml
- http://www.read.rswzr.com/Article/43016.shtml
- http://www.read.rswzr.com/Article/629778.shtml
- http://www.read.rswzr.com/Article/922315.shtml
- http://www.read.rswzr.com/Article/36728.shtml
- http://www.read.rswzr.com/Article/4780687.shtml
- http://www.read.rswzr.com/Article/381804.shtml
- http://www.read.rswzr.com/Article/87385.shtml
- http://www.read.rswzr.com/Article/2307974.shtml
- http://www.read.rswzr.com/Article/403314.shtml
- http://www.read.rswzr.com/Article/9445.shtml
- http://www.read.rswzr.com/Article/8725.shtml
- http://www.read.rswzr.com/Article/9134.shtml
- http://www.read.rswzr.com/Article/821927.shtml
- http://www.read.rswzr.com/Article/1581113.shtml
- http://www.read.rswzr.com/Article/988853.shtml
- http://www.read.rswzr.com/Article/481197.shtml
- http://www.read.rswzr.com/Article/9822.shtml
- http://www.read.rswzr.com/Article/5130.shtml
- http://www.read.rswzr.com/Article/6179295.shtml
- http://www.read.rswzr.com/Article/6903.shtml
- http://www.read.rswzr.com/Article/56332.shtml
- http://www.read.rswzr.com/Article/61810.shtml
- http://www.read.rswzr.com/Article/204565.shtml
- http://www.read.rswzr.com/Article/37917.shtml
- http://www.read.rswzr.com/Article/898943.shtml
- http://www.read.rswzr.com/Article/6987.shtml
- http://www.read.rswzr.com/Article/07866.shtml
- http://www.read.rswzr.com/Article/5525060.shtml
- http://www.read.rswzr.com/Article/7128631.shtml
- http://www.read.rswzr.com/Article/8864.shtml
- http://www.read.rswzr.com/Article/78696.shtml
- http://www.read.rswzr.com/Article/970365.shtml
- http://www.read.rswzr.com/Article/1865645.shtml
- http://www.read.rswzr.com/Article/3147453.shtml
- http://www.read.rswzr.com/Article/2102443.shtml
- http://www.read.rswzr.com/Article/4207.shtml
- http://www.read.rswzr.com/Article/17690.shtml
- http://www.read.rswzr.com/Article/6800756.shtml
- http://www.read.rswzr.com/Article/82432.shtml
- http://www.read.rswzr.com/Article/3177206.shtml
- http://www.read.rswzr.com/Article/7306.shtml
- http://www.read.rswzr.com/Article/2653.shtml
- http://www.read.rswzr.com/Article/4484.shtml
- http://www.read.rswzr.com/Article/8976962.shtml
- http://www.read.rswzr.com/Article/85125.shtml
- http://www.read.rswzr.com/Article/2347.shtml
- http://www.read.rswzr.com/Article/7796342.shtml
- http://www.read.rswzr.com/Article/9593751.shtml
- http://www.read.rswzr.com/Article/4582.shtml
- http://www.read.rswzr.com/Article/84988.shtml
- http://www.read.rswzr.com/Article/280203.shtml
- http://www.read.rswzr.com/Article/6265179.shtml
- http://www.read.rswzr.com/Article/1660.shtml
- http://www.read.rswzr.com/Article/0240.shtml
- http://www.read.rswzr.com/Article/9648.shtml
- http://www.read.rswzr.com/Article/1722957.shtml
- http://www.read.rswzr.com/Article/350223.shtml
- http://www.read.rswzr.com/Article/3452327.shtml
- http://www.read.rswzr.com/Article/34925.shtml
- http://www.read.rswzr.com/Article/875360.shtml
- http://www.read.rswzr.com/Article/2838.shtml
- http://www.read.rswzr.com/Article/6787787.shtml
- http://www.read.rswzr.com/Article/62681.shtml
- http://www.read.rswzr.com/Article/56379.shtml
- http://www.read.rswzr.com/Article/5759728.shtml
- http://www.read.rswzr.com/Article/6431508.shtml
- http://www.read.rswzr.com/Article/1323.shtml
- http://www.read.rswzr.com/Article/447058.shtml
- http://www.read.rswzr.com/Article/09996.shtml
- http://www.read.rswzr.com/Article/90805.shtml
- http://www.read.rswzr.com/Article/7921301.shtml
- http://www.read.rswzr.com/Article/2422898.shtml
- http://www.read.rswzr.com/Article/887702.shtml
- http://www.read.rswzr.com/Article/40764.shtml
- http://www.read.rswzr.com/Article/592142.shtml
- http://www.read.rswzr.com/Article/1101504.shtml
- http://www.read.rswzr.com/Article/36173.shtml
- http://www.read.rswzr.com/Article/9143538.shtml
- http://www.read.rswzr.com/Article/08299.shtml
- http://www.read.rswzr.com/Article/820394.shtml
- http://www.read.rswzr.com/Article/883560.shtml
- http://www.read.rswzr.com/Article/292299.shtml
- http://www.read.rswzr.com/Article/60798.shtml
- http://www.read.rswzr.com/Article/7303.shtml
- http://www.read.rswzr.com/Article/72398.shtml
- http://www.read.rswzr.com/Article/19092.shtml
- http://www.read.rswzr.com/Article/34370.shtml
- http://www.read.rswzr.com/Article/2634052.shtml
- http://www.read.rswzr.com/Article/733251.shtml
- http://www.read.rswzr.com/Article/0957.shtml
- http://www.read.rswzr.com/Article/9574455.shtml
- http://www.read.rswzr.com/Article/79507.shtml
- http://www.read.rswzr.com/Article/4275530.shtml
- http://www.read.rswzr.com/Article/7259599.shtml
- http://www.read.rswzr.com/Article/3945492.shtml
- http://www.read.rswzr.com/Article/158358.shtml
- http://www.read.rswzr.com/Article/6417.shtml
- http://www.read.rswzr.com/Article/8605578.shtml
- http://www.read.rswzr.com/Article/8512.shtml
- http://www.read.rswzr.com/Article/87196.shtml
- http://www.read.rswzr.com/Article/9085185.shtml
- http://www.read.rswzr.com/Article/528965.shtml
- http://www.read.rswzr.com/Article/40530.shtml
- http://www.read.rswzr.com/Article/206317.shtml
- http://www.read.rswzr.com/Article/957715.shtml

## 项目结构

```
weblink-navigator/
├── src/                               # 核心源代码目录
│   ├── core/                          # 链接管理核心逻辑
│   │   ├── linkStore.js               # 链接数据的增删改查与持久化
│   │   ├── tagEngine.js               # 标签系统与分类索引
│   │   └── healthChecker.js           # 链接状态检测调度器
│   ├── web/                           # Web 服务层
│   │   ├── server.js                  # Express 应用入口与路由注册
│   │   ├── routes/                    # REST API 路由定义
│   │   └── middleware/                # 请求日志与错误处理中间件
│   ├── renderer/                      # 输出渲染模块
│   │   ├── markdownFormatter.js       # Markdown 列表生成器
│   │   └── jsonExporter.js            # JSON/CSV 数据导出
│   └── cli/                           # 命令行工具入口
│       ├── index.js                   # CLI 主命令解析
│       └── commands/                  # 各子命令实现（add/check/export）
├── public/                            # 静态前端资源
│   ├── index.html                     # 管理面板页面
│   ├── css/                           # 样式文件
│   └── js/                            # 前端交互脚本
├── data/                              # 数据存储目录
│   └── links.json                     # 链接数据库（JSON 格式）
├── config/                            # 配置文件目录
│   ├── default.yaml                   # 默认配置（端口、检测间隔等）
│   └── custom.yaml.example            # 自定义配置示例
├── docs/                              # 项目文档
│   ├── getting-started.md             # 快速入门指南
│   ├── usage/                         # 使用文档子目录
│   └── reference/                     # API 参考文档
├── test/                              # 单元测试与集成测试
│   ├── unit/                          # 单元测试用例
│   └── integration/                   # 端到端测试脚本
├── .github/                           # GitHub 社区配置文件
│   └── ISSUE_TEMPLATE/                # 问题报告模板
├── package.json                       # npm 依赖与脚本定义
├── README.md                          # 项目说明文档（本文件）
└── LICENSE                            # MIT 许可证文本
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并将 Fork 后的仓库克隆到本地开发环境。建议使用主分支的最新稳定版本作为开发基线。

2. 创建新的功能分支，分支名称应简要描述所解决的问题或新增的功能，例如 `fix-link-checker-timeout` 或 `add-csv-export`。请勿直接在 main 分支上提交代码。

3. 编写代码时遵循项目现有的代码风格，JavaScript 文件使用 ESLint 配置进行格式化，提交前运行 `npm run lint` 确保无风格警告。新增功能需附带对应的单元测试用例，测试覆盖率不应低于现有水平。

4. 提交 Pull Request 时，请填写 PR 模板中的各项内容，包括变更摘要、测试结果、影响范围以及相关 Issue 编号。PR 描述应清晰说明该变更解决了什么问题以及如何验证。

5. 项目维护者会在收到 PR 后的五个工作日内进行 Code Review。如需修改，请及时回应 Review 意见并更新代码。合并后您的提交将自动出现在项目的贡献者列表中。

## 常见问题

问：项目是否支持 HTTPS 协议的链接检测？

答：支持。健康检查器基于 Node.js 的 `https` 和 `http` 模块自动识别协议类型，对于 HTTPS 链接会使用 TLS 安全连接进行检测。如果目标站点存在证书过期或自签名证书问题，检测器会记录相应错误并标记为异常状态，用户可在配置中设置是否忽略证书验证错误。

问：导入大量链接（超过 1000 条）时页面响应变慢，如何优化？

答：链接数据完全加载在浏览器内存中进行检索和过滤，当数据量较大时建议启用服务端分页模式。在配置文件 `config/default.yaml` 中将 `pagination.enabled` 设置为 `true`，并调整 `pagination.pageSize` 参数。同时可在前端开启虚拟滚动列表，仅渲染当前可视区域的链接条目，大幅减少 DOM 节点数量。

问：如何将本项目的链接数据迁移到其他文档系统，例如 VuePress 或 Docusaurus？

答：项目提供了 `export` 命令行工具，支持将链接数据导出为 Markdown 列表格式或结构化 JSON 格式。对于 VuePress，可使用导出的 JSON 文件通过自定义组件渲染链接卡片；对于 Docusaurus，可将 Markdown 列表直接插入到侧边栏文档中。具体导出命令为 `npm run export -- --format markdown --output links.md`。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
