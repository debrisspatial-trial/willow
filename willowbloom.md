# WebLink Hub

WebLink Hub 是一个面向技术研究者和信息分析人员的外链资源归集与结构化导航系统。该项目定位于将分散于互联网各处的优质技术文章、行业报告、案例分析与数据快讯进行统一收录、分类索引与版本化归档，解决个人收藏夹杂乱、链接失效、检索困难等长期痛点。通过轻量化的元数据标记与全文快照机制，WebLink Hub 帮助用户快速建立可追溯、可分享、可审计的外部知识参考库，适用于学术文献追踪、竞品动态监测、技术方案选型评估等多种严肃信息工作场景。

## 功能概览

批量链接导入与去重校验 支持从文本文件、浏览器书签导出或剪贴板批量导入原始 URL，自动识别重复条目并生成导入报告。

智能分类与标签体系 基于 URL 路径、来源域名、内容关键词等特征，自动建议分类标签；用户可自定义多级目录与标签组合。

全文快照与元数据抽取 对收录链接自动抓取页面标题、发布时间、作者、核心摘要等元数据，并保存网页快照以抵抗链接失效。

全文检索与高级筛选 提供基于标题、正文、标签、时间范围、来源域名的多条件组合检索，搜索结果支持按相关度、时间、阅读量排序。

定期健康检查与失效告警 周期性检测已收录链接的可访问性，自动标记失效链接并生成告警报告，支持一键导出失效清单。

数据导入导出与开放 API 支持 JSON、CSV、Markdown 表格等多种格式的批量导入导出；提供 RESTful API 接口，便于与其他知识管理工具集成。

协作评论与批注 支持对单条链接添加内部批注、问题标记和协作评论，适用于团队共享知识库的审核与讨论流程。

## 应用场景

技术方案选型评估 架构师或技术负责人收集多个候选中间件、框架或云服务的官方文档、性能测评与社区讨论链接，通过 WebLink Hub 统一存储并添加对比批注，形成结构化的技术决策参考材料。

行业竞品动态监测 产品经理与市场分析师定期整理竞品发布公告、版本更新日志、用户评价及第三方评测报告，利用健康检查功能监控链接可用性，确保长期追踪数据的完整性。

学术文献与研究报告整理 研究人员批量导入论文预印本、数据开源仓库、实验记录和同行评审评论等外部链接，分类标记研究主题与阶段，通过快照功能保留不同时间点的引用证据链。

技术培训与新人入职指引 团队维护一套标准化的内部技术栈学习资源索引，包括必读博客、官方教程、最佳实践案例与常见问题讨论帖，新成员可通过此导航快速进入学习路径。

事件复盘与故障归档 运维工程师将事故处理过程中的外部参考文档、临时修复方案链接、厂商公告等归集至特定事件目录，便于事后复盘时回溯完整信息上下文。

## 快速开始

以下步骤帮助您在本地环境中快速启动 WebLink Hub 服务。

```bash
# 步骤 1: 克隆代码仓库
git clone https://github.com/weblink-hub/weblink-hub.git
cd weblink-hub

# 步骤 2: 安装项目依赖
npm install

# 步骤 3: 启动开发服务器
npm run dev
```

服务启动后，通过浏览器访问 http://localhost:3000 即可进入 WebLink Hub 主界面。首次启动将自动创建 SQLite 数据库文件并生成默认管理员账户，默认账户信息请查阅 `.env.example` 文件中的初始化配置说明。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | >= 18.0.0 | 项目运行时环境，推荐使用 LTS 版本 |
| npm | >= 9.0.0 | 包管理器，用于安装项目依赖 |
| SQLite3 | 系统自带或手动安装 | 默认数据库引擎，无需额外配置 |
| Python 3.11+ （可选） | >= 3.11 | 用于执行部分元数据抽取辅助脚本 |
| Chromium 内核浏览器 （可选） | 最新稳定版 | 用于高质量网页快照渲染，若缺失则降级为静态抓取 |
| 系统内存 | >= 512 MB | 最低运行内存，推荐 2 GB 以上以获得良好性能 |
| 磁盘可用空间 | >= 1 GB | 用于存储 SQLite 数据库与网页快照文件，实际需求随链接数量增长 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户入门 | /docs/guide/getting-started.md | 如何安装、配置与首次启动？如何导入第一批链接？ |
| 功能使用 | /docs/guide/features.md | 标签系统如何工作？快照抓取策略是什么？如何设置健康检查频率？ |
| API 参考 | /docs/api/endpoints.md | 有哪些可用的 REST API 接口？请求与响应格式如何？ |
| 运维管理 | /docs/administration/deployment.md | 如何部署到生产环境？数据库备份与恢复流程是什么？性能调优参数有哪些？ |
| 贡献规范 | /docs/contributing/coding-standards.md | 代码风格要求是什么？提交信息格式规范？如何新增一个抓取解析器？ |

