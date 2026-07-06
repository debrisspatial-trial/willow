# ReadX Reference Aggregator

ReadX Reference Aggregator 是一个面向技术文档工程师、学术研究人员和内容创作者的轻量化外链资源归集系统。该项目专注于对分散在多个内容源中的深度文章进行结构化整理、元数据提取和快速检索，帮助用户以最小成本建立个人或团队的知识索引层。

系统以静态站点形态交付，无需数据库，仅依赖文件系统与 HTTP 缓存，即可完成对特定域名下批量文章链接的抓取、分类与展示。项目内置了分批导入机制，当前批次包含 250 个来自 read.xwpxi.com 域名的深度文章链接，后续批次可平滑追加。目标用户为需要长期跟踪特定源站内容更新的技术运营者、数据标注团队以及进行文献回溯的学术辅助人员。

## 功能概览

批量链接导入器 支持按批次导入包含数百个文章 URL 的清单文件，自动校验链接可访问性并过滤重复项。

元数据自动抽取 对每个文章链接发起 HEAD 与 GET 请求，从响应头与 HTML 结构中的 meta 标签提取标题、发布时间、内容类型及字符编码。

分类标签生成引擎 基于 URL 路径中的数字段规则与文章标题关键词，通过正则表达式和简单贝叶斯分类器为每篇文章分配初级标签。

静态站点生成管线 将导入的文章元数据渲染为按标签、日期、文章编号三种维度索引的 HTML 页面，所有页面均无需动态服务端支持。

全文检索占位系统 集成基于 Lunr.js 或 Minisearch 的客户端侧搜索能力，允许用户在本地索引范围内对文章标题和摘要进行关键词匹配。

增量更新工作流 支持通过差异比较导入新批次链接，仅处理新增或状态变更的 URL，避免全量重建。

导出接口 提供 JSON、CSV 和 Markdown 表格三种格式的元数据导出，便于与其他文献管理工具或数据分析流水线对接。

## 应用场景

技术文档团队的历史文章回溯
当团队需要整理某个技术博客或新闻源站过去数年发布的数千篇文章时，可使用该项目的分批导入机制，将 URL 列表逐批注入，自动抽取元数据并生成索引页面，供团队成员按时间线或标签浏览。

学术研究中的参考文献补充
研究人员在收集某专题文献时，可将从各类推荐系统或订阅源获得的文章链接集中导入，项目生成的静态站点可作为该专题的本地镜像资料库，方便随时调阅和标注。

内容运营的竞品动态监控
内容运营人员将竞品官网的文章列表页链接整理成批次，导入后系统可定期执行增量更新，通过比对新增链接及时发现竞品的内容发布节奏与选题方向。

个人知识库的链接归档
个人开发者或写作者可将长期积累的“待读”或“已读”书签链接导入系统，利用自动生成的分类标签和检索功能，将浏览器收藏夹转化为可检索、可分享的本地知识网页。

## 快速开始

以下命令演示了从克隆仓库到启动开发服务器的完整流程，适用于 Linux 与 macOS 环境。Windows 用户建议使用 WSL2 或 Git Bash 执行。

```bash
git clone https://github.com/readx-project/readx-aggregator.git
cd readx-aggregator

# 安装项目依赖
npm install

# 执行链接导入与站点构建
npm run import -- --batch=1 --source=./data/urls_batch_1.txt
npm run build

# 启动本地预览服务
npm run serve
```

访问控制台输出的本地地址（默认 http://localhost:8080）即可查看生成的索引站点。若需导入当前批次，请将提供的 URL 列表保存为 data/urls_batch_1.txt 后执行导入命令。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 16.20.0 或更高 | 运行时环境，建议使用 LTS 版本 |
| npm | 8.0.0 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.25.0 或更高 | 版本控制工具，用于克隆仓库 |
| 网络访问 | 出站 80/443 端口开放 | 用于对导入的 URL 发起 HTTP 请求以抽取元数据 |
| 文件系统权限 | 读写权限 | 项目需要在工作目录下创建 cache/ 和 dist/ 目录 |
| 内存 | 最低 512MB，推荐 1GB | 处理 250 个链接时峰值内存占用约 300MB |
| 磁盘空间 | 200MB 可用空间 | 用于存储缓存元数据及生成的静态页面文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide/ | 如何安装、配置批次文件、执行导入与构建、部署生成的站点 |
| 开发者指南 | /docs/developer-guide/ | 项目模块划分、核心类与函数说明、新增解析器或分类器的扩展方法 |
| 批次管理 | /docs/batch-management/ | 批次文件的格式规范、校验规则、如何续接或合并多个批次的数据 |
| 部署运维 | /docs/deployment/ | 生产环境构建优化、Nginx 或 Apache 的静态托管配置、缓存策略 |
| API 参考 | /docs/api-reference/ | 导出数据结构的 JSON Schema、CSV 列定义、命令行工具的完整参数列表 |
| 常见工作流 | /docs/workflows/ | 结合 cron 定时任务实现自动更新、与 Notion/Airtable 的集成示例 |

