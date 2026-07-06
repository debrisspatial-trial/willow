# ResourceBridge

ResourceBridge 是一个面向开发者、技术研究人员与内容创作者的轻量级技术资源外链聚合与导航工具。该项目不存储任何实际内容，仅提供结构化索引与访问入口，帮助用户快速定位分散在互联网各处的技术文章、教程、文档与案例页面。ResourceBridge 适用于需要批量整理、分类、检索和分享外部技术链接的个人或团队，尤其适合作为内部知识库、技术周报素材库或学习路径辅助系统使用。

ResourceBridge 的核心设计理念是极简、可扩展与无依赖。项目本身由静态 HTML 和纯文本索引构成，无需数据库，无需构建工具，可在任何支持 HTTP 服务的环境下运行。通过约定优于配置的目录结构，用户可以轻松新增、删除或分类整理链接集合。ResourceBridge 不追踪用户行为，不植入广告，不依赖第三方前端框架，所有样式与脚本均内联自包含，确保长期可用性与低维护成本。

## 功能概览

批量外链导入与自动结构化存储：支持通过编辑单一文本索引文件批量添加 URL，系统自动按资源类型、来源域名或自定义标签生成分类目录。

多维度资源检索：提供基于标题关键词、来源域名、添加时间区间和自定义标签的全文检索能力，检索结果按相关度与时间排序。

静态资源预览代理：对于支持跨域访问的 HTML 页面，提供纯文本内容提取与代码片段高亮预览功能，帮助用户在不离开本站的情况下快速判断资源价值。

链接可用性健康检查：内置定时任务模块，可配置周期对已收录链接进行 HTTP 状态码检测，自动标记失效链接并生成异常报告。

自定义元数据扩展：每条链接支持添加备注、重要程度评分、阅读时长估算和关联资源 ID，便于构建个人或团队知识图谱。

导出与集成能力：支持将当前链接集合导出为 JSON、Markdown 表格或 CSV 格式，便于导入 Notion、Obsidian、Hugo 或 VuePress 等第三方工具。

访问统计与热度排序：基于本地存储记录每个链接的点击次数与最后访问时间，提供按热度、时效性和随机三种排序模式。

响应式布局与暗色主题：适配桌面、平板与移动设备，内置系统主题跟随与手动切换两种暗色模式，保证不同环境下的阅读体验。

## 应用场景

技术团队内部知识沉淀与共享：团队负责人或技术文档维护者可以使用 ResourceBridge 汇总项目开发过程中参考的官方文档、博客文章、解决方案和调试案例，统一入口，减少重复搜索时间。团队成员可通过检索功能快速找到与当前问题相关的历史资料。

个人技术学习路径管理：学习者可以在学习新技术栈（如 Rust、Kubernetes、WebAssembly）时，将遇到的优质教程、API 参考和开源项目示例集中收录，并利用重要程度评分和阅读时长估算规划每日学习任务，形成可追溯的学习轨迹。

技术内容运营与编辑辅助：技术社区运营、新闻简报编辑或自媒体创作者可以使用 ResourceBridge 作为素材暂存池，批量采集潜在引用来源，通过备注字段记录选题思路、写作进度和稿件关联，提升内容生产流程的条理性。

离线归档与本地知识库构建：在内部网络或无互联网环境中，运维人员可将 ResourceBridge 部署在内网服务器，收录团队内部 Wiki、代码仓库地址和 CI/CD 流水线仪表盘，结合链接健康检查功能监控内网服务可用性。

## 快速开始

以下命令演示如何从 GitHub 克隆项目、安装依赖（如果需要）并启动开发服务器。ResourceBridge 核心无需任何依赖，但若启用高级预览功能，需安装 Node.js 环境。

```bash
# 克隆代码仓库
git clone https://github.com/resourcebridge/resourcebridge.git
cd resourcebridge

# 安装可选依赖（用于预览和健康检查模块）
npm install

# 启动内置静态服务，默认监听 8080 端口
npm start
# 或使用 Python 简易服务器
python3 -m http.server 8080
```

