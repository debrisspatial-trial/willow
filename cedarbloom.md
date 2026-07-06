# LinkVault 技术资源聚合系统

LinkVault 是一个面向开发者与技术研究人员的分布式外链资源聚合与导航平台。该项目通过对多源技术文章、文档、教程及行业分析链接进行结构化收录与分类标注，构建一个高可读性、低噪音的技术阅读入口。目标用户包括运维工程师、全栈开发者、技术决策者以及开源贡献者，帮助其在海量信息中快速定位高价值技术内容，减少重复检索成本，提升研究效率。

LinkVault 不生产内容，而是通过严谨的链接筛选机制、版本化的资源目录以及轻量级元数据标记，为技术社区提供一个可靠的外链参考系。项目自身采用静态站点生成方案，可低成本部署于任何 Web 服务器或对象存储平台，适合个人开发者或小型团队作为知识管理底座进行二次开发。

## 功能概览

**批量链接导入与去重**：支持从文本文件、CSV 或直接粘贴的原始 URL 列表中批量导入链接，系统自动执行语法校验与重复性检测，确保资源库的纯净度。

**分类标签与全文检索**：每个收录链接可绑定多个自定义标签（如 Kubernetes、Python、安全审计），并支持基于标题、描述及标签的全文检索引擎，检索结果按相关度排序。

**资源状态监控与可用性探测**：后台定时任务对已收录链接进行 HTTP 状态码检查，自动标记失效或重定向链接，并生成健康度报告，便于管理员及时清理或更新。

**自定义元数据扩展**：每条记录除标准字段（URL、标题、来源站点、收录时间）外，支持通过 JSON Schema 扩展自定义属性，例如阅读时长、技术等级、关联 Issue 编号等。

**多维度视图输出**：内置卡片视图、列表视图与紧凑表格视图三种展示模式，同时支持按日期、分类、来源域名进行筛选与排序，适应不同阅读偏好。

**开放 API 接口**：提供 RESTful API 用于外部系统集成，支持查询、新增及批量更新操作，API 响应格式兼容 JSON 与 RSS，便于构建自动化工作流。

**静态站点生成引擎**：基于配置的模板主题，将资源数据渲染为完整的静态 HTML 站点，输出结果可直接部署至 Nginx、Apache 或 S3 兼容存储，无需运行时数据库依赖。

## 应用场景

技术团队内部知识库构建：开发团队可将日常遇到的优质技术博客、官方文档及故障排查案例统一收录至 LinkVault，形成团队共享的技术备忘录。新成员入职时，可通过标签筛选快速了解团队关注的技术栈方向与常用工具链。

个人技术阅读工作流优化：技术爱好者可定期将 Hacker News、Reddit 或技术周报中发现的感兴趣文章导入系统，利用状态监控功能跟踪未读内容，避免链接丢失或遗忘。周末集中阅读时，按时间倒序排列即可获得待读清单。

开源项目参考附录管理：开源项目维护者可以在项目仓库的 README 或 Wiki 中引用 LinkVault 生成的资源列表，作为补充参考资料。例如，某数据库中间件项目可将所有相关的性能测试报告、调优案例及社区 FAQ 链接统一托管，降低用户获取背景知识的门槛。

技术内容聚合站运维：个人站长或小规模内容平台可使用 LinkVault 管理外链投稿与友链交换，借助分类标签与健康度探测功能，自动化筛选有效链接，减少人工审核工作量，同时为访问者提供稳定的导航服务。

## 快速开始

以下指令适用于 Linux / macOS / Windows WSL 环境，需提前安装 Git 与 Node.js 18.x 及以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/linkvault/linkvault-core.git
cd linkvault-core

# 安装项目依赖
npm install --production=false

# 执行初始链接导入（示例数据）
npm run seed:links -- --source ./data/sample_urls.txt