## 资源列表

- http://www.read.xwpxi.com/Article/625734.shtml
- http://www.read.xwpxi.com/Article/40038.shtml
- http://www.read.xwpxi.com/Article/726282.shtml
- http://www.read.xwpxi.com/Article/8457.shtml
- http://www.read.xwpxi.com/Article/42317.shtml
- http://www.read.xwpxi.com/Article/397358.shtml
- http://www.read.xwpxi.com/Article/2079678.shtml
- http://www.read.xwpxi.com/Article/908798.shtml
- http://www.read.xwpxi.com/Article/6235888.shtml
- http://www.read.xwpxi.com/Article/8252489.shtml
- http://www.read.xwpxi.com/Article/934508.shtml
- http://www.read.xwpxi.com/Article/43402.shtml
- http://www.read.xwpxi.com/Article/738679.shtml
- http://www.read.xwpxi.com/Article/7477.shtml
- http://www.read.xwpxi.com/Article/1360588.shtml
- http://www.read.xwpxi.com/Article/3539.shtml
- http://www.read.xwpxi.com/Article/97670.shtml
- http://www.read.xwpxi.com/Article/536086.shtml
- http://www.read.xwpxi.com/Article/4472106.shtml
- http://www.read.xwpxi.com/Article/4841.shtml
- http://www.read.xwpxi.com/Article/512096.shtml
- http://www.read.xwpxi.com/Article/97274.shtml
- http://www.read.xwpxi.com/Article/489542.shtml
- http://www.read.xwpxi.com/Article/02578.shtml
- http://www.read.xwpxi.com/Article/670699.shtml
- http://www.read.xwpxi.com/Article/364280.shtml
- http://www.read.xwpxi.com/Article/47856.shtml
- http://www.read.xwpxi.com/Article/751421.shtml
- http://www.read.xwpxi.com/Article/2205.shtml
- http://www.read.xwpxi.com/Article/0095615.shtml
- http://www.read.xwpxi.com/Article/8269274.shtml
- http://www.read.xwpxi.com/Article/43249.shtml
- http://www.read.xwpxi.com/Article/2183851.shtml
- http://www.read.xwpxi.com/Article/68961.shtml
- http://www.read.xwpxi.com/Article/83494.shtml
- http://www.read.xwpxi.com/Article/15545.shtml
- http://www.read.xwpxi.com/Article/2277538.shtml
- http://www.read.xwpxi.com/Article/5883990.shtml
- http://www.read.xwpxi.com/Article/979714.shtml
- http://www.read.xwpxi.com/Article/6427463.shtml
- http://www.read.xwpxi.com/Article/8016355.shtml
- http://www.read.xwpxi.com/Article/3824.shtml
- http://www.read.xwpxi.com/Article/4471.shtml
- http://www.read.xwpxi.com/Article/21399.shtml
- http://www.read.xwpxi.com/Article/4523834.shtml
- http://www.read.xwpxi.com/Article/9927.shtml
- http://www.read.xwpxi.com/Article/1433.shtml
- http://www.read.xwpxi.com/Article/048506.shtml
- http://www.read.xwpxi.com/Article/3246994.shtml
- http://www.read.xwpxi.com/Article/0685752.shtml
- http://www.read.xwpxi.com/Article/67114.shtml
- http://www.read.xwpxi.com/Article/3485388.shtml
- http://www.read.xwpxi.com/Article/917971.shtml
- http://www.read.xwpxi.com/Article/8006731.shtml
- http://www.read.xwpxi.com/Article/0949543.shtml
- http://www.read.xwpxi.com/Article/220366.shtml
- http://www.read.xwpxi.com/Article/0448199.shtml
- http://www.read.xwpxi.com/Article/627611.shtml
- http://www.read.xwpxi.com/Article/8524.shtml
- http://www.read.xwpxi.com/Article/8726.shtml
- http://www.read.xwpxi.com/Article/92159.shtml
- http://www.read.xwpxi.com/Article/6837669.shtml
- http://www.read.xwpxi.com/Article/048349.shtml
- http://www.read.xwpxi.com/Article/18873.shtml
- http://www.read.xwpxi.com/Article/282797.shtml
- http://www.read.xwpxi.com/Article/9009739.shtml
- http://www.read.xwpxi.com/Article/6850.shtml
- http://www.read.xwpxi.com/Article/748202.shtml
- http://www.read.xwpxi.com/Article/995866.shtml
- http://www.read.xwpxi.com/Article/84931.shtml
- http://www.read.xwpxi.com/Article/543983.shtml
- http://www.read.xwpxi.com/Article/83786.shtml
- http://www.read.xwpxi.com/Article/2977.shtml
- http://www.read.xwpxi.com/Article/957678.shtml
- http://www.read.xwpxi.com/Article/665083.shtml
- http://www.read.xwpxi.com/Article/88669.shtml
- http://www.read.xwpxi.com/Article/900482.shtml
- http://www.read.xwpxi.com/Article/3304.shtml
- http://www.read.xwpxi.com/Article/5161275.shtml
- http://www.read.xwpxi.com/Article/487024.shtml
- http://www.read.xwpxi.com/Article/3869473.shtml
- http://www.read.xwpxi.com/Article/95875.shtml
- http://www.read.xwpxi.com/Article/8117.shtml
- http://www.read.xwpxi.com/Article/4645.shtml
- http://www.read.xwpxi.com/Article/512088.shtml
- http://www.read.xwpxi.com/Article/95286.shtml
- http://www.read.xwpxi.com/Article/5323.shtml
- http://www.read.xwpxi.com/Article/97161.shtml
- http://www.read.xwpxi.com/Article/7636.shtml
- http://www.read.xwpxi.com/Article/93887.shtml
- http://www.read.xwpxi.com/Article/0393.shtml
- http://www.read.xwpxi.com/Article/5336862.shtml
- http://www.read.xwpxi.com/Article/851010.shtml
- http://www.read.xwpxi.com/Article/6807546.shtml
- http://www.read.xwpxi.com/Article/6522501.shtml
- http://www.read.xwpxi.com/Article/88956.shtml
- http://www.read.xwpxi.com/Article/3926935.shtml
- http://www.read.xwpxi.com/Article/4830113.shtml
- http://www.read.xwpxi.com/Article/92343.shtml
- http://www.read.xwpxi.com/Article/4417279.shtml
- http://www.read.xwpxi.com/Article/43559.shtml
- http://www.read.xwpxi.com/Article/349951.shtml
- http://www.read.xwpxi.com/Article/03411.shtml
- http://www.read.xwpxi.com/Article/2162583.shtml
- http://www.read.xwpxi.com/Article/1794.shtml
- http://www.read.xwpxi.com/Article/701027.shtml
- http://www.read.xwpxi.com/Article/390285.shtml
- http://www.read.xwpxi.com/Article/26610.shtml
- http://www.read.xwpxi.com/Article/672546.shtml
- http://www.read.xwpxi.com/Article/245209.shtml
- http://www.read.xwpxi.com/Article/03127.shtml
- http://www.read.xwpxi.com/Article/7256.shtml
- http://www.read.xwpxi.com/Article/33176.shtml
- http://www.read.xwpxi.com/Article/42318.shtml
- http://www.read.xwpxi.com/Article/01581.shtml
- http://www.read.xwpxi.com/Article/147780.shtml
- http://www.read.xwpxi.com/Article/20169.shtml
- http://www.read.xwpxi.com/Article/3586524.shtml
- http://www.read.xwpxi.com/Article/5616162.shtml
- http://www.read.xwpxi.com/Article/0120.shtml
- http://www.read.xwpxi.com/Article/6340874.shtml
- http://www.read.xwpxi.com/Article/735354.shtml
- http://www.read.xwpxi.com/Article/9835.shtml
- http://www.read.xwpxi.com/Article/522672.shtml
- http://www.read.xwpxi.com/Article/94059.shtml
- http://www.read.xwpxi.com/Article/120947.shtml
- http://www.read.xwpxi.com/Article/4721.shtml
- http://www.read.xwpxi.com/Article/5945.shtml
- http://www.read.xwpxi.com/Article/080470.shtml
- http://www.read.xwpxi.com/Article/38506.shtml
- http://www.read.xwpxi.com/Article/29288.shtml
- http://www.read.xwpxi.com/Article/2825.shtml
- http://www.read.xwpxi.com/Article/550286.shtml
- http://www.read.xwpxi.com/Article/3421.shtml
- http://www.read.xwpxi.com/Article/0600300.shtml
- http://www.read.xwpxi.com/Article/5172373.shtml
- http://www.read.xwpxi.com/Article/5686335.shtml
- http://www.read.xwpxi.com/Article/2774591.shtml
- http://www.read.xwpxi.com/Article/96328.shtml
- http://www.read.xwpxi.com/Article/3310.shtml
- http://www.read.xwpxi.com/Article/459036.shtml
- http://www.read.xwpxi.com/Article/036365.shtml
- http://www.read.xwpxi.com/Article/90095.shtml
- http://www.read.xwpxi.com/Article/1792247.shtml
- http://www.read.xwpxi.com/Article/407314.shtml
- http://www.read.xwpxi.com/Article/578659.shtml
- http://www.read.xwpxi.com/Article/0770160.shtml
- http://www.read.xwpxi.com/Article/20703.shtml
- http://www.read.xwpxi.com/Article/28290.shtml
- http://www.read.xwpxi.com/Article/5433123.shtml
- http://www.read.xwpxi.com/Article/0079542.shtml
- http://www.read.xwpxi.com/Article/9412.shtml
- http://www.read.xwpxi.com/Article/51600.shtml
- http://www.read.xwpxi.com/Article/2836997.shtml
- http://www.read.xwpxi.com/Article/3454269.shtml
- http://www.read.xwpxi.com/Article/94922.shtml
- http://www.read.xwpxi.com/Article/3459531.shtml
- http://www.read.xwpxi.com/Article/346367.shtml
- http://www.read.xwpxi.com/Article/9150152.shtml
- http://www.read.xwpxi.com/Article/1352.shtml
- http://www.read.xwpxi.com/Article/370603.shtml
- http://www.read.xwpxi.com/Article/71745.shtml
- http://www.read.xwpxi.com/Article/669200.shtml
- http://www.read.xwpxi.com/Article/175429.shtml
- http://www.read.xwpxi.com/Article/65150.shtml
- http://www.read.xwpxi.com/Article/1944.shtml
- http://www.read.xwpxi.com/Article/0667999.shtml
- http://www.read.xwpxi.com/Article/5030567.shtml
- http://www.read.xwpxi.com/Article/616538.shtml
- http://www.read.xwpxi.com/Article/6831848.shtml
- http://www.read.xwpxi.com/Article/55554.shtml
- http://www.read.xwpxi.com/Article/7289.shtml
- http://www.read.xwpxi.com/Article/8373913.shtml
- http://www.read.xwpxi.com/Article/42066.shtml
- http://www.read.xwpxi.com/Article/45102.shtml
- http://www.read.xwpxi.com/Article/4848627.shtml
- http://www.read.xwpxi.com/Article/087729.shtml
- http://www.read.xwpxi.com/Article/5568087.shtml
- http://www.read.xwpxi.com/Article/168302.shtml
- http://www.read.xwpxi.com/Article/27832.shtml
- http://www.read.xwpxi.com/Article/9439812.shtml
- http://www.read.xwpxi.com/Article/7996804.shtml
- http://www.read.xwpxi.com/Article/288399.shtml
- http://www.read.xwpxi.com/Article/19183.shtml
- http://www.read.xwpxi.com/Article/4576854.shtml
- http://www.read.xwpxi.com/Article/1259562.shtml
- http://www.read.xwpxi.com/Article/1732.shtml
- http://www.read.xwpxi.com/Article/10037.shtml
- http://www.read.xwpxi.com/Article/9458150.shtml
- http://www.read.xwpxi.com/Article/125935.shtml
- http://www.read.xwpxi.com/Article/3679.shtml
- http://www.read.xwpxi.com/Article/5479267.shtml
- http://www.read.xwpxi.com/Article/82443.shtml
- http://www.read.xwpxi.com/Article/12724.shtml
- http://www.read.xwpxi.com/Article/18704.shtml
- http://www.read.xwpxi.com/Article/7066.shtml
- http://www.read.xwpxi.com/Article/614765.shtml
- http://www.read.xwpxi.com/Article/6780136.shtml
- http://www.read.xwpxi.com/Article/5271704.shtml
- http://www.read.xwpxi.com/Article/2604.shtml
- http://www.read.xwpxi.com/Article/8620.shtml
- http://www.read.xwpxi.com/Article/7673.shtml
- http://www.read.xwpxi.com/Article/85164.shtml
- http://www.read.xwpxi.com/Article/5588.shtml
- http://www.read.xwpxi.com/Article/13099.shtml
- http://www.read.xwpxi.com/Article/520924.shtml
- http://www.read.xwpxi.com/Article/142072.shtml
- http://www.read.xwpxi.com/Article/13906.shtml
- http://www.read.xwpxi.com/Article/25368.shtml
- http://www.read.xwpxi.com/Article/953773.shtml
- http://www.read.xwpxi.com/Article/7866.shtml
- http://www.read.xwpxi.com/Article/053302.shtml
- http://www.read.xwpxi.com/Article/515035.shtml
- http://www.read.xwpxi.com/Article/0857.shtml
- http://www.read.xwpxi.com/Article/4538.shtml
- http://www.read.xwpxi.com/Article/6197395.shtml
- http://www.read.xwpxi.com/Article/9319019.shtml
- http://www.read.xwpxi.com/Article/1349784.shtml
- http://www.read.xwpxi.com/Article/84873.shtml
- http://www.read.xwpxi.com/Article/2830929.shtml
- http://www.read.xwpxi.com/Article/223759.shtml
- http://www.read.xwpxi.com/Article/6916.shtml
- http://www.read.xwpxi.com/Article/681543.shtml
- http://www.read.xwpxi.com/Article/1785805.shtml
- http://www.read.xwpxi.com/Article/1521.shtml
- http://www.read.xwpxi.com/Article/148671.shtml
- http://www.read.xwpxi.com/Article/11852.shtml
- http://www.read.xwpxi.com/Article/42262.shtml
- http://www.read.xwpxi.com/Article/8924.shtml
- http://www.read.xwpxi.com/Article/0832.shtml
- http://www.read.xwpxi.com/Article/29556.shtml
- http://www.read.xwpxi.com/Article/6912.shtml
- http://www.read.xwpxi.com/Article/54579.shtml
- http://www.read.xwpxi.com/Article/9280.shtml
- http://www.read.xwpxi.com/Article/06306.shtml
- http://www.read.xwpxi.com/Article/7446583.shtml
- http://www.read.xwpxi.com/Article/30142.shtml
- http://www.read.xwpxi.com/Article/8445.shtml
- http://www.read.xwpxi.com/Article/7134.shtml
- http://www.read.xwpxi.com/Article/114048.shtml
- http://www.read.xwpxi.com/Article/95112.shtml
- http://www.read.xwpxi.com/Article/3179727.shtml
- http://www.read.xwpxi.com/Article/0629734.shtml
- http://www.read.xwpxi.com/Article/1697.shtml
- http://www.read.xwpxi.com/Article/290801.shtml
- http://www.read.xwpxi.com/Article/34666.shtml
- http://www.read.xwpxi.com/Article/6375.shtml
- http://www.read.xwpxi.com/Article/637622.shtml
- http://www.read.xwpxi.com/Article/078396.shtml
- http://www.read.xwpxi.com/Article/05076.shtml