## 资源列表

- http://www.read.xwpxi.com/Article/9373339.shtml
- http://www.read.xwpxi.com/Article/9089157.shtml
- http://www.read.xwpxi.com/Article/74316.shtml
- http://www.read.xwpxi.com/Article/5658912.shtml
- http://www.read.xwpxi.com/Article/9440339.shtml
- http://www.read.xwpxi.com/Article/492067.shtml
- http://www.read.xwpxi.com/Article/38227.shtml
- http://www.read.xwpxi.com/Article/7597.shtml
- http://www.read.xwpxi.com/Article/2115.shtml
- http://www.read.xwpxi.com/Article/63770.shtml
- http://www.read.xwpxi.com/Article/2024.shtml
- http://www.read.xwpxi.com/Article/3490834.shtml
- http://www.read.xwpxi.com/Article/6588829.shtml
- http://www.read.xwpxi.com/Article/6901.shtml
- http://www.read.xwpxi.com/Article/7233142.shtml
- http://www.read.xwpxi.com/Article/79043.shtml
- http://www.read.xwpxi.com/Article/55893.shtml
- http://www.read.xwpxi.com/Article/71235.shtml
- http://www.read.xwpxi.com/Article/915711.shtml
- http://www.read.xwpxi.com/Article/6755286.shtml
- http://www.read.xwpxi.com/Article/2655.shtml
- http://www.read.xwpxi.com/Article/7201951.shtml
- http://www.read.xwpxi.com/Article/42905.shtml
- http://www.read.xwpxi.com/Article/6455565.shtml
- http://www.read.xwpxi.com/Article/3342.shtml
- http://www.read.xwpxi.com/Article/638552.shtml
- http://www.read.xwpxi.com/Article/4214380.shtml
- http://www.read.xwpxi.com/Article/425391.shtml
- http://www.read.xwpxi.com/Article/917493.shtml
- http://www.read.xwpxi.com/Article/8643.shtml
- http://www.read.xwpxi.com/Article/5537829.shtml
- http://www.read.xwpxi.com/Article/72567.shtml
- http://www.read.xwpxi.com/Article/73643.shtml
- http://www.read.xwpxi.com/Article/40364.shtml
- http://www.read.xwpxi.com/Article/17036.shtml
- http://www.read.xwpxi.com/Article/13743.shtml
- http://www.read.xwpxi.com/Article/8188343.shtml
- http://www.read.xwpxi.com/Article/29362.shtml
- http://www.read.xwpxi.com/Article/12366.shtml
- http://www.read.xwpxi.com/Article/954721.shtml
- http://www.read.xwpxi.com/Article/415080.shtml
- http://www.read.xwpxi.com/Article/7244.shtml
- http://www.read.xwpxi.com/Article/5146.shtml
- http://www.read.xwpxi.com/Article/545563.shtml
- http://www.read.xwpxi.com/Article/6070.shtml
- http://www.read.xwpxi.com/Article/808527.shtml
- http://www.read.xwpxi.com/Article/085153.shtml
- http://www.read.xwpxi.com/Article/0519678.shtml
- http://www.read.xwpxi.com/Article/80039.shtml
- http://www.read.xwpxi.com/Article/8378114.shtml
- http://www.read.xwpxi.com/Article/655490.shtml
- http://www.read.xwpxi.com/Article/8069.shtml
- http://www.read.xwpxi.com/Article/2693.shtml
- http://www.read.xwpxi.com/Article/9187.shtml
- http://www.read.xwpxi.com/Article/010603.shtml
- http://www.read.xwpxi.com/Article/85677.shtml
- http://www.read.xwpxi.com/Article/19408.shtml
- http://www.read.xwpxi.com/Article/715458.shtml
- http://www.read.xwpxi.com/Article/256730.shtml
- http://www.read.xwpxi.com/Article/51384.shtml
- http://www.read.xwpxi.com/Article/7075712.shtml
- http://www.read.xwpxi.com/Article/194519.shtml
- http://www.read.xwpxi.com/Article/751919.shtml
- http://www.read.xwpxi.com/Article/86003.shtml
- http://www.read.xwpxi.com/Article/38340.shtml
- http://www.read.xwpxi.com/Article/433109.shtml
- http://www.read.xwpxi.com/Article/1575990.shtml
- http://www.read.xwpxi.com/Article/2043428.shtml
- http://www.read.xwpxi.com/Article/409304.shtml
- http://www.read.xwpxi.com/Article/88080.shtml
- http://www.read.xwpxi.com/Article/7943984.shtml
- http://www.read.xwpxi.com/Article/065059.shtml
- http://www.read.xwpxi.com/Article/06710.shtml
- http://www.read.xwpxi.com/Article/937856.shtml
- http://www.read.xwpxi.com/Article/72882.shtml
- http://www.read.xwpxi.com/Article/246837.shtml
- http://www.read.xwpxi.com/Article/6905.shtml
- http://www.read.xwpxi.com/Article/058966.shtml
- http://www.read.xwpxi.com/Article/7212645.shtml
- http://www.read.xwpxi.com/Article/643041.shtml
- http://www.read.xwpxi.com/Article/74929.shtml
- http://www.read.xwpxi.com/Article/1162596.shtml
- http://www.read.xwpxi.com/Article/8256.shtml
- http://www.read.xwpxi.com/Article/1809814.shtml
- http://www.read.xwpxi.com/Article/4048.shtml
- http://www.read.xwpxi.com/Article/030013.shtml
- http://www.read.xwpxi.com/Article/7514235.shtml
- http://www.read.xwpxi.com/Article/603527.shtml
- http://www.read.xwpxi.com/Article/10121.shtml
- http://www.read.xwpxi.com/Article/57990.shtml
- http://www.read.xwpxi.com/Article/4096198.shtml
- http://www.read.xwpxi.com/Article/81542.shtml
- http://www.read.xwpxi.com/Article/15304.shtml
- http://www.read.xwpxi.com/Article/60913.shtml
- http://www.read.xwpxi.com/Article/85395.shtml
- http://www.read.xwpxi.com/Article/36470.shtml
- http://www.read.xwpxi.com/Article/479592.shtml
- http://www.read.xwpxi.com/Article/36854.shtml
- http://www.read.xwpxi.com/Article/4461.shtml
- http://www.read.xwpxi.com/Article/36449.shtml
- http://www.read.xwpxi.com/Article/0560.shtml
- http://www.read.xwpxi.com/Article/0203717.shtml
- http://www.read.xwpxi.com/Article/81617.shtml
- http://www.read.xwpxi.com/Article/2747613.shtml
- http://www.read.xwpxi.com/Article/02747.shtml
- http://www.read.xwpxi.com/Article/618840.shtml
- http://www.read.xwpxi.com/Article/296862.shtml
- http://www.read.xwpxi.com/Article/049496.shtml
- http://www.read.xwpxi.com/Article/9108.shtml
- http://www.read.xwpxi.com/Article/139004.shtml
- http://www.read.xwpxi.com/Article/17591.shtml
- http://www.read.xwpxi.com/Article/3807667.shtml
- http://www.read.xwpxi.com/Article/262381.shtml
- http://www.read.xwpxi.com/Article/8952051.shtml
- http://www.read.xwpxi.com/Article/3848.shtml
- http://www.read.xwpxi.com/Article/792261.shtml
- http://www.read.xwpxi.com/Article/300161.shtml
- http://www.read.xwpxi.com/Article/91129.shtml
- http://www.read.xwpxi.com/Article/0887.shtml
- http://www.read.xwpxi.com/Article/20854.shtml
- http://www.read.xwpxi.com/Article/636653.shtml
- http://www.read.xwpxi.com/Article/284325.shtml
- http://www.read.xwpxi.com/Article/40689.shtml
- http://www.read.xwpxi.com/Article/798171.shtml
- http://www.read.xwpxi.com/Article/2829.shtml
- http://www.read.xwpxi.com/Article/880556.shtml
- http://www.read.xwpxi.com/Article/62226.shtml
- http://www.read.xwpxi.com/Article/30205.shtml
- http://www.read.xwpxi.com/Article/492828.shtml
- http://www.read.xwpxi.com/Article/278870.shtml
- http://www.read.xwpxi.com/Article/3171565.shtml
- http://www.read.xwpxi.com/Article/34924.shtml
- http://www.read.xwpxi.com/Article/1769.shtml
- http://www.read.xwpxi.com/Article/71701.shtml
- http://www.read.xwpxi.com/Article/1999.shtml
- http://www.read.xwpxi.com/Article/0955.shtml
- http://www.read.xwpxi.com/Article/174266.shtml
- http://www.read.xwpxi.com/Article/5685118.shtml
- http://www.read.xwpxi.com/Article/2290.shtml
- http://www.read.xwpxi.com/Article/208270.shtml
- http://www.read.xwpxi.com/Article/84070.shtml
- http://www.read.xwpxi.com/Article/2435384.shtml
- http://www.read.xwpxi.com/Article/0005.shtml
- http://www.read.xwpxi.com/Article/7620.shtml
- http://www.read.xwpxi.com/Article/96547.shtml
- http://www.read.xwpxi.com/Article/1520313.shtml
- http://www.read.xwpxi.com/Article/2400.shtml
- http://www.read.xwpxi.com/Article/6771.shtml
- http://www.read.xwpxi.com/Article/604348.shtml
- http://www.read.xwpxi.com/Article/27540.shtml
- http://www.read.xwpxi.com/Article/5163295.shtml
- http://www.read.xwpxi.com/Article/0805.shtml
- http://www.read.xwpxi.com/Article/17485.shtml
- http://www.read.xwpxi.com/Article/50304.shtml
- http://www.read.xwpxi.com/Article/740469.shtml
- http://www.read.xwpxi.com/Article/1466246.shtml
- http://www.read.xwpxi.com/Article/499299.shtml
- http://www.read.xwpxi.com/Article/239695.shtml
- http://www.read.xwpxi.com/Article/3116790.shtml
- http://www.read.xwpxi.com/Article/305287.shtml
- http://www.read.xwpxi.com/Article/979480.shtml
- http://www.read.xwpxi.com/Article/3918.shtml
- http://www.read.xwpxi.com/Article/8819436.shtml
- http://www.read.xwpxi.com/Article/354533.shtml
- http://www.read.xwpxi.com/Article/26916.shtml
- http://www.read.xwpxi.com/Article/0904.shtml
- http://www.read.xwpxi.com/Article/43174.shtml
- http://www.read.xwpxi.com/Article/9636842.shtml
- http://www.read.xwpxi.com/Article/53996.shtml
- http://www.read.xwpxi.com/Article/8128649.shtml
- http://www.read.xwpxi.com/Article/35093.shtml
- http://www.read.xwpxi.com/Article/6093.shtml
- http://www.read.xwpxi.com/Article/45322.shtml
- http://www.read.xwpxi.com/Article/596261.shtml
- http://www.read.xwpxi.com/Article/5486052.shtml
- http://www.read.xwpxi.com/Article/0451.shtml
- http://www.read.xwpxi.com/Article/344781.shtml
- http://www.read.xwpxi.com/Article/221402.shtml
- http://www.read.xwpxi.com/Article/4735.shtml
- http://www.read.xwpxi.com/Article/33022.shtml
- http://www.read.xwpxi.com/Article/87879.shtml
- http://www.read.xwpxi.com/Article/741567.shtml
- http://www.read.xwpxi.com/Article/762889.shtml
- http://www.read.xwpxi.com/Article/09986.shtml
- http://www.read.xwpxi.com/Article/9943160.shtml
- http://www.read.xwpxi.com/Article/38370.shtml
- http://www.read.xwpxi.com/Article/0147.shtml
- http://www.read.xwpxi.com/Article/9305552.shtml
- http://www.read.xwpxi.com/Article/215299.shtml
- http://www.read.xwpxi.com/Article/4486.shtml
- http://www.read.xwpxi.com/Article/11200.shtml
- http://www.read.xwpxi.com/Article/3913258.shtml
- http://www.read.xwpxi.com/Article/538471.shtml
- http://www.read.xwpxi.com/Article/856738.shtml
- http://www.read.xwpxi.com/Article/777897.shtml
- http://www.read.xwpxi.com/Article/2541.shtml
- http://www.read.xwpxi.com/Article/57632.shtml
- http://www.read.xwpxi.com/Article/04250.shtml
- http://www.read.xwpxi.com/Article/37116.shtml
- http://www.read.xwpxi.com/Article/2884.shtml
- http://www.read.xwpxi.com/Article/9784839.shtml
- http://www.read.xwpxi.com/Article/0726421.shtml
- http://www.read.xwpxi.com/Article/3595025.shtml
- http://www.read.xwpxi.com/Article/95223.shtml
- http://www.read.xwpxi.com/Article/7745092.shtml
- http://www.read.xwpxi.com/Article/78775.shtml
- http://www.read.xwpxi.com/Article/70909.shtml
- http://www.read.xwpxi.com/Article/362730.shtml
- http://www.read.xwpxi.com/Article/1303.shtml
- http://www.read.xwpxi.com/Article/3287234.shtml
- http://www.read.xwpxi.com/Article/098812.shtml
- http://www.read.xwpxi.com/Article/784485.shtml
- http://www.read.xwpxi.com/Article/85501.shtml
- http://www.read.xwpxi.com/Article/4428906.shtml
- http://www.read.xwpxi.com/Article/2397741.shtml
- http://www.read.xwpxi.com/Article/1542.shtml
- http://www.read.xwpxi.com/Article/270805.shtml
- http://www.read.xwpxi.com/Article/73410.shtml
- http://www.read.xwpxi.com/Article/798323.shtml
- http://www.read.xwpxi.com/Article/111236.shtml
- http://www.read.xwpxi.com/Article/8126601.shtml
- http://www.read.xwpxi.com/Article/8634.shtml
- http://www.read.xwpxi.com/Article/876162.shtml
- http://www.read.xwpxi.com/Article/2808568.shtml
- http://www.read.xwpxi.com/Article/6763854.shtml
- http://www.read.xwpxi.com/Article/4211842.shtml
- http://www.read.xwpxi.com/Article/607271.shtml
- http://www.read.xwpxi.com/Article/32021.shtml
- http://www.read.xwpxi.com/Article/007811.shtml
- http://www.read.xwpxi.com/Article/8921516.shtml
- http://www.read.xwpxi.com/Article/18539.shtml
- http://www.read.xwpxi.com/Article/5910562.shtml
- http://www.read.xwpxi.com/Article/6472.shtml
- http://www.read.xwpxi.com/Article/716896.shtml
- http://www.read.xwpxi.com/Article/0944585.shtml
- http://www.read.xwpxi.com/Article/0860.shtml
- http://www.read.xwpxi.com/Article/3176.shtml
- http://www.read.xwpxi.com/Article/2194021.shtml
- http://www.read.xwpxi.com/Article/7164.shtml
- http://www.read.xwpxi.com/Article/87619.shtml
- http://www.read.xwpxi.com/Article/44290.shtml
- http://www.read.xwpxi.com/Article/02455.shtml
- http://www.read.xwpxi.com/Article/30395.shtml
- http://www.read.xwpxi.com/Article/3380527.shtml
- http://www.read.xwpxi.com/Article/53146.shtml
- http://www.read.xwpxi.com/Article/46101.shtml
- http://www.read.xwpxi.com/Article/333359.shtml
- http://www.read.xwpxi.com/Article/4388337.shtml
- http://www.read.xwpxi.com/Article/8818.shtml
- http://www.read.xwpxi.com/Article/337699.shtml