启动后，在浏览器中访问 http://localhost:8080 即可看到主界面。默认索引文件位于 `data/links.txt`，你可以直接编辑该文件添加或删除链接。添加链接后刷新页面，系统会自动重新构建分类索引。

## 安装要求

ResourceBridge 的主体功能完全静态化，不依赖任何外部运行环境。若需要使用完整功能集，包括定时健康检查、预览内容提取和导出增强，则需要满足以下要求：

| 依赖组件 | 必需性 | 说明 |
| :--- | :--- | :--- |
| 现代浏览器（Chrome / Firefox / Edge / Safari 最新两版） | 必需 | 用于访问界面和交互功能，不支持 IE 及老旧浏览器 |
| HTTP 服务器（Nginx / Apache / Caddy 或 Python http.server） | 必需 | 任何能提供静态文件服务的 HTTP 服务器均可 |
| Node.js 18.x 或更高版本 | 可选 | 仅当需要使用预览代理、健康检查定时任务和高级导出功能时安装 |
| npm 或 yarn | 可选 | 用于安装 node-fetch、cheerio 等可选依赖包 |
| Git 2.25 或更高版本 | 可选 | 仅当通过 git clone 方式获取项目源码时需要 |
| 磁盘空间至少 10MB | 必需 | 用于存储索引文件、配置和静态资源，不存储实际页面内容 |

## 文档导航

ResourceBridge 提供完整的用户手册、API 参考和开发者指南，以下表格概括了主要文档模块及其解决的核心问题：

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 用户入门 | /docs/quick-start.md | 如何添加第一批链接、如何分类、如何搜索和分享 |
| 配置参考 | /docs/configuration.md | 如何修改端口、调整健康检查间隔、自定义分类规则 |
| 元数据规范 | /docs/metadata-schema.md | 每条链接支持哪些字段、格式要求、字段含义和示例 |
| 开发与扩展 | /docs/development.md | 如何新增预览解析器、自定义导出模板、集成外部 API |

## 资源列表