## 项目结构

```
readx-aggregator/
├── bin/                                # 可执行脚本入口
│   └── cli.js                          # 命令行工具主程序，注册 import/build/serve 子命令
├── src/                                # 核心源码目录
│   ├── core/                           # 核心业务逻辑模块
│   │   ├── importer.js                 # 链接导入器，负责读取批次文件、校验 URL 格式
│   │   ├── fetcher.js                  # HTTP 抓取器，处理请求头、重定向与超时重试
│   │   ├── parser.js                   # 元数据解析器，从 HTML 中抽取标题、日期、关键词
│   │   └── classifier.js               # 分类标签生成器，基于规则与简单统计模型
│   ├── generators/                     # 站点生成模块
│   │   ├── page-builder.js             # 页面构建器，将元数据渲染为 HTML 字符串
│   │   ├── index-generator.js          # 首页索引生成，包含最近更新与标签云
│   │   └── rss-generator.js            # RSS 订阅源生成，供外部阅读器订阅
│   ├── cache/                          # 缓存管理模块
│   │   ├── manager.js                  # 文件缓存读写，基于文章 ID 进行键值存储
│   │   └── cleaner.js                  # 缓存清理策略，支持按时间与容量驱逐
│   └── utils/                          # 通用工具函数集合
│       ├── network.js                  # 网络相关辅助，如 User-Agent 轮换、代理配置
│       ├── string.js                   # 字符串处理，截断、去除 HTML 标签、slug 生成
│       └── validator.js                # 输入校验，URL 合规性、批次文件格式检查
├── data/                               # 数据目录，存放批次文件与持久化元数据
│   ├── batches/                        # 批次文件存储，每批次以 .txt 或 .json 存放
│   │   └── batch_1.txt                 # 第一批次 URL 清单，格式为每行一个链接
│   └── metadata/                       # 抽取后的元数据存储，按批次分目录
│       └── batch_1/                    # 第一批次元数据，包含 .meta.json 与 .index.json
├── templates/                          # 模板文件目录，用于生成 HTML 页面
│   ├── layout.ejs                      # 基础布局模板，包含 head 与导航栏
│   ├── index.ejs                       # 首页模板，展示统计信息与最新列表
│   └── detail.ejs                      # 详情页模板，展示单篇文章的完整元数据
├── dist/                               # 构建输出目录，生成的静态站点文件
│   ├── index.html                      # 首页
│   ├── tags/                           # 按标签分类的页面子目录
│   ├── dates/                          # 按日期归档的页面子目录
│   └── assets/                         # 静态资源文件，CSS 样式与客户端脚本
├── config/                             # 配置文件目录
│   ├── default.json                    # 默认配置，包含超时时间、并发数、缓存路径
│   └── custom.example.json             # 自定义配置示例，供用户覆盖默认值
├── tests/                              # 单元测试与集成测试
│   ├── unit/                           # 单元测试，覆盖核心函数与工具类
│   └── integration/                    # 集成测试，模拟完整导入与构建流程
├── .eslintrc.js                        # ESLint 代码规范配置
├── .gitignore                          # Git 忽略规则，排除 node_modules 与缓存目录
├── package.json                        # 项目依赖与脚本定义
├── README.md                           # 项目说明文档，即当前文件
└── LICENSE                             # MIT 许可证文件
```