# 启动开发服务器
npm run dev
```

执行完毕后，访问 http://localhost:5173 即可查看本地实例。如需构建生产环境静态文件，请执行 `npm run build`，输出目录为 `./dist`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境与包管理基础 |
| npm | 9.x 或 10.x | 依赖安装与脚本执行工具 |
| SQLite3 | 系统级或内嵌 | 默认元数据存储引擎，无需额外配置 |
| Git | 2.30 及以上 | 版本控制与仓库克隆 |
| 内存 | 最低 512 MB | 开发模式建议 1 GB 以上 |
| 磁盘空间 | 最低 200 MB | 含依赖库与构建缓存 |
| 操作系统 | Linux / macOS / Windows 10+ | 跨平台支持，WSL 可正常运行 |
| 浏览器 | 现代浏览器（Chrome 110+ / Firefox 110+） | 仅开发预览与后台管理界面需要 |
| 网络 | 出站可达 | 用于链接状态检查与外部资源加载 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/guide/getting-started.md | 如何在一分钟内跑起实例？如何导入第一批链接？ |
| 配置手册 | docs/guide/configuration.md | 环境变量有哪些？如何修改站点标题与主题样式？ |
| API 参考 | docs/api/restful-api.md | 如何通过接口新增链接？查询参数如何构造？ |
| 部署指引 | docs/guide/deployment.md | 支持哪些部署方式？如何配置 Nginx 反向代理？ |
| 架构说明 | docs/architecture/overview.md | 系统由哪些模块组成？数据流如何流转？ |
| 数据格式 | docs/architecture/data-schema.md | 链接记录的 JSON 结构是什么？标签如何存储？ |
| 主题开发 | docs/development/theme-custom.md | 如何编写自定义模板？静态生成钩子如何使用？ |
| 贡献规范 | CONTRIBUTING.md | 提交 PR 前需要运行哪些检查？Commit 信息格式有何要求？ |

## 资源列表

- http://www.read.xwpxi.com/Article/965377.shtml
- http://www.read.xwpxi.com/Article/626361.shtml
- http://www.read.xwpxi.com/Article/3426949.shtml
- http://www.read.xwpxi.com/Article/90359.shtml
- http://www.read.xwpxi.com/Article/17847.shtml
- http://www.read.xwpxi.com/Article/1275458.shtml
- http://www.read.xwpxi.com/Article/21656.shtml
- http://www.read.xwpxi.com/Article/3413733.shtml
- http://www.read.xwpxi.com/Article/487816.shtml
- http://www.read.xwpxi.com/Article/07535.shtml
- http://www.read.xwpxi.com/Article/29273.shtml
- http://www.read.xwpxi.com/Article/768409.shtml
- http://www.read.xwpxi.com/Article/167889.shtml
- http://www.read.xwpxi.com/Article/0811.shtml
- http://www.read.xwpxi.com/Article/34038.shtml
- http://www.read.xwpxi.com/Article/8307956.shtml
- http://www.read.xwpxi.com/Article/6435.shtml
- http://www.read.xwpxi.com/Article/635151.shtml
- http://www.read.xwpxi.com/Article/0768.shtml
- http://www.read.xwpxi.com/Article/16267.shtml
- http://www.read.xwpxi.com/Article/8503844.shtml
- http://www.read.xwpxi.com/Article/88062.shtml
- http://www.read.xwpxi.com/Article/57027.shtml
- http://www.read.xwpxi.com/Article/878259.shtml
- http://www.read.xwpxi.com/Article/9099765.shtml
- http://www.read.xwpxi.com/Article/7005173.shtml
- http://www.read.xwpxi.com/Article/971324.shtml
- http://www.read.xwpxi.com/Article/395885.shtml
- http://www.read.xwpxi.com/Article/447329.shtml
- http://www.read.xwpxi.com/Article/88632.shtml
- http://www.read.xwpxi.com/Article/80289.shtml
- http://www.read.xwpxi.com/Article/536085.shtml
- http://www.read.xwpxi.com/Article/2770264.shtml
- http://www.read.xwpxi.com/Article/7703828.shtml
- http://www.read.xwpxi.com/Article/67447.shtml
- http://www.read.xwpxi.com/Article/55991.shtml
- http://www.read.xwpxi.com/Article/7070.shtml
- http://www.read.xwpxi.com/Article/22199.shtml
- http://www.read.xwpxi.com/Article/1713436.shtml
- http://www.read.xwpxi.com/Article/73900.shtml
- http://www.read.xwpxi.com/Article/5151.shtml
- http://www.read.xwpxi.com/Article/7443646.shtml
- http://www.read.xwpxi.com/Article/0091005.shtml
- http://www.read.xwpxi.com/Article/4220.shtml
- http://www.read.xwpxi.com/Article/1120.shtml
- http://www.read.xwpxi.com/Article/035492.shtml
- http://www.read.xwpxi.com/Article/2145619.shtml
- http://www.read.xwpxi.com/Article/7617.shtml
- http://www.read.xwpxi.com/Article/5626740.shtml
- http://www.read.xwpxi.com/Article/31026.shtml
- http://www.read.xwpxi.com/Article/6556029.shtml
- http://www.read.xwpxi.com/Article/1053172.shtml
- http://www.read.xwpxi.com/Article/77020.shtml
- http://www.read.xwpxi.com/Article/251939.shtml
- http://www.read.xwpxi.com/Article/33009.shtml
- http://www.read.xwpxi.com/Article/90789.shtml
- http://www.read.xwpxi.com/Article/0443956.shtml
- http://www.read.xwpxi.com/Article/423148.shtml
- http://www.read.xwpxi.com/Article/8549236.shtml
- http://www.read.xwpxi.com/Article/44873.shtml
- http://www.read.xwpxi.com/Article/7427.shtml
- http://www.read.xwpxi.com/Article/6794772.shtml
- http://www.read.xwpxi.com/Article/396735.shtml
- http://www.read.xwpxi.com/Article/635902.shtml
- http://www.read.xwpxi.com/Article/95355.shtml
- http://www.read.xwpxi.com/Article/319502.shtml
- http://www.read.xwpxi.com/Article/7662.shtml
- http://www.read.xwpxi.com/Article/17841.shtml
- http://www.read.xwpxi.com/Article/65671.shtml
- http://www.read.xwpxi.com/Article/6924391.shtml
- http://www.read.xwpxi.com/Article/5765.shtml
- http://www.read.xwpxi.com/Article/06270.shtml
- http://www.read.xwpxi.com/Article/19375.shtml
- http://www.read.xwpxi.com/Article/158115.shtml
- http://www.read.xwpxi.com/Article/8913.shtml
- http://www.read.xwpxi.com/Article/4737.shtml
- http://www.read.xwpxi.com/Article/84565.shtml
- http://www.read.xwpxi.com/Article/8039075.shtml
- http://www.read.xwpxi.com/Article/630666.shtml
- http://www.read.xwpxi.com/Article/068503.shtml
- http://www.read.xwpxi.com/Article/678449.shtml
- http://www.read.xwpxi.com/Article/25530.shtml
- http://www.read.xwpxi.com/Article/1258.shtml
- http://www.read.xwpxi.com/Article/9377.shtml
- http://www.read.xwpxi.com/Article/8599893.shtml
- http://www.read.xwpxi.com/Article/23459.shtml
- http://www.read.xwpxi.com/Article/604457.shtml
- http://www.read.xwpxi.com/Article/4404871.shtml
- http://www.read.xwpxi.com/Article/9715850.shtml
- http://www.read.xwpxi.com/Article/72305.shtml
- http://www.read.xwpxi.com/Article/6930.shtml
- http://www.read.xwpxi.com/Article/4465354.shtml
- http://www.read.xwpxi.com/Article/449172.shtml
- http://www.read.xwpxi.com/Article/509995.shtml
- http://www.read.xwpxi.com/Article/2871.shtml
- http://www.read.xwpxi.com/Article/00375.shtml
- http://www.read.xwpxi.com/Article/59762.shtml
- http://www.read.xwpxi.com/Article/24580.shtml
- http://www.read.xwpxi.com/Article/634163.shtml
- http://www.read.xwpxi.com/Article/1802.shtml
- http://www.read.xwpxi.com/Article/9341442.shtml
- http://www.read.xwpxi.com/Article/92399.shtml
- http://www.read.xwpxi.com/Article/31824.shtml
- http://www.read.xwpxi.com/Article/9405436.shtml
- http://www.read.xwpxi.com/Article/7820.shtml
- http://www.read.xwpxi.com/Article/4178436.shtml
- http://www.read.xwpxi.com/Article/768952.shtml
- http://www.read.xwpxi.com/Article/38223.shtml
- http://www.read.xwpxi.com/Article/9868721.shtml
- http://www.read.xwpxi.com/Article/72801.shtml
- http://www.read.xwpxi.com/Article/9668899.shtml
- http://www.read.xwpxi.com/Article/3620.shtml
- http://www.read.xwpxi.com/Article/0477921.shtml
- http://www.read.xwpxi.com/Article/96148.shtml
- http://www.read.xwpxi.com/Article/052438.shtml
- http://www.read.xwpxi.com/Article/4657810.shtml
- http://www.read.xwpxi.com/Article/308377.shtml
- http://www.read.xwpxi.com/Article/7680446.shtml
- http://www.read.xwpxi.com/Article/5338128.shtml
- http://www.read.xwpxi.com/Article/72283.shtml
- http://www.read.xwpxi.com/Article/75678.shtml
- http://www.read.xwpxi.com/Article/55350.shtml
- http://www.read.xwpxi.com/Article/8964.shtml
- http://www.read.xwpxi.com/Article/904028.shtml
- http://www.read.xwpxi.com/Article/970251.shtml
- http://www.read.xwpxi.com/Article/7808649.shtml
- http://www.read.xwpxi.com/Article/2409510.shtml
- http://www.read.xwpxi.com/Article/5172.shtml
- http://www.read.xwpxi.com/Article/1167.shtml
- http://www.read.xwpxi.com/Article/481353.shtml
- http://www.read.xwpxi.com/Article/59223.shtml
- http://www.read.xwpxi.com/Article/22124.shtml
- http://www.read.xwpxi.com/Article/5206.shtml
- http://www.read.xwpxi.com/Article/15788.shtml
- http://www.read.xwpxi.com/Article/63279.shtml
- http://www.read.xwpxi.com/Article/44324.shtml
- http://www.read.xwpxi.com/Article/732740.shtml
- http://www.read.xwpxi.com/Article/258640.shtml
- http://www.read.xwpxi.com/Article/900880.shtml
- http://www.read.xwpxi.com/Article/9612.shtml
- http://www.read.xwpxi.com/Article/6516628.shtml
- http://www.read.xwpxi.com/Article/60562.shtml
- http://www.read.xwpxi.com/Article/72369.shtml
- http://www.read.xwpxi.com/Article/010276.shtml
- http://www.read.xwpxi.com/Article/3598066.shtml
- http://www.read.xwpxi.com/Article/039945.shtml
- http://www.read.xwpxi.com/Article/822801.shtml
- http://www.read.xwpxi.com/Article/763035.shtml
- http://www.read.xwpxi.com/Article/80923.shtml
- http://www.read.xwpxi.com/Article/6357.shtml
- http://www.read.xwpxi.com/Article/4948865.shtml
- http://www.read.xwpxi.com/Article/9063.shtml
- http://www.read.xwpxi.com/Article/92861.shtml
- http://www.read.xwpxi.com/Article/6799079.shtml
- http://www.read.xwpxi.com/Article/636197.shtml
- http://www.read.xwpxi.com/Article/1125015.shtml
- http://www.read.xwpxi.com/Article/296286.shtml
- http://www.read.xwpxi.com/Article/72850.shtml
- http://www.read.xwpxi.com/Article/3766934.shtml
- http://www.read.xwpxi.com/Article/4748449.shtml
- http://www.read.xwpxi.com/Article/1253983.shtml
- http://www.read.xwpxi.com/Article/4150.shtml
- http://www.read.xwpxi.com/Article/0871222.shtml
- http://www.read.xwpxi.com/Article/326281.shtml
- http://www.read.xwpxi.com/Article/9968805.shtml
- http://www.read.xwpxi.com/Article/964539.shtml
- http://www.read.xwpxi.com/Article/8148170.shtml
- http://www.read.xwpxi.com/Article/1369395.shtml
- http://www.read.xwpxi.com/Article/9306859.shtml
- http://www.read.xwpxi.com/Article/11295.shtml
- http://www.read.xwpxi.com/Article/20455.shtml
- http://www.read.xwpxi.com/Article/94751.shtml
- http://www.read.xwpxi.com/Article/97256.shtml
- http://www.read.xwpxi.com/Article/1680426.shtml
- http://www.read.xwpxi.com/Article/4746770.shtml
- http://www.read.xwpxi.com/Article/540349.shtml
- http://www.read.xwpxi.com/Article/20551.shtml
- http://www.read.xwpxi.com/Article/98774.shtml
- http://www.read.xwpxi.com/Article/8574750.shtml
- http://www.read.xwpxi.com/Article/1929.shtml
- http://www.read.xwpxi.com/Article/9938605.shtml
- http://www.read.xwpxi.com/Article/89674.shtml
- http://www.read.xwpxi.com/Article/0101409.shtml
- http://www.read.xwpxi.com/Article/2218204.shtml
- http://www.read.xwpxi.com/Article/2185393.shtml
- http://www.read.xwpxi.com/Article/37662.shtml
- http://www.read.xwpxi.com/Article/8352810.shtml
- http://www.read.xwpxi.com/Article/01903.shtml
- http://www.read.xwpxi.com/Article/42779.shtml
- http://www.read.xwpxi.com/Article/8488.shtml
- http://www.read.xwpxi.com/Article/4620.shtml
- http://www.read.xwpxi.com/Article/0952.shtml
- http://www.read.xwpxi.com/Article/46107.shtml
- http://www.read.xwpxi.com/Article/7048619.shtml
- http://www.read.xwpxi.com/Article/6228.shtml
- http://www.read.xwpxi.com/Article/17510.shtml
- http://www.read.xwpxi.com/Article/650333.shtml
- http://www.read.xwpxi.com/Article/406944.shtml
- http://www.read.xwpxi.com/Article/8416.shtml
- http://www.read.xwpxi.com/Article/43692.shtml
- http://www.read.xwpxi.com/Article/7727272.shtml
- http://www.read.xwpxi.com/Article/0803661.shtml
- http://www.read.xwpxi.com/Article/96248.shtml
- http://www.read.xwpxi.com/Article/73445.shtml
- http://www.read.xwpxi.com/Article/857633.shtml
- http://www.read.xwpxi.com/Article/6937535.shtml
- http://www.read.xwpxi.com/Article/398265.shtml
- http://www.read.xwpxi.com/Article/10603.shtml
- http://www.read.xwpxi.com/Article/9561.shtml
- http://www.read.xwpxi.com/Article/312277.shtml
- http://www.read.xwpxi.com/Article/5455866.shtml
- http://www.read.xwpxi.com/Article/9846094.shtml
- http://www.read.xwpxi.com/Article/977592.shtml
- http://www.read.xwpxi.com/Article/304549.shtml
- http://www.read.xwpxi.com/Article/5102118.shtml
- http://www.read.xwpxi.com/Article/956261.shtml
- http://www.read.xwpxi.com/Article/50014.shtml
- http://www.read.xwpxi.com/Article/8151917.shtml
- http://www.read.xwpxi.com/Article/995379.shtml
- http://www.read.xwpxi.com/Article/416225.shtml
- http://www.read.xwpxi.com/Article/453971.shtml
- http://www.read.xwpxi.com/Article/6607.shtml
- http://www.read.xwpxi.com/Article/426054.shtml
- http://www.read.xwpxi.com/Article/8751.shtml
- http://www.read.xwpxi.com/Article/3922.shtml
- http://www.read.xwpxi.com/Article/065113.shtml
- http://www.read.xwpxi.com/Article/6808337.shtml
- http://www.read.xwpxi.com/Article/7448633.shtml
- http://www.read.xwpxi.com/Article/645803.shtml
- http://www.read.xwpxi.com/Article/07324.shtml
- http://www.read.xwpxi.com/Article/449148.shtml
- http://www.read.xwpxi.com/Article/4231.shtml
- http://www.read.xwpxi.com/Article/57501.shtml
- http://www.read.xwpxi.com/Article/84767.shtml
- http://www.read.xwpxi.com/Article/3509300.shtml
- http://www.read.xwpxi.com/Article/4060.shtml
- http://www.read.xwpxi.com/Article/6178468.shtml
- http://www.read.xwpxi.com/Article/5483346.shtml
- http://www.read.xwpxi.com/Article/3530261.shtml
- http://www.read.xwpxi.com/Article/6342251.shtml
- http://www.read.xwpxi.com/Article/4383322.shtml
- http://www.read.xwpxi.com/Article/923978.shtml
- http://www.read.xwpxi.com/Article/4404.shtml
- http://www.read.xwpxi.com/Article/62223.shtml
- http://www.read.xwpxi.com/Article/326383.shtml
- http://www.read.xwpxi.com/Article/3738440.shtml
- http://www.read.xwpxi.com/Article/883162.shtml
- http://www.read.xwpxi.com/Article/432068.shtml
- http://www.read.xwpxi.com/Article/3438.shtml
- http://www.read.xwpxi.com/Article/85824.shtml

## 项目结构

```
linkvault-core/
├── docs/                                 # 完整项目文档目录
│   ├── guide/                            # 用户指南：安装、配置、部署
│   ├── api/                              # API 参考文档与示例
│   ├── architecture/                     # 系统设计、数据模型与扩展点说明
│   └── development/                      # 开发者指南：调试、测试、主题定制
├── packages/                             # 多包管理目录（Monorepo 结构）
│   ├── core/                             # 核心逻辑：链接解析、去重、状态检查
│   ├── cli/                              # 命令行工具入口与命令实现
│   ├── web/                              # 前端界面：Vue 3 后台管理面板
│   ├── renderer/                         # 静态站点生成器：模板引擎与输出适配
│   └── shared/                           # 公共工具函数、类型定义与常量
├── data/                                 # 数据存储与迁移目录
│   ├── migrations/                       # 数据库结构变更脚本（SQLite）
│   ├── seeds/                            # 初始示例数据与测试链接集
│   └── backups/                          # 自动备份与恢复点存储位置
├── tests/                                # 单元测试与集成测试套件
│   ├── unit/                             # 各模块独立测试用例
│   ├── integration/                      # 端到端流程测试
│   └── fixtures/                         # 测试用静态资源与模拟数据
├── scripts/                              # 运维与辅助脚本
│   ├── health-check.sh                   # 链接健康度手动触发脚本
│   ├── export-csv.js                     # 导出资源列表为 CSV 格式
│   └── import-legacy.js                  # 旧版数据格式迁移工具
├── config/                               # 环境配置文件目录
│   ├── default.yaml                      # 基础配置（开发环境）
│   ├── production.yaml                   # 生产环境覆盖配置
│   └── custom/                           # 用户自定义配置片段（可覆盖）
├── dist/                                 # 构建输出目录（静态站点生成结果）
├── logs/                                 # 运行日志存储（按日期轮转）
├── .github/                              # GitHub 社区模板与 CI 流水线定义
│   ├── workflows/                        # GitHub Actions 持续集成配置
│   └── ISSUE_TEMPLATE/                   # 问题与功能请求模板
├── package.json                          # 项目依赖与脚本定义
├── tsconfig.json                         # TypeScript 编译配置
├── vitest.config.ts                      # 单元测试运行器配置
├── eslint.config.js                      # 代码风格检查规则
└── README.md                             # 本文件
```

## 贡献指南

1. 阅读项目行为准则与贡献者许可协议，确认接受相关条款。所有贡献者需签署开发者原创声明，确保提交内容不侵犯第三方权益。

2. 从 Issue 列表中选择标记为 `good-first-issue` 或 `help-wanted` 的任务，或在 Discussion 中提出新功能建议并等待维护者反馈。建议先沟通再动手，避免重复劳动。

3. Fork 项目仓库并创建特性分支，分支命名遵循 `feature/功能简述` 或 `fix/问题简述` 格式。提交代码前运行 `npm run lint` 与 `npm run test` 确保质量检查通过。

4. 提交 Pull Request 时需填写完整模板，包含变更摘要、测试覆盖说明以及关联 Issue 编号。PR 描述中需明确指出是否包含破坏性变更。

5. 维护者将在 5 个工作日内进行代码审查，提出修改意见或合并请求。合并后代码将自动触发 CI 构建与预览环境部署，最终随下一个版本一同发布。

## 常见问题

**Q1：导入大量链接时性能如何？是否有数量上限？**

单次批量导入建议不超过 5000 条记录，此时系统可在 30 秒内完成去重与校验。总记录数受限于 SQLite 数据库的存储上限，实际测试中 50 万条链接仍可保持正常查询响应（约 200ms 以内）。如需更高并发或更大数据量，可考虑将存储引擎切换为 PostgreSQL（官方提供迁移指南）。

**Q2：链接状态检查会对外部站点造成压力吗？**

系统默认采用渐进式探测策略，每个目标站点的请求间隔至少为 5 秒，且并发请求数限制为 3 个。同时支持用户配置 `User-Agent` 与请求超时时间（默认 10 秒），避免对小型或个人站点造成意外流量冲击。检查结果仅用于内部标记，不会对外公开或缓存页面内容。

**Q3：如何将现有书签或浏览器收藏夹导入 LinkVault？**

官方提供 `scripts/import-from-html.js` 工具，可直接解析 Chrome / Firefox 导出的书签 HTML 文件，自动提取标题与 URL，并保留文件夹名称作为标签。同时支持 Netscape 格式的通用书签文件导入。执行命令为 `npm run import:bookmarks -- --file ./bookmarks.html`。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