## 项目结构

```
weblink-hub/
├── apps/
│   ├── web/                           # 主 Web 应用（Next.js 14）
│   │   ├── app/                       # App Router 页面路由
│   │   ├── components/                # 可复用 UI 组件（分类面板、链接卡片、搜索栏）
│   │   └── api/                       # API 路由（链接管理、快照抓取、健康检查）
│   └── worker/                        # 后台工作进程（独立服务）
│       ├── crawler/                   # 网页抓取与快照生成模块
│       ├── scheduler/                 # 健康检查定时任务调度器
│       └── queue/                     # 基于 BullMQ 的任务队列管理
├── packages/
│   ├── core/                          # 核心数据模型与业务逻辑（TypeScript）
│   │   ├── models/                    # SQLite 数据表映射（链接、标签、快照、批注）
│   │   ├── services/                  # 链接解析、分类建议、去重校验服务
│   │   └── utils/                     # 通用工具函数（URL 标准化、时间处理）
│   ├── parser/                        # 多格式导入解析器（HTML 书签、CSV、JSON）
│   └── api-client/                    # 对外 REST API 客户端 SDK
├── configs/
│   ├── eslint/                        # ESLint 共享配置
│   ├── typescript/                    # TypeScript 路径映射与编译选项
│   └── jest/                          # 单元测试预设配置
├── data/
│   ├── database/                      # SQLite 数据库文件（默认 weblink.db）
│   ├── snapshots/                     # 网页快照存储目录（按域名分文件夹）
│   └── imports/                       # 导入任务临时文件暂存区
├── scripts/
│   ├── init-db.ts                     # 初始化数据库表结构与默认标签
│   ├── batch-import.ts               # 批量导入命令行工具
│   └── health-check.ts               # 手动触发健康检查脚本
├── tests/
│   ├── unit/                          # 单元测试（核心服务、解析器）
│   └── integration/                   # 集成测试（API 端点、数据库操作）
├── docs/                              # 完整文档（见文档导航章节）
├── .env.example                       # 环境变量配置模板
├── docker-compose.yml                 # 容器化部署编排配置
├── Dockerfile                         # 生产环境镜像构建文件
├── package.json                       # 项目依赖与脚本定义
├── tsconfig.json                      # TypeScript 根配置
└── README.md                          # 项目说明文件（当前文档）
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于代码提交、文档改进、问题报告与功能建议。请遵循以下步骤参与项目：

1. 查阅问题列表与项目看板 访问 GitHub Issues 页面查看已标记的 good first issue 或 help wanted 标签任务，或在 Discussions 板块提出新功能设想以避免重复工作。

2. Fork 仓库并创建功能分支 将主仓库 Fork 至个人账号，基于 main 分支创建描述性名称的新分支（如 feat/add-rss-export 或 fix/snapshot-timeout）。

3. 遵循代码规范与测试要求 提交前运行 npm run lint 与 npm run test 确保代码风格一致且所有测试通过。新增功能需附带对应的单元测试或集成测试用例。

4. 提交变更并签署开发者原创声明 提交信息格式遵循 Conventional Commits 规范（类型(范围): 主题）。提交时需签署 DCO（Developer Certificate of Origin），表明您有权贡献且同意开源许可条款。

5. 发起 Pull Request 并参与评审 推送到个人 Fork 仓库后，向主仓库的 main 分支发起 Pull Request。描述中请清晰说明变更内容、关联问题编号以及测试覆盖情况。评审通过后由项目维护者合并。

## 常见问题

Q: 导入大量链接时页面响应缓慢或超时怎么办？
A: 批量导入操作采用后台任务队列处理，建议一次导入不超过 500 条链接。若需导入更大批次，可使用命令行工具 scripts/batch-import.ts 并配合 --chunk-size 参数分块执行。同时确保系统内存充足，SQLite 数据库文件所在磁盘有足够剩余空间。

Q: 网页快照抓取失败或内容不完整如何处理？
A: 快照抓取失败通常由目标网站的反爬机制、网络超时或动态内容渲染不完整导致。可尝试以下措施：调整 .env 中的 CRAWLER_TIMEOUT 和 USER_AGENT 配置；安装 Chromium 浏览器并启用 HEADLESS_BROWSER 选项以支持 JavaScript 渲染；对于特定域名可在 parser 配置中添加自定义重试规则。失败条目将在健康检查报告中标记，支持手动重新抓取。

Q: 如何将 WebLink Hub 迁移到另一台服务器？
A: 迁移涉及数据库文件与快照存储目录两大部分。首先停止服务进程，复制 data/database/ 下的 .db 文件以及 data/snapshots/ 目录至新服务器相同相对路径。确保新服务器的 Node.js 版本与环境变量（如 DATABASE_PATH、SNAPSHOT_STORAGE）与原服务器一致。启动服务后执行 npm run db:migrate 检查并升级数据库结构至最新版本。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