## 贡献指南

提交问题报告与功能请求
请在 GitHub Issues 页面选择对应的模板进行提交。缺陷报告需包含复现步骤、预期行为与实际行为，并提供运行环境信息。功能请求需清晰描述应用场景与期望的解决方案。

代码贡献流程
Fork 本仓库后，在您的分支上进行开发。请确保代码通过 ESLint 校验，并为新增功能或修复编写对应的单元测试。提交前请运行 npm test 确认所有测试通过。完成后向主仓库的 develop 分支发起 Pull Request。

文档完善
欢迎对文档进行补充或修正，包括但不限于 README 的错别字修正、使用示例的补充、API 描述的细化。文档修改可直接在主仓库创建分支并提交 PR，无需 Fork。

批次数据扩充
若您拥有合法授权的文章链接列表，且符合项目的数据格式规范，可将其整理为批次文件并提交至 data/batches 目录的示例中。请注意，项目本身不存储文章正文，仅保留元数据索引。

本地开发环境搭建
克隆仓库后执行 npm install 安装依赖。使用 npm run dev 可启动监听模式，代码变动时自动重新构建。项目使用 EJS 作为模板引擎，修改模板后需重新构建方可生效。

## 常见问题

导入链接时部分 URL 返回超时错误，如何处理
项目默认的请求超时时间为 10 秒，单次请求失败后会进行最多 2 次重试，间隔为 2 秒。若目标服务器响应缓慢，可通过修改 config/default.json 中的 requestTimeout 与 retryTimes 字段调整参数。此外，网络环境不稳定时可尝试配置代理，将 proxy 字段设置为有效地址。

生成的静态站点中部分文章标题显示为空或乱码
该问题通常源于源站页面未设置正确的字符编码声明。项目的解析器会优先从 HTTP 响应头的 Content-Type 字段读取编码，其次从 HTML 中的 meta 标签读取。若两者均未提供，将回退为 UTF-8。您可在导入后手动编辑 metadata 目录下对应文章的 .meta.json 文件，补充或修正 title 与 encoding 字段，然后重新执行构建命令即可更新页面。

如何续接新的 URL 批次而不覆盖已有数据
项目支持增量导入模式。在执行导入命令时，请使用 --batch 参数指定一个未被使用的新批次编号，例如 --batch=2，并确保对应的批次文件存在。新批次的元数据将存储在独立的子目录中，构建时会合并所有批次的数据生成统一索引。注意不同批次间若存在相同 URL，系统会以最新批次的元数据为准。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
