# WebLink Indexer

WebLink Indexer 是一个面向技术文档聚合与外部资源索引的开源工具集，专注于将分散在各类技术博客、新闻站点、手册页面中的高质量外链进行结构化采集、分类存储与可检索化展示。项目定位为开发者、技术写作人员与运维工程师的辅助知识库，用于解决日常查阅资料时链接散落、重复检索、上下文丢失等问题。

项目提供从链接抓取、元数据提取、标签化分类到静态站点生成的全链路能力，支持用户自定义解析规则，并内置针对 `read.xwpxi.com` 等常见技术内容站点的适配模板。WebLink Indexer 本身不存储任何版权内容，仅对公开可访问的 URL 进行索引与归类，适合作为个人或团队内部的知识导航层。

## 功能概览

- **批量链接导入与去重**：支持从文本文件、CSV、浏览器书签导出文件批量导入 URL，自动识别重复条目并保留首次添加记录。
- **智能元数据提取**：对每个链接自动请求并解析 HTML 标题、Meta Description、正文首段摘要、最后更新时间，生成标准化的索引卡片。
- **多级标签与分类体系**：允许用户为每个链接添加多个自定义标签，并基于标签组合生成动态分类视图，支持层级标签结构。
- **全文检索与过滤**：内置基于倒排索引的搜索功能，支持按标题、摘要、标签、域名、时间范围多维度过滤，检索结果按相关度排序。
- **静态站点生成器**：将索引数据输出为纯 HTML/CSS/JavaScript 静态网站，适配移动端与桌面端浏览，无需数据库即可部署至任何 Web 服务器或 CDN。
- **定时更新与监控**：集成 cron 驱动的增量更新机制，定期检查已索引链接的状态码与内容变更，标记失效链接并记录变动日志。
- **RESTful API 接口**：提供 JSON 格式的查询、添加、更新、删除接口，便于与其他系统（如自动化脚本、聊天机器人、IDE 插件）集成。

## 应用场景

**技术团队内部知识库维护**  
开发团队在日常工作中积累大量技术方案、排障记录、官方文档参考链接。WebLink Indexer 可作为团队知识库的入口层，将分散在 Wiki、Issue、邮件中的链接统一汇集，并通过标签体系按项目、技术栈、优先级组织，新成员入职时可快速浏览团队常用资源。

**个人技术阅读工作流管理**  
技术从业者每天浏览大量新闻、教程、仓库文档，但事后回溯困难。使用 WebLink Indexer 可在一键保存链接的同时自动抓取摘要，后续通过关键词检索或标签浏览快速定位以往读过的内容，避免重复搜索。

**技术博客与社区的内容关联**  
技术博主或社区运营人员可在文章底部嵌入由 WebLink Indexer 生成的关联链接区块，自动展示与当前主题相关的历史索引条目，提升站内流量闭环与阅读连贯性。

**运维监控的辅助信息源**  
运维工程师可将告警处理手册、常见错误解决方案链接导入 WebLink Indexer，并通过 API 集成至监控面板。当特定错误码触发时，面板直接展示相关链接卡片，缩短故障排查时间。

## 快速开始

以下指令适用于 Linux / macOS / Windows WSL 环境，依赖 Git、Node.js 18+ 与 npm。

```bash
# 克隆仓库
git clone https://github.com/weblink-indexer/weblink-indexer.git
cd weblink-indexer

# 安装依赖
npm install

# 执行初始索引构建（示例数据）
npm run build -- --input ./samples/links.txt --output ./dist

# 启动开发服务器预览静态站点
npm run serve
```