- http://www.read.xwpxi.com/Article/5409.shtml
- http://www.read.xwpxi.com/Article/7264.shtml
- http://www.read.xwpxi.com/Article/846639.shtml
- http://www.read.xwpxi.com/Article/3054.shtml
- http://www.read.xwpxi.com/Article/028956.shtml
- http://www.read.xwpxi.com/Article/4942588.shtml
- http://www.read.xwpxi.com/Article/347856.shtml
- http://www.read.xwpxi.com/Article/6996070.shtml
- http://www.read.xwpxi.com/Article/7863211.shtml
- http://www.read.xwpxi.com/Article/8323209.shtml
- http://www.read.xwpxi.com/Article/265617.shtml
- http://www.read.xwpxi.com/Article/529456.shtml
- http://www.read.xwpxi.com/Article/75966.shtml
- http://www.read.xwpxi.com/Article/3185039.shtml
- http://www.read.xwpxi.com/Article/934306.shtml
- http://www.read.xwpxi.com/Article/605274.shtml
- http://www.read.xwpxi.com/Article/46028.shtml
- http://www.read.xwpxi.com/Article/17418.shtml
- http://www.read.xwpxi.com/Article/361673.shtml
- http://www.read.xwpxi.com/Article/276360.shtml
- http://www.read.xwpxi.com/Article/448984.shtml
- http://www.read.xwpxi.com/Article/0859.shtml
- http://www.read.xwpxi.com/Article/537902.shtml
- http://www.read.xwpxi.com/Article/9740321.shtml
- http://www.read.xwpxi.com/Article/37352.shtml
- http://www.read.xwpxi.com/Article/2562996.shtml
- http://www.read.xwpxi.com/Article/410946.shtml
- http://www.read.xwpxi.com/Article/6808701.shtml
- http://www.read.xwpxi.com/Article/2393826.shtml
- http://www.read.xwpxi.com/Article/1238286.shtml
- http://www.read.xwpxi.com/Article/8244.shtml
- http://www.read.xwpxi.com/Article/267449.shtml
- http://www.read.xwpxi.com/Article/83552.shtml
- http://www.read.xwpxi.com/Article/86825.shtml
- http://www.read.xwpxi.com/Article/906646.shtml
- http://www.read.xwpxi.com/Article/5894.shtml
- http://www.read.xwpxi.com/Article/0972.shtml
- http://www.read.xwpxi.com/Article/61159.shtml
- http://www.read.xwpxi.com/Article/4930.shtml
- http://www.read.xwpxi.com/Article/8903701.shtml
- http://www.read.xwpxi.com/Article/430739.shtml
- http://www.read.xwpxi.com/Article/8568224.shtml
- http://www.read.xwpxi.com/Article/1847.shtml
- http://www.read.xwpxi.com/Article/1917853.shtml
- http://www.read.xwpxi.com/Article/4747008.shtml
- http://www.read.xwpxi.com/Article/9409117.shtml
- http://www.read.xwpxi.com/Article/19587.shtml
- http://www.read.xwpxi.com/Article/9920926.shtml
- http://www.read.xwpxi.com/Article/172385.shtml
- http://www.read.xwpxi.com/Article/927544.shtml
- http://www.read.xwpxi.com/Article/61591.shtml
- http://www.read.xwpxi.com/Article/8424.shtml
- http://www.read.xwpxi.com/Article/3684978.shtml
- http://www.read.xwpxi.com/Article/9656283.shtml
- http://www.read.xwpxi.com/Article/5139.shtml
- http://www.read.xwpxi.com/Article/6643217.shtml
- http://www.read.xwpxi.com/Article/7357675.shtml
- http://www.read.xwpxi.com/Article/3978678.shtml
- http://www.read.xwpxi.com/Article/2161.shtml
- http://www.read.xwpxi.com/Article/668980.shtml
- http://www.read.xwpxi.com/Article/09118.shtml
- http://www.read.xwpxi.com/Article/165021.shtml
- http://www.read.xwpxi.com/Article/636941.shtml
- http://www.read.xwpxi.com/Article/340554.shtml
- http://www.read.xwpxi.com/Article/9400822.shtml
- http://www.read.xwpxi.com/Article/9748723.shtml
- http://www.read.xwpxi.com/Article/026899.shtml
- http://www.read.xwpxi.com/Article/6378.shtml
- http://www.read.xwpxi.com/Article/025815.shtml
- http://www.read.xwpxi.com/Article/82447.shtml
- http://www.read.xwpxi.com/Article/1547225.shtml
- http://www.read.xwpxi.com/Article/419112.shtml
- http://www.read.xwpxi.com/Article/899117.shtml
- http://www.read.xwpxi.com/Article/2695978.shtml
- http://www.read.xwpxi.com/Article/7121.shtml
- http://www.read.xwpxi.com/Article/7247763.shtml
- http://www.read.xwpxi.com/Article/241019.shtml
- http://www.read.xwpxi.com/Article/1435584.shtml
- http://www.read.xwpxi.com/Article/491220.shtml
- http://www.read.xwpxi.com/Article/4722.shtml
- http://www.read.xwpxi.com/Article/298379.shtml
- http://www.read.xwpxi.com/Article/44354.shtml
- http://www.read.xwpxi.com/Article/7497764.shtml
- http://www.read.xwpxi.com/Article/7899607.shtml
- http://www.read.xwpxi.com/Article/5723.shtml
- http://www.read.xwpxi.com/Article/5392384.shtml
- http://www.read.xwpxi.com/Article/670238.shtml
- http://www.read.xwpxi.com/Article/7567.shtml
- http://www.read.xwpxi.com/Article/64009.shtml
- http://www.read.xwpxi.com/Article/1851.shtml
- http://www.read.xwpxi.com/Article/5166.shtml
- http://www.read.xwpxi.com/Article/587915.shtml
- http://www.read.xwpxi.com/Article/55318.shtml
- http://www.read.xwpxi.com/Article/8081.shtml
- http://www.read.xwpxi.com/Article/3863.shtml
- http://www.read.xwpxi.com/Article/2680.shtml
- http://www.read.xwpxi.com/Article/5371.shtml
- http://www.read.xwpxi.com/Article/715362.shtml
- http://www.read.xwpxi.com/Article/804636.shtml
- http://www.read.xwpxi.com/Article/844885.shtml
- http://www.read.xwpxi.com/Article/8306402.shtml
- http://www.read.xwpxi.com/Article/46952.shtml
- http://www.read.xwpxi.com/Article/8396524.shtml
- http://www.read.xwpxi.com/Article/9193447.shtml
- http://www.read.xwpxi.com/Article/6788847.shtml
- http://www.read.xwpxi.com/Article/8370406.shtml
- http://www.read.xwpxi.com/Article/9155867.shtml
- http://www.read.xwpxi.com/Article/63894.shtml
- http://www.read.xwpxi.com/Article/90986.shtml
- http://www.read.xwpxi.com/Article/518633.shtml
- http://www.read.xwpxi.com/Article/55964.shtml
- http://www.read.xwpxi.com/Article/4657.shtml
- http://www.read.xwpxi.com/Article/04630.shtml
- http://www.read.xwpxi.com/Article/48614.shtml
- http://www.read.xwpxi.com/Article/790356.shtml
- http://www.read.xwpxi.com/Article/13554.shtml
- http://www.read.xwpxi.com/Article/6904.shtml
- http://www.read.xwpxi.com/Article/4496.shtml
- http://www.read.xwpxi.com/Article/299425.shtml
- http://www.read.xwpxi.com/Article/4259.shtml
- http://www.read.xwpxi.com/Article/03786.shtml
- http://www.read.xwpxi.com/Article/5175462.shtml
- http://www.read.xwpxi.com/Article/9116152.shtml
- http://www.read.xwpxi.com/Article/6483.shtml
- http://www.read.xwpxi.com/Article/80302.shtml
- http://www.read.xwpxi.com/Article/1361730.shtml
- http://www.read.xwpxi.com/Article/5688147.shtml
- http://www.read.xwpxi.com/Article/2478.shtml
- http://www.read.xwpxi.com/Article/9934.shtml
- http://www.read.xwpxi.com/Article/329771.shtml
- http://www.read.xwpxi.com/Article/304836.shtml
- http://www.read.xwpxi.com/Article/60887.shtml
- http://www.read.xwpxi.com/Article/1384.shtml
- http://www.read.xwpxi.com/Article/1722613.shtml
- http://www.read.xwpxi.com/Article/5660.shtml
- http://www.read.xwpxi.com/Article/2046.shtml
- http://www.read.xwpxi.com/Article/095924.shtml
- http://www.read.xwpxi.com/Article/8858.shtml
- http://www.read.xwpxi.com/Article/5582721.shtml
- http://www.read.xwpxi.com/Article/9318068.shtml
- http://www.read.xwpxi.com/Article/1724.shtml
- http://www.read.xwpxi.com/Article/431836.shtml
- http://www.read.xwpxi.com/Article/52705.shtml
- http://www.read.xwpxi.com/Article/89249.shtml
- http://www.read.xwpxi.com/Article/7450580.shtml
- http://www.read.xwpxi.com/Article/4268621.shtml
- http://www.read.xwpxi.com/Article/2295334.shtml
- http://www.read.xwpxi.com/Article/216360.shtml
- http://www.read.xwpxi.com/Article/1820791.shtml
- http://www.read.xwpxi.com/Article/949662.shtml
- http://www.read.xwpxi.com/Article/494232.shtml
- http://www.read.xwpxi.com/Article/5950726.shtml
- http://www.read.xwpxi.com/Article/3276151.shtml
- http://www.read.xwpxi.com/Article/66754.shtml
- http://www.read.xwpxi.com/Article/7230324.shtml
- http://www.read.xwpxi.com/Article/7284.shtml
- http://www.read.xwpxi.com/Article/58321.shtml
- http://www.read.xwpxi.com/Article/53283.shtml
- http://www.read.xwpxi.com/Article/786935.shtml
- http://www.read.xwpxi.com/Article/885162.shtml
- http://www.read.xwpxi.com/Article/249677.shtml
- http://www.read.xwpxi.com/Article/1165156.shtml
- http://www.read.xwpxi.com/Article/84436.shtml
- http://www.read.xwpxi.com/Article/580218.shtml
- http://www.read.xwpxi.com/Article/0635.shtml
- http://www.read.xwpxi.com/Article/09659.shtml
- http://www.read.xwpxi.com/Article/5514.shtml
- http://www.read.xwpxi.com/Article/43533.shtml
- http://www.read.xwpxi.com/Article/1614868.shtml
- http://www.read.xwpxi.com/Article/2876.shtml
- http://www.read.xwpxi.com/Article/24989.shtml
- http://www.read.xwpxi.com/Article/44796.shtml
- http://www.read.xwpxi.com/Article/4843198.shtml
- http://www.read.xwpxi.com/Article/8369008.shtml
- http://www.read.xwpxi.com/Article/8923572.shtml
- http://www.read.xwpxi.com/Article/23154.shtml
- http://www.read.xwpxi.com/Article/892420.shtml
- http://www.read.xwpxi.com/Article/4990.shtml
- http://www.read.xwpxi.com/Article/1041486.shtml
- http://www.read.xwpxi.com/Article/75378.shtml
- http://www.read.xwpxi.com/Article/21017.shtml
- http://www.read.xwpxi.com/Article/618343.shtml
- http://www.read.xwpxi.com/Article/4872.shtml
- http://www.read.xwpxi.com/Article/1777.shtml
- http://www.read.xwpxi.com/Article/051365.shtml
- http://www.read.xwpxi.com/Article/8116616.shtml
- http://www.read.xwpxi.com/Article/9337.shtml
- http://www.read.xwpxi.com/Article/3650.shtml
- http://www.read.xwpxi.com/Article/93926.shtml
- http://www.read.xwpxi.com/Article/642832.shtml
- http://www.read.xwpxi.com/Article/08718.shtml
- http://www.read.xwpxi.com/Article/29375.shtml
- http://www.read.xwpxi.com/Article/3423239.shtml
- http://www.read.xwpxi.com/Article/29766.shtml
- http://www.read.xwpxi.com/Article/1669.shtml
- http://www.read.xwpxi.com/Article/0151.shtml
- http://www.read.xwpxi.com/Article/3386417.shtml
- http://www.read.xwpxi.com/Article/8730462.shtml
- http://www.read.xwpxi.com/Article/376037.shtml
- http://www.read.xwpxi.com/Article/174941.shtml
- http://www.read.xwpxi.com/Article/067813.shtml
- http://www.read.xwpxi.com/Article/4984728.shtml
- http://www.read.xwpxi.com/Article/70086.shtml
- http://www.read.xwpxi.com/Article/28125.shtml
- http://www.read.xwpxi.com/Article/7544.shtml
- http://www.read.xwpxi.com/Article/3659.shtml
- http://www.read.xwpxi.com/Article/93324.shtml
- http://www.read.xwpxi.com/Article/92126.shtml
- http://www.read.xwpxi.com/Article/6516.shtml
- http://www.read.xwpxi.com/Article/2756.shtml
- http://www.read.xwpxi.com/Article/6284000.shtml
- http://www.read.xwpxi.com/Article/405329.shtml
- http://www.read.xwpxi.com/Article/326132.shtml
- http://www.read.xwpxi.com/Article/0335.shtml
- http://www.read.xwpxi.com/Article/5348831.shtml
- http://www.read.xwpxi.com/Article/62882.shtml
- http://www.read.xwpxi.com/Article/57858.shtml
- http://www.read.xwpxi.com/Article/1680459.shtml
- http://www.read.xwpxi.com/Article/62460.shtml
- http://www.read.xwpxi.com/Article/549162.shtml
- http://www.read.xwpxi.com/Article/5483.shtml
- http://www.read.xwpxi.com/Article/3948548.shtml
- http://www.read.xwpxi.com/Article/34252.shtml
- http://www.read.xwpxi.com/Article/6584361.shtml
- http://www.read.xwpxi.com/Article/797996.shtml
- http://www.read.xwpxi.com/Article/71006.shtml
- http://www.read.xwpxi.com/Article/31790.shtml
- http://www.read.xwpxi.com/Article/51310.shtml
- http://www.read.xwpxi.com/Article/5915.shtml
- http://www.read.xwpxi.com/Article/55569.shtml
- http://www.read.xwpxi.com/Article/4421.shtml
- http://www.read.xwpxi.com/Article/0816828.shtml
- http://www.read.xwpxi.com/Article/8631862.shtml
- http://www.read.xwpxi.com/Article/97365.shtml
- http://www.read.xwpxi.com/Article/9939.shtml
- http://www.read.xwpxi.com/Article/8079444.shtml
- http://www.read.xwpxi.com/Article/65288.shtml
- http://www.read.xwpxi.com/Article/308695.shtml
- http://www.read.xwpxi.com/Article/8766278.shtml
- http://www.read.xwpxi.com/Article/566243.shtml
- http://www.read.xwpxi.com/Article/25096.shtml
- http://www.read.xwpxi.com/Article/63863.shtml
- http://www.read.xwpxi.com/Article/9486.shtml
- http://www.read.xwpxi.com/Article/5665.shtml
- http://www.read.xwpxi.com/Article/94696.shtml
- http://www.read.xwpxi.com/Article/1739246.shtml
- http://www.read.xwpxi.com/Article/754502.shtml
- http://www.read.xwpxi.com/Article/06775.shtml
- http://www.read.xwpxi.com/Article/767612.shtml
- http://www.read.xwpxi.com/Article/62895.shtml

## 项目结构

ResourceBridge 采用约定式目录结构，所有用户数据与配置均集中在 data 和 config 目录下，静态资源与页面模板分离。以下为项目根目录的完整结构示意：

```
resourcebridge/
├── index.html                  # 主入口页面，包含布局框架与全局样式
├── favicon.ico                 # 站点图标
├── robots.txt                  # 搜索引擎爬虫规则，禁止收录外链页面
├── CNAME                       # 自定义域名配置（若部署在 GitHub Pages）
├── 404.html                    # 自定义错误页面
├── assets/                     # 静态资源目录
│   ├── css/
│   │   ├── base.css            # 基础重置与排版样式
│   │   ├── theme-light.css     # 亮色主题变量定义
│   │   └── theme-dark.css      # 暗色主题变量定义
│   ├── js/
│   │   ├── core.js             # 核心交互逻辑：检索、分页、排序
│   │   ├── storage.js          # localStorage 读写封装
│   │   ├── health.js           # 链接健康检查前端调度器
│   │   └── exporter.js         # 导出模块（JSON / CSV / Markdown）
│   └── fonts/                  # 包含系统字体回退与图标字体（可选）
├── data/                       # 用户数据目录（核心）
│   ├── links.txt               # 主索引文件，每行一个 URL，支持 # 注释
│   ├── metadata.json           # 每条链接的元数据扩展（标签、备注、评分）
│   ├── tags.index              # 标签倒排索引，用于加速分类检索
│   └── health.log              # 健康检查历史记录（滚动存储）
├── config/                     # 配置文件目录
│   ├── app.json                # 应用级配置：站点标题、每页条数、默认排序
│   ├── crawler.json            # 预览代理配置：超时时间、最大内容长度
│   └── whitelist.txt           # 允许预览的域名白名单
├── scripts/                    # 辅助脚本（可选功能）
│   ├── import.js               # 批量导入外部文本列表
│   ├── export.js               # 命令行导出工具
│   └── health-check.js         # 独立运行的定时健康检查进程
├── docs/                       # 文档目录
│   ├── quick-start.md
│   ├── configuration.md
│   ├── metadata-schema.md
│   └── development.md
├── tests/                      # 单元测试（使用 Node.js 原生 assert）
│   ├── storage.test.js
│   ├── parser.test.js
│   └── health.test.js
├── .gitignore                  # Git 忽略规则（忽略 data/health.log 等）
├── package.json                # npm 项目描述文件（可选依赖声明）
├── package-lock.json           # 锁定依赖版本
└── LICENSE                     # MIT 许可证文件
```