完成上述步骤后，访问 `http://localhost:8080` 即可查看生成的索引首页。如需导入自定义链接列表，替换 `./samples/links.txt` 文件内容或通过 `--input` 参数指定其他文件路径。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行抓取、解析与生成逻辑 |
| npm | 9.x 或 10.x | 包管理器，用于安装项目依赖库 |
| Git | 2.30 及以上 | 版本控制工具，用于克隆仓库与管理补丁 |
| 网络连接 | 稳定出站访问 | 抓取外部链接时需要访问公网，需确保 DNS 解析与 HTTP/HTTPS 出站策略 |
| 存储空间 | 至少 500 MB 可用 | 用于存放索引数据库、缓存页面摘要与生成的静态文件，实际用量随链接数量线性增长 |
| 内存 | 建议 2 GB 以上 | 批量处理大量链接时 Node.js 进程内存占用较高，可通过 `--max-old-space-size` 调整 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/` | 如何安装、配置、导入链接、使用搜索与标签、生成站点、设置定时任务 |
| 开发者指南 | `/docs/developer-guide/` | 如何扩展解析器、自定义元数据提取规则、贡献代码、运行测试套件 |
| API 参考 | `/docs/api-reference/` | RESTful API 各端点的请求格式、响应结构、状态码含义、速率限制策略 |
| 运维部署 | `/docs/deployment/` | 如何将生成的静态站点部署至 Nginx、S3、Cloudflare Pages、GitHub Pages 等平台 |

## 资源列表

- http://www.read.xwpxi.com/Article/5920110.shtml
- http://www.read.xwpxi.com/Article/9974498.shtml
- http://www.read.xwpxi.com/Article/763279.shtml
- http://www.read.xwpxi.com/Article/87868.shtml
- http://www.read.xwpxi.com/Article/2117.shtml
- http://www.read.xwpxi.com/Article/2042505.shtml
- http://www.read.xwpxi.com/Article/2783.shtml
- http://www.read.xwpxi.com/Article/9011.shtml
- http://www.read.xwpxi.com/Article/15088.shtml
- http://www.read.xwpxi.com/Article/564567.shtml
- http://www.read.xwpxi.com/Article/6062322.shtml
- http://www.read.xwpxi.com/Article/9854.shtml
- http://www.read.xwpxi.com/Article/805118.shtml
- http://www.read.xwpxi.com/Article/119141.shtml
- http://www.read.xwpxi.com/Article/01852.shtml
- http://www.read.xwpxi.com/Article/740947.shtml
- http://www.read.xwpxi.com/Article/687643.shtml
- http://www.read.xwpxi.com/Article/4250724.shtml
- http://www.read.xwpxi.com/Article/944226.shtml
- http://www.read.xwpxi.com/Article/91471.shtml
- http://www.read.xwpxi.com/Article/13163.shtml
- http://www.read.xwpxi.com/Article/131514.shtml
- http://www.read.xwpxi.com/Article/0102367.shtml
- http://www.read.xwpxi.com/Article/1953494.shtml
- http://www.read.xwpxi.com/Article/26230.shtml
- http://www.read.xwpxi.com/Article/3282620.shtml
- http://www.read.xwpxi.com/Article/454825.shtml
- http://www.read.xwpxi.com/Article/5719.shtml
- http://www.read.xwpxi.com/Article/88737.shtml
- http://www.read.xwpxi.com/Article/4391.shtml
- http://www.read.xwpxi.com/Article/8386.shtml
- http://www.read.xwpxi.com/Article/61056.shtml
- http://www.read.xwpxi.com/Article/1482.shtml
- http://www.read.xwpxi.com/Article/215734.shtml
- http://www.read.xwpxi.com/Article/1326477.shtml
- http://www.read.xwpxi.com/Article/9090638.shtml
- http://www.read.xwpxi.com/Article/3663.shtml
- http://www.read.xwpxi.com/Article/3756595.shtml
- http://www.read.xwpxi.com/Article/94697.shtml
- http://www.read.xwpxi.com/Article/88375.shtml
- http://www.read.xwpxi.com/Article/075199.shtml
- http://www.read.xwpxi.com/Article/0430.shtml
- http://www.read.xwpxi.com/Article/7812298.shtml
- http://www.read.xwpxi.com/Article/2267.shtml
- http://www.read.xwpxi.com/Article/845366.shtml
- http://www.read.xwpxi.com/Article/47242.shtml
- http://www.read.xwpxi.com/Article/951592.shtml
- http://www.read.xwpxi.com/Article/0571.shtml
- http://www.read.xwpxi.com/Article/835493.shtml
- http://www.read.xwpxi.com/Article/624658.shtml
- http://www.read.xwpxi.com/Article/796805.shtml
- http://www.read.xwpxi.com/Article/7321.shtml
- http://www.read.xwpxi.com/Article/5038.shtml
- http://www.read.xwpxi.com/Article/23904.shtml
- http://www.read.xwpxi.com/Article/74953.shtml
- http://www.read.xwpxi.com/Article/5707746.shtml
- http://www.read.xwpxi.com/Article/4152.shtml
- http://www.read.xwpxi.com/Article/29317.shtml
- http://www.read.xwpxi.com/Article/7044.shtml
- http://www.read.xwpxi.com/Article/68885.shtml
- http://www.read.xwpxi.com/Article/6245888.shtml
- http://www.read.xwpxi.com/Article/421719.shtml
- http://www.read.xwpxi.com/Article/59566.shtml
- http://www.read.xwpxi.com/Article/15987.shtml
- http://www.read.xwpxi.com/Article/84858.shtml
- http://www.read.xwpxi.com/Article/78504.shtml
- http://www.read.xwpxi.com/Article/880109.shtml
- http://www.read.xwpxi.com/Article/8130.shtml
- http://www.read.xwpxi.com/Article/284696.shtml
- http://www.read.xwpxi.com/Article/20220.shtml
- http://www.read.xwpxi.com/Article/31243.shtml
- http://www.read.xwpxi.com/Article/511139.shtml
- http://www.read.xwpxi.com/Article/6964423.shtml
- http://www.read.xwpxi.com/Article/6681.shtml
- http://www.read.xwpxi.com/Article/50640.shtml
- http://www.read.xwpxi.com/Article/1553935.shtml
- http://www.read.xwpxi.com/Article/2171305.shtml
- http://www.read.xwpxi.com/Article/273848.shtml
- http://www.read.xwpxi.com/Article/1439.shtml
- http://www.read.xwpxi.com/Article/782978.shtml
- http://www.read.xwpxi.com/Article/3050794.shtml
- http://www.read.xwpxi.com/Article/534147.shtml
- http://www.read.xwpxi.com/Article/8164.shtml
- http://www.read.xwpxi.com/Article/0210044.shtml
- http://www.read.xwpxi.com/Article/5339.shtml
- http://www.read.xwpxi.com/Article/9562736.shtml
- http://www.read.xwpxi.com/Article/8080899.shtml
- http://www.read.xwpxi.com/Article/009224.shtml
- http://www.read.xwpxi.com/Article/950577.shtml
- http://www.read.xwpxi.com/Article/9962.shtml
- http://www.read.xwpxi.com/Article/56469.shtml
- http://www.read.xwpxi.com/Article/316822.shtml
- http://www.read.xwpxi.com/Article/9958867.shtml
- http://www.read.xwpxi.com/Article/2925.shtml
- http://www.read.xwpxi.com/Article/643275.shtml
- http://www.read.xwpxi.com/Article/52140.shtml
- http://www.read.xwpxi.com/Article/41148.shtml
- http://www.read.xwpxi.com/Article/44361.shtml
- http://www.read.xwpxi.com/Article/194272.shtml
- http://www.read.xwpxi.com/Article/366024.shtml
- http://www.read.xwpxi.com/Article/44604.shtml
- http://www.read.xwpxi.com/Article/291746.shtml
- http://www.read.xwpxi.com/Article/3131993.shtml
- http://www.read.xwpxi.com/Article/1099.shtml
- http://www.read.xwpxi.com/Article/62312.shtml
- http://www.read.xwpxi.com/Article/9207.shtml
- http://www.read.xwpxi.com/Article/7681521.shtml
- http://www.read.xwpxi.com/Article/0230700.shtml
- http://www.read.xwpxi.com/Article/5735903.shtml
- http://www.read.xwpxi.com/Article/7661582.shtml
- http://www.read.xwpxi.com/Article/891855.shtml
- http://www.read.xwpxi.com/Article/902219.shtml
- http://www.read.xwpxi.com/Article/3576377.shtml
- http://www.read.xwpxi.com/Article/8265.shtml
- http://www.read.xwpxi.com/Article/617951.shtml
- http://www.read.xwpxi.com/Article/1451.shtml
- http://www.read.xwpxi.com/Article/45789.shtml
- http://www.read.xwpxi.com/Article/346374.shtml
- http://www.read.xwpxi.com/Article/4186157.shtml
- http://www.read.xwpxi.com/Article/147838.shtml
- http://www.read.xwpxi.com/Article/4544.shtml
- http://www.read.xwpxi.com/Article/6246984.shtml
- http://www.read.xwpxi.com/Article/0970.shtml
- http://www.read.xwpxi.com/Article/92190.shtml
- http://www.read.xwpxi.com/Article/39735.shtml
- http://www.read.xwpxi.com/Article/5252266.shtml
- http://www.read.xwpxi.com/Article/68834.shtml
- http://www.read.xwpxi.com/Article/7186365.shtml
- http://www.read.xwpxi.com/Article/2407294.shtml
- http://www.read.xwpxi.com/Article/811034.shtml
- http://www.read.xwpxi.com/Article/3154431.shtml
- http://www.read.xwpxi.com/Article/3702.shtml
- http://www.read.xwpxi.com/Article/495096.shtml
- http://www.read.xwpxi.com/Article/85301.shtml
- http://www.read.xwpxi.com/Article/288157.shtml
- http://www.read.xwpxi.com/Article/4529.shtml
- http://www.read.xwpxi.com/Article/15460.shtml
- http://www.read.xwpxi.com/Article/2123.shtml
- http://www.read.xwpxi.com/Article/676892.shtml
- http://www.read.xwpxi.com/Article/5282.shtml
- http://www.read.xwpxi.com/Article/42966.shtml
- http://www.read.xwpxi.com/Article/6181.shtml
- http://www.read.xwpxi.com/Article/70252.shtml
- http://www.read.xwpxi.com/Article/2510874.shtml
- http://www.read.xwpxi.com/Article/88504.shtml
- http://www.read.xwpxi.com/Article/0021.shtml
- http://www.read.xwpxi.com/Article/41462.shtml
- http://www.read.xwpxi.com/Article/6831677.shtml
- http://www.read.xwpxi.com/Article/492883.shtml
- http://www.read.xwpxi.com/Article/4583.shtml
- http://www.read.xwpxi.com/Article/1321086.shtml
- http://www.read.xwpxi.com/Article/035735.shtml
- http://www.read.xwpxi.com/Article/8466080.shtml
- http://www.read.xwpxi.com/Article/72736.shtml
- http://www.read.xwpxi.com/Article/0490.shtml
- http://www.read.xwpxi.com/Article/6557.shtml
- http://www.read.xwpxi.com/Article/42321.shtml
- http://www.read.xwpxi.com/Article/3090.shtml
- http://www.read.xwpxi.com/Article/9636431.shtml
- http://www.read.xwpxi.com/Article/69352.shtml
- http://www.read.xwpxi.com/Article/18074.shtml
- http://www.read.xwpxi.com/Article/25414.shtml
- http://www.read.xwpxi.com/Article/4061.shtml
- http://www.read.xwpxi.com/Article/3904419.shtml
- http://www.read.xwpxi.com/Article/69283.shtml
- http://www.read.xwpxi.com/Article/34331.shtml
- http://www.read.xwpxi.com/Article/16964.shtml
- http://www.read.xwpxi.com/Article/4404042.shtml
- http://www.read.xwpxi.com/Article/6142980.shtml
- http://www.read.xwpxi.com/Article/59452.shtml
- http://www.read.xwpxi.com/Article/9014574.shtml
- http://www.read.xwpxi.com/Article/104770.shtml
- http://www.read.xwpxi.com/Article/76816.shtml
- http://www.read.xwpxi.com/Article/3627375.shtml
- http://www.read.xwpxi.com/Article/1841295.shtml
- http://www.read.xwpxi.com/Article/16050.shtml
- http://www.read.xwpxi.com/Article/60419.shtml
- http://www.read.xwpxi.com/Article/244349.shtml
- http://www.read.xwpxi.com/Article/83259.shtml
- http://www.read.xwpxi.com/Article/322658.shtml
- http://www.read.xwpxi.com/Article/77919.shtml
- http://www.read.xwpxi.com/Article/176392.shtml
- http://www.read.xwpxi.com/Article/9464.shtml
- http://www.read.xwpxi.com/Article/9719475.shtml
- http://www.read.xwpxi.com/Article/697109.shtml
- http://www.read.xwpxi.com/Article/04937.shtml
- http://www.read.xwpxi.com/Article/2452.shtml
- http://www.read.xwpxi.com/Article/46053.shtml
- http://www.read.xwpxi.com/Article/6108483.shtml
- http://www.read.xwpxi.com/Article/233745.shtml
- http://www.read.xwpxi.com/Article/467876.shtml
- http://www.read.xwpxi.com/Article/0424.shtml
- http://www.read.xwpxi.com/Article/3427.shtml
- http://www.read.xwpxi.com/Article/1819103.shtml
- http://www.read.xwpxi.com/Article/0809052.shtml
- http://www.read.xwpxi.com/Article/859574.shtml
- http://www.read.xwpxi.com/Article/1085654.shtml
- http://www.read.xwpxi.com/Article/83585.shtml
- http://www.read.xwpxi.com/Article/50568.shtml
- http://www.read.xwpxi.com/Article/04951.shtml
- http://www.read.xwpxi.com/Article/439596.shtml
- http://www.read.xwpxi.com/Article/271293.shtml
- http://www.read.xwpxi.com/Article/3052.shtml
- http://www.read.xwpxi.com/Article/329629.shtml
- http://www.read.xwpxi.com/Article/70352.shtml
- http://www.read.xwpxi.com/Article/60298.shtml
- http://www.read.xwpxi.com/Article/81474.shtml
- http://www.read.xwpxi.com/Article/069148.shtml
- http://www.read.xwpxi.com/Article/4626316.shtml
- http://www.read.xwpxi.com/Article/4101.shtml
- http://www.read.xwpxi.com/Article/6807.shtml
- http://www.read.xwpxi.com/Article/8455446.shtml
- http://www.read.xwpxi.com/Article/3248803.shtml
- http://www.read.xwpxi.com/Article/916534.shtml
- http://www.read.xwpxi.com/Article/20737.shtml
- http://www.read.xwpxi.com/Article/601401.shtml
- http://www.read.xwpxi.com/Article/81014.shtml
- http://www.read.xwpxi.com/Article/4507879.shtml
- http://www.read.xwpxi.com/Article/87534.shtml
- http://www.read.xwpxi.com/Article/0391.shtml
- http://www.read.xwpxi.com/Article/785953.shtml
- http://www.read.xwpxi.com/Article/225528.shtml
- http://www.read.xwpxi.com/Article/4861.shtml
- http://www.read.xwpxi.com/Article/881932.shtml
- http://www.read.xwpxi.com/Article/5304242.shtml
- http://www.read.xwpxi.com/Article/5220668.shtml
- http://www.read.xwpxi.com/Article/63101.shtml
- http://www.read.xwpxi.com/Article/4468964.shtml
- http://www.read.xwpxi.com/Article/807998.shtml
- http://www.read.xwpxi.com/Article/7587.shtml
- http://www.read.xwpxi.com/Article/853413.shtml
- http://www.read.xwpxi.com/Article/94554.shtml
- http://www.read.xwpxi.com/Article/2207.shtml
- http://www.read.xwpxi.com/Article/43015.shtml
- http://www.read.xwpxi.com/Article/7511.shtml
- http://www.read.xwpxi.com/Article/2329.shtml
- http://www.read.xwpxi.com/Article/5258186.shtml
- http://www.read.xwpxi.com/Article/27571.shtml
- http://www.read.xwpxi.com/Article/552227.shtml
- http://www.read.xwpxi.com/Article/1787014.shtml
- http://www.read.xwpxi.com/Article/6652007.shtml
- http://www.read.xwpxi.com/Article/4562.shtml
- http://www.read.xwpxi.com/Article/6449.shtml
- http://www.read.xwpxi.com/Article/9333375.shtml
- http://www.read.xwpxi.com/Article/351469.shtml
- http://www.read.xwpxi.com/Article/486097.shtml
- http://www.read.xwpxi.com/Article/9922258.shtml
- http://www.read.xwpxi.com/Article/7753.shtml
- http://www.read.xwpxi.com/Article/5461779.shtml
- http://www.read.xwpxi.com/Article/4221147.shtml

## 项目结构

```
weblink-indexer/
├── src/
│   ├── core/                     # 核心逻辑模块
│   │   ├── crawler.js            # 链接抓取与HTTP请求调度，含重试与超时控制
│   │   ├── parser.js             # HTML元数据解析，基于cheerio实现选择器提取
│   │   ├── indexer.js            # 倒排索引构建与更新，管理词项-文档映射
│   │   └── storage.js            # 本地JSON存储读写，包含增量合并与备份
│   ├── api/                      # RESTful API 路由与控制器
│   │   ├── routes.js             # 路由注册，定义/v1/links等端点
│   │   └── handlers.js           # 请求校验、业务逻辑调用与响应格式化
│   ├── generator/                # 静态站点生成器
│   │   ├── template.js           # HTML模板引擎，支持布局与组件插槽
│   │   ├── page-builder.js       # 分页逻辑、标签聚合页、详情页构建
│   │   └── assets/               # 内置CSS样式与JavaScript交互脚本
│   ├── cli/                      # 命令行入口
│   │   ├── build.js              # build命令实现，整合抓取-索引-生成流程
│   │   ├── serve.js              # 开发服务器启动，带热重载支持
│   │   └── update.js             # 增量更新命令，仅处理新增或变更链接
│   └── adapters/                 # 站点适配器
│       └── read-xwpxi.js         # 针对read.xwpxi.com的专用解析规则，含字段映射
├── config/                       # 配置文件目录
│   ├── default.json              # 默认配置：并发数、超时时间、输出路径
│   └── custom.json               # 用户自定义配置，覆盖默认值（不提交至仓库）
├── samples/                      # 示例数据
│   └── links.txt                 # 初始链接列表，每行一个URL
├── tests/                        # 单元测试与集成测试
│   ├── crawler.test.js           # 抓取模块的模拟网络测试
│   ├── parser.test.js            # 解析器针对各类HTML结构的测试用例
│   └── indexer.test.js           # 索引增删改查的正确性验证
├── docs/                         # 完整文档（见文档导航章节）
├── dist/                         # 生成的静态站点输出目录（构建后出现）
├── .github/                      # GitHub Actions 工作流
│   └── workflows/                # 持续集成与自动部署配置
├── package.json                  # npm 项目配置，含依赖与脚本定义
├── README.md                     # 本文件
└── LICENSE                       # MIT 许可证文本
```

## 贡献指南

1. 查阅开发者指南文档了解项目架构、代码规范与测试要求。建议从标记为 `good-first-issue` 的 GitHub Issue 入手，熟悉代码流程。

2. 在 GitHub 上 Fork 本仓库，并在本地新建功能分支（如 `feature/add-new-adapter`）。分支命名采用 `类型/简述` 格式，类型包括 `feature`、`fix`、`docs`、`refactor`。

3. 完成代码修改后，确保所有现有测试通过，并为新增功能或修复补充相应测试用例。运行 `npm run test` 执行全部测试套件，覆盖率不低于 85%。

4. 提交前运行 `npm run lint` 与 `npm run format` 统一代码风格。提交信息采用 Conventional Commits 规范，如 `feat: add support for custom meta extractor`。

5. 发起 Pull Request 至主仓库的 `main` 分支，PR 描述中说明改动动机、实现方式、影响范围以及是否包含破坏性变更。维护者将在 7 个工作日内完成审核。

## 常见问题

**问：如何处理目标站点反爬限制或频繁返回 429/403 状态码？**

答：项目内置了指数退避重试机制，初始重试延迟为 1 秒，最大延迟为 60 秒。用户可在 `config/default.json` 中调整 `retry.maxAttempts` 和 `retry.baseDelay` 参数。对于严格限制的站点，建议配置 `request.headers` 中的 `User-Agent` 和 `Referer` 模拟真实浏览器访问，或通过 `adapters` 目录下的专用适配器设置更长的请求间隔。如果站点要求 cookie 或 JavaScript 渲染，可使用 Puppeteer 扩展模式（文档部署章节有说明）。

**问：索引的链接数量上限是多少？性能如何？**

答：本项目设计目标为处理 5000 至 10000 个链接的个人或团队使用场景。在 2 GB 内存、4 核 CPU 的环境下，初次抓取 1000 个链接（含元数据解析）约需 3 至 5 分钟（取决于网络响应速度）。生成静态站点时，5000 个链接的页面渲染耗时约 8 至 12 秒。索引存储采用分片 JSON 文件，单文件大小建议不超过 50 MB，超过时可通过配置开启分片存储模式。如需索引更大规模的链接，建议结合 Redis 或 SQLite 后端（未来版本规划）。

**问：如何迁移或备份已索引的数据？**

答：所有索引数据默认存储在项目根目录下的 `.data/` 文件夹中，包含 `links.json`（链接元数据）、`tags.json`（标签映射）、`index.json`（倒排索引）。备份时直接复制该文件夹即可。恢复时，将备份文件夹放置于相同路径，重新运行 `npm run build -- --skip-crawl` 即可基于已有数据重新生成静态站点，无需重复抓取外部链接。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