## 贡献指南

ResourceBridge 欢迎各类贡献，包括但不限于新增索引规则、优化预览解析器、完善文档和修复缺陷。请遵循以下步骤参与项目：

1. 在 GitHub 上 Fork 本仓库至个人账号，并克隆到本地开发环境。建议在 dev 分支上进行所有修改，保持 main 分支与上游同步。

2. 运行 `npm install` 安装开发依赖（如 ESLint、Prettier），提交前执行 `npm run lint` 和 `npm run format` 以保证代码风格一致。若新增或修改了核心功能，请在 tests 目录下补充相应的单元测试用例，确保所有测试通过（`npm test`）。

3. 对于新增功能或重大变更，请先创建 Issue 描述设计思路和使用场景，与维护者沟通后再着手实现，避免无效工作。文档类变更可直接提交 Pull Request。

4. 提交 Pull Request 时，请填写清晰的变更描述，包含动机、实现方式、测试结果和兼容性说明。PR 标题需遵循约定式提交格式，例如 `feat: add support for custom sorting fields` 或 `fix: correct metadata parsing for empty tags`。

5. 代码审查通过后，维护者将合并 PR 并更新 CHANGELOG。所有贡献者将自动列入 CONTRIBUTORS 列表，除非明确要求匿名。

## 常见问题

Q: ResourceBridge 是否存储外部页面的完整内容或快照？
A: 不存储。ResourceBridge 仅保留 URL 和用户手动添加的元数据（如标签、备注）。预览功能仅在用户主动点击时实时请求外部页面，且只提取纯文本内容，不保存任何快照到本地。所有数据均为用户自有，完全可控。

Q: 收录的链接数量很大时，检索和加载速度是否会变慢？
A: ResourceBridge 的索引文件为纯文本和轻量 JSON 结构，单批次 250 条链接的规模下，检索耗时在本地环境通常低于 50 毫秒。对于超过 5000 条链接的场景，建议启用服务端检索方案或使用浏览器端 Web Worker 进行异步处理。项目文档中提供了分页和懒加载配置建议。

Q: 健康检查功能如何配置？是否会影响外部站点？
A: 健康检查通过 HEAD 请求检测链接状态，不会下载页面完整内容，对目标服务器影响极小。默认检查间隔为 24 小时，并发数限制为 5 个连接，避免触发目标站点限流策略。所有检查记录仅存储于本地 `health.log`，不会上传至任何外部服务。

## 许可证

ResourceBridge 使用 MIT 许可证。你可以自由使用、修改、分发本软件，包括商业用途，但需保留原始版权声明和许可声明。完整许可证文本请参见项目根目录下的 LICENSE 文件。

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
