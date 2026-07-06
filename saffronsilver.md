# ResourceBridge

ResourceBridge 是一个面向技术文档聚合与语义化外链管理的高效工具集。该项目不提供内容存储，而是通过结构化索引、标签分类与可用性检测，帮助开发者、技术作者与团队知识管理员将散落在各处的优质外链资源进行统一收纳、快速检索与健康监控。ResourceBridge 定位为轻量级的技术资源网关，解决的是资源链接散乱、失效不可知、复用困难这三类核心问题，适合与现有文档站点、内部知识库或自动化流程集成使用。

## 功能概览

- 批量资源导入与标准化清洗：支持从纯文本、CSV 或简单列表批量导入外链，自动完成 URL 规范化、去重与协议补全建议，减少人工整理成本。
- 实时可用性检测与状态标记：定时或手动触发链接存活检测，基于 HTTP 状态码与响应时间对资源进行健康分级（正常、可疑、失效），并生成可视化报告。
- 多级标签与业务域分类：允许为每个资源赋予多个自定义标签，支持按技术栈、项目阶段、文档类型或团队维度进行灵活归类，便于后续按场景筛选。
- 语义化全文检索：基于倒排索引与轻量级分词，支持对资源标题、描述、标签及来源域名进行快速检索，搜索结果可按相关度或更新时间排序。
- 外部引用关系追踪：记录每个资源被哪些内部文档或项目引用，支持反向查询，帮助评估单个外链的重要程度与影响范围。
- 资源变更历史审计：完整记录每次资源信息的增加、修改、删除与状态变更操作，保留操作人、时间与变更前后差异，满足团队协作与合规追溯需求。
- 开放数据导出与订阅：支持将资源列表导出为 JSON、Markdown 表格或 CSV 格式，同时允许通过 Webhook 订阅资源状态变更通知，便于与监控或消息系统对接。

## 应用场景

- 技术团队知识库外链治理：技术团队在日常开发中积累了数百个外部文档、API 参考、开源库地址与最佳实践文章。通过 ResourceBridge 可以统一纳管这些零散链接，定期检查可用性，并按照微服务、前端、运维等不同领域分类，显著降低知识碎片化带来的查找成本。
- 开源项目 README 与文档站资源同步：开源项目维护者常常在 README 中列出大量参考链接、教程或社区扩展。ResourceBridge 可以集中管理这些外链，并通过自动生成的 Markdown 资源列表快速更新到项目文档中，同时监控链接有效性，避免用户在阅读文档时遇到死链。
- 自动化报告与监控看板集成：运维或质量保障团队可以将 ResourceBridge 的可用性检测结果接入 Grafana 等可视化看板，按域名或标签维度展示资源健康趋势，当核心依赖文档或工具链地址出现异常时第一时间获得告警。
- 内容聚合网站的链接资产管理：技术博客、导航站或在线教程平台运营者可以使用 ResourceBridge 管理所有对外引用链接，借助标签系统实现动态分类页面生成，并通过变更历史追踪每个链接的添加和修改原因，提升内容维护的透明度和协作效率。

## 快速开始

以下步骤帮助你在本地环境快速启动 ResourceBridge 服务。

```bash
# 克隆代码仓库
git clone https://github.com/resourcebridge/resourcebridge.git
cd resourcebridge

# 安装项目依赖（使用 pip 与虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化默认配置文件与本地数据库
cp config.example.yaml config.yaml
python scripts/init_db.py

# 启动开发服务器
python app.py
```

服务默认监听 8000 端口，启动后可通过 http://localhost:8000 访问 Web 管理界面，或通过 API 进行资源管理操作。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Python | 3.9 及以上 | 核心运行环境，建议使用 3.10 或 3.11 以获得更好的性能与类型提示支持 |
| SQLite | 3.35 及以上 | 默认内嵌数据库，用于存储资源元数据、标签与审计日志，无需额外安装 |
| Redis | 6.0 及以上 | 可选组件，用于提升检测任务队列性能与缓存加速，生产环境建议配置 |
| requests | 2.28.0 及以上 | 处理所有对外 HTTP 检测请求，支持超时控制与重试策略 |
| PyYAML | 6.0 及以上 | 解析配置文件与资源导入导出时的 YAML 格式支持 |
| pytest | 7.0 及以上 | 仅开发与测试环境需要，用于运行单元测试与集成测试套件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 入门指南 | docs/quickstart.md | 如何从零开始部署 ResourceBridge，完成第一次资源导入和检测？ |
| 配置参考 | docs/configuration.md | 所有配置项的含义、默认值以及不同环境下的推荐调整策略是什么？ |
| API 手册 | docs/api_reference.md | 如何通过 RESTful API 进行资源的增删改查、批量操作与状态获取？ |
| 运维指南 | docs/operations.md | 如何配置定时检测任务、数据备份、日志轮转以及性能调优参数？ |

## 资源列表

- http://www.read.xwpxi.com/Article/28199.shtml
- http://www.read.xwpxi.com/Article/54919.shtml
- http://www.read.xwpxi.com/Article/383111.shtml
- http://www.read.xwpxi.com/Article/9903197.shtml
- http://www.read.xwpxi.com/Article/4550.shtml
- http://www.read.xwpxi.com/Article/2044342.shtml
- http://www.read.xwpxi.com/Article/3477502.shtml
- http://www.read.xwpxi.com/Article/258904.shtml
- http://www.read.xwpxi.com/Article/912941.shtml
- http://www.read.xwpxi.com/Article/772789.shtml
- http://www.read.xwpxi.com/Article/2401427.shtml
- http://www.read.xwpxi.com/Article/6694979.shtml
- http://www.read.xwpxi.com/Article/2808.shtml
- http://www.read.xwpxi.com/Article/5056.shtml
- http://www.read.xwpxi.com/Article/4780368.shtml
- http://www.read.xwpxi.com/Article/037599.shtml
- http://www.read.xwpxi.com/Article/9888.shtml
- http://www.read.xwpxi.com/Article/1870.shtml
- http://www.read.xwpxi.com/Article/390752.shtml
- http://www.read.xwpxi.com/Article/6714.shtml
- http://www.read.xwpxi.com/Article/5637106.shtml
- http://www.read.xwpxi.com/Article/0191.shtml
- http://www.read.xwpxi.com/Article/173114.shtml
- http://www.read.xwpxi.com/Article/939493.shtml
- http://www.read.xwpxi.com/Article/3534.shtml
- http://www.read.xwpxi.com/Article/2092.shtml
- http://www.read.xwpxi.com/Article/81298.shtml
- http://www.read.xwpxi.com/Article/533239.shtml
- http://www.read.xwpxi.com/Article/5500.shtml
- http://www.read.xwpxi.com/Article/1816.shtml
- http://www.read.xwpxi.com/Article/5387753.shtml
- http://www.read.xwpxi.com/Article/1685194.shtml
- http://www.read.xwpxi.com/Article/9732905.shtml
- http://www.read.xwpxi.com/Article/3132277.shtml
- http://www.read.xwpxi.com/Article/029753.shtml
- http://www.read.xwpxi.com/Article/9378370.shtml
- http://www.read.xwpxi.com/Article/4049.shtml
- http://www.read.xwpxi.com/Article/949971.shtml
- http://www.read.xwpxi.com/Article/8763469.shtml
- http://www.read.xwpxi.com/Article/0848.shtml
- http://www.read.xwpxi.com/Article/5313634.shtml
- http://www.read.xwpxi.com/Article/7788301.shtml
- http://www.read.xwpxi.com/Article/5798.shtml
- http://www.read.xwpxi.com/Article/0777980.shtml
- http://www.read.xwpxi.com/Article/4564830.shtml
- http://www.read.xwpxi.com/Article/84643.shtml
- http://www.read.xwpxi.com/Article/382559.shtml
- http://www.read.xwpxi.com/Article/242858.shtml
- http://www.read.xwpxi.com/Article/5240.shtml
- http://www.read.xwpxi.com/Article/678565.shtml
- http://www.read.xwpxi.com/Article/808660.shtml
- http://www.read.xwpxi.com/Article/8701.shtml
- http://www.read.xwpxi.com/Article/033732.shtml
- http://www.read.xwpxi.com/Article/292059.shtml
- http://www.read.xwpxi.com/Article/25866.shtml
- http://www.read.xwpxi.com/Article/5305404.shtml
- http://www.read.xwpxi.com/Article/427246.shtml
- http://www.read.xwpxi.com/Article/5142156.shtml
- http://www.read.xwpxi.com/Article/42919.shtml
- http://www.read.xwpxi.com/Article/11706.shtml
- http://www.read.xwpxi.com/Article/98721.shtml
- http://www.read.xwpxi.com/Article/005317.shtml
- http://www.read.xwpxi.com/Article/0159.shtml
- http://www.read.xwpxi.com/Article/54119.shtml
- http://www.read.xwpxi.com/Article/0737.shtml
- http://www.read.xwpxi.com/Article/18930.shtml
- http://www.read.xwpxi.com/Article/056849.shtml
- http://www.read.xwpxi.com/Article/7333691.shtml
- http://www.read.xwpxi.com/Article/0755525.shtml
- http://www.read.xwpxi.com/Article/9993015.shtml
- http://www.read.xwpxi.com/Article/9758.shtml
- http://www.read.xwpxi.com/Article/16811.shtml
- http://www.read.xwpxi.com/Article/36337.shtml
- http://www.read.xwpxi.com/Article/836748.shtml
- http://www.read.xwpxi.com/Article/7703.shtml
- http://www.read.xwpxi.com/Article/593587.shtml
- http://www.read.xwpxi.com/Article/93588.shtml
- http://www.read.xwpxi.com/Article/68263.shtml
- http://www.read.xwpxi.com/Article/76378.shtml
- http://www.read.xwpxi.com/Article/7826.shtml
- http://www.read.xwpxi.com/Article/3035.shtml
- http://www.read.xwpxi.com/Article/5543676.shtml
- http://www.read.xwpxi.com/Article/535299.shtml
- http://www.read.xwpxi.com/Article/781354.shtml
- http://www.read.xwpxi.com/Article/355118.shtml
- http://www.read.xwpxi.com/Article/1577601.shtml
- http://www.read.xwpxi.com/Article/96461.shtml
- http://www.read.xwpxi.com/Article/6796468.shtml
- http://www.read.xwpxi.com/Article/4780686.shtml
- http://www.read.xwpxi.com/Article/2035095.shtml
- http://www.read.xwpxi.com/Article/9417839.shtml
- http://www.read.xwpxi.com/Article/09183.shtml
- http://www.read.xwpxi.com/Article/2586.shtml
- http://www.read.xwpxi.com/Article/4894187.shtml
- http://www.read.xwpxi.com/Article/04533.shtml
- http://www.read.xwpxi.com/Article/31322.shtml
- http://www.read.xwpxi.com/Article/8134744.shtml
- http://www.read.xwpxi.com/Article/8682166.shtml
- http://www.read.xwpxi.com/Article/6767.shtml
- http://www.read.xwpxi.com/Article/4126050.shtml
- http://www.read.xwpxi.com/Article/8514694.shtml
- http://www.read.xwpxi.com/Article/804823.shtml
- http://www.read.xwpxi.com/Article/19313.shtml
- http://www.read.xwpxi.com/Article/8922658.shtml
- http://www.read.xwpxi.com/Article/6456556.shtml
- http://www.read.xwpxi.com/Article/103329.shtml
- http://www.read.xwpxi.com/Article/32606.shtml
- http://www.read.xwpxi.com/Article/1466014.shtml
- http://www.read.xwpxi.com/Article/96997.shtml
- http://www.read.xwpxi.com/Article/194182.shtml
- http://www.read.xwpxi.com/Article/23479.shtml
- http://www.read.xwpxi.com/Article/73510.shtml
- http://www.read.xwpxi.com/Article/771808.shtml
- http://www.read.xwpxi.com/Article/27367.shtml
- http://www.read.xwpxi.com/Article/7090.shtml
- http://www.read.xwpxi.com/Article/2495781.shtml
- http://www.read.xwpxi.com/Article/204340.shtml
- http://www.read.xwpxi.com/Article/6033229.shtml
- http://www.read.xwpxi.com/Article/40436.shtml
- http://www.read.xwpxi.com/Article/9211459.shtml
- http://www.read.xwpxi.com/Article/142867.shtml
- http://www.read.xwpxi.com/Article/7715743.shtml
- http://www.read.xwpxi.com/Article/82236.shtml
- http://www.read.xwpxi.com/Article/040409.shtml
- http://www.read.xwpxi.com/Article/193064.shtml
- http://www.read.xwpxi.com/Article/1733.shtml
- http://www.read.xwpxi.com/Article/61891.shtml
- http://www.read.xwpxi.com/Article/426644.shtml
- http://www.read.xwpxi.com/Article/06087.shtml
- http://www.read.xwpxi.com/Article/941753.shtml
- http://www.read.xwpxi.com/Article/282755.shtml
- http://www.read.xwpxi.com/Article/5942.shtml
- http://www.read.xwpxi.com/Article/846125.shtml
- http://www.read.xwpxi.com/Article/7161.shtml
- http://www.read.xwpxi.com/Article/08973.shtml
- http://www.read.xwpxi.com/Article/419927.shtml
- http://www.read.xwpxi.com/Article/9592245.shtml
- http://www.read.xwpxi.com/Article/11638.shtml
- http://www.read.xwpxi.com/Article/0482.shtml
- http://www.read.xwpxi.com/Article/9878872.shtml
- http://www.read.xwpxi.com/Article/91141.shtml
- http://www.read.xwpxi.com/Article/63177.shtml
- http://www.read.xwpxi.com/Article/2458.shtml
- http://www.read.xwpxi.com/Article/36413.shtml
- http://www.read.xwpxi.com/Article/70866.shtml
- http://www.read.xwpxi.com/Article/281908.shtml
- http://www.read.xwpxi.com/Article/9242.shtml
- http://www.read.xwpxi.com/Article/9303.shtml
- http://www.read.xwpxi.com/Article/1541054.shtml
- http://www.read.xwpxi.com/Article/29561.shtml
- http://www.read.xwpxi.com/Article/815051.shtml
- http://www.read.xwpxi.com/Article/8414583.shtml
- http://www.read.xwpxi.com/Article/8573746.shtml
- http://www.read.xwpxi.com/Article/1681304.shtml
- http://www.read.xwpxi.com/Article/83899.shtml
- http://www.read.xwpxi.com/Article/5008.shtml
- http://www.read.xwpxi.com/Article/592415.shtml
- http://www.read.xwpxi.com/Article/0897.shtml
- http://www.read.xwpxi.com/Article/7595.shtml
- http://www.read.xwpxi.com/Article/0729736.shtml
- http://www.read.xwpxi.com/Article/841760.shtml
- http://www.read.xwpxi.com/Article/020292.shtml
- http://www.read.xwpxi.com/Article/36997.shtml
- http://www.read.xwpxi.com/Article/1798169.shtml
- http://www.read.xwpxi.com/Article/5941012.shtml
- http://www.read.xwpxi.com/Article/2601.shtml
- http://www.read.xwpxi.com/Article/579596.shtml
- http://www.read.xwpxi.com/Article/140005.shtml
- http://www.read.xwpxi.com/Article/9240216.shtml
- http://www.read.xwpxi.com/Article/2872.shtml
- http://www.read.xwpxi.com/Article/49132.shtml
- http://www.read.xwpxi.com/Article/9621.shtml
- http://www.read.xwpxi.com/Article/3758197.shtml
- http://www.read.xwpxi.com/Article/510260.shtml
- http://www.read.xwpxi.com/Article/1378.shtml
- http://www.read.xwpxi.com/Article/8018.shtml
- http://www.read.xwpxi.com/Article/454589.shtml
- http://www.read.xwpxi.com/Article/976527.shtml
- http://www.read.xwpxi.com/Article/9151222.shtml
- http://www.read.xwpxi.com/Article/1842044.shtml
- http://www.read.xwpxi.com/Article/2964199.shtml
- http://www.read.xwpxi.com/Article/629427.shtml
- http://www.read.xwpxi.com/Article/163483.shtml
- http://www.read.xwpxi.com/Article/966631.shtml
- http://www.read.xwpxi.com/Article/0814.shtml
- http://www.read.xwpxi.com/Article/3180268.shtml
- http://www.read.xwpxi.com/Article/44141.shtml
- http://www.read.xwpxi.com/Article/467988.shtml
- http://www.read.xwpxi.com/Article/62959.shtml
- http://www.read.xwpxi.com/Article/8981028.shtml
- http://www.read.xwpxi.com/Article/170200.shtml
- http://www.read.xwpxi.com/Article/4902.shtml
- http://www.read.xwpxi.com/Article/4158.shtml
- http://www.read.xwpxi.com/Article/8359809.shtml
- http://www.read.xwpxi.com/Article/0240.shtml
- http://www.read.xwpxi.com/Article/8412.shtml
- http://www.read.xwpxi.com/Article/89006.shtml
- http://www.read.xwpxi.com/Article/357662.shtml
- http://www.read.xwpxi.com/Article/81460.shtml
- http://www.read.xwpxi.com/Article/86255.shtml
- http://www.read.xwpxi.com/Article/68090.shtml
- http://www.read.xwpxi.com/Article/43329.shtml
- http://www.read.xwpxi.com/Article/911724.shtml
- http://www.read.xwpxi.com/Article/2166752.shtml
- http://www.read.xwpxi.com/Article/6010144.shtml
- http://www.read.xwpxi.com/Article/9183667.shtml
- http://www.read.xwpxi.com/Article/2921.shtml
- http://www.read.xwpxi.com/Article/44416.shtml
- http://www.read.xwpxi.com/Article/1828.shtml
- http://www.read.xwpxi.com/Article/578753.shtml
- http://www.read.xwpxi.com/Article/134572.shtml
- http://www.read.xwpxi.com/Article/63782.shtml
- http://www.read.xwpxi.com/Article/7256848.shtml
- http://www.read.xwpxi.com/Article/9872069.shtml
- http://www.read.xwpxi.com/Article/8507.shtml
- http://www.read.xwpxi.com/Article/7752.shtml
- http://www.read.xwpxi.com/Article/540422.shtml
- http://www.read.xwpxi.com/Article/1825.shtml
- http://www.read.xwpxi.com/Article/02520.shtml
- http://www.read.xwpxi.com/Article/819169.shtml
- http://www.read.xwpxi.com/Article/6399.shtml
- http://www.read.xwpxi.com/Article/3160045.shtml
- http://www.read.xwpxi.com/Article/846486.shtml
- http://www.read.xwpxi.com/Article/5819.shtml
- http://www.read.xwpxi.com/Article/8046.shtml
- http://www.read.xwpxi.com/Article/7686660.shtml
- http://www.read.xwpxi.com/Article/1026045.shtml
- http://www.read.xwpxi.com/Article/69678.shtml
- http://www.read.xwpxi.com/Article/9376588.shtml
- http://www.read.xwpxi.com/Article/9054.shtml
- http://www.read.xwpxi.com/Article/216358.shtml
- http://www.read.xwpxi.com/Article/9240.shtml
- http://www.read.xwpxi.com/Article/1241650.shtml
- http://www.read.xwpxi.com/Article/08117.shtml
- http://www.read.xwpxi.com/Article/98326.shtml
- http://www.read.xwpxi.com/Article/55552.shtml
- http://www.read.xwpxi.com/Article/039937.shtml
- http://www.read.xwpxi.com/Article/785520.shtml
- http://www.read.xwpxi.com/Article/1956.shtml
- http://www.read.xwpxi.com/Article/8539288.shtml
- http://www.read.xwpxi.com/Article/873528.shtml
- http://www.read.xwpxi.com/Article/27440.shtml
- http://www.read.xwpxi.com/Article/4968302.shtml
- http://www.read.xwpxi.com/Article/3046.shtml
- http://www.read.xwpxi.com/Article/5992.shtml
- http://www.read.xwpxi.com/Article/0559739.shtml
- http://www.read.xwpxi.com/Article/3011549.shtml
- http://www.read.xwpxi.com/Article/21739.shtml
- http://www.read.xwpxi.com/Article/45929.shtml
- http://www.read.xwpxi.com/Article/73681.shtml

## 项目结构

```
resourcebridge/
├── app/                            # 核心应用模块
│   ├── api/                        # RESTful API 路由与请求处理
│   │   ├── v1/                     # API 版本 v1 实现
│   │   │   ├── resources.py        # 资源增删改查接口
│   │   │   └── health.py           # 可用性检测与状态查询接口
│   │   └── middleware.py           # 请求日志、跨域与认证中间件
│   ├── core/                       # 核心业务逻辑与领域模型
│   │   ├── models.py               # 数据模型定义（资源、标签、审计）
│   │   ├── checker.py              # 链接存活检测引擎
│   │   └── indexer.py              # 标签索引与全文检索构建器
│   ├── services/                   # 外部服务与基础设施集成
│   │   ├── database.py             # 数据库连接池与事务管理
│   │   ├── redis_client.py         # Redis 缓存与任务队列客户端
│   │   └── webhook.py              # 订阅通知与回调分发服务
│   ├── utils/                      # 通用工具函数与辅助类
│   │   ├── url_normalizer.py       # URL 清洗、协议补全与去重工具
│   │   ├── validators.py           # 输入参数校验与类型检查
│   │   └── exporters.py            # 资源列表导出为 JSON、CSV、Markdown
│   └── config.py                   # 配置加载与合并逻辑
├── scripts/                        # 运维与开发辅助脚本
│   ├── init_db.py                  # 初始化数据库表结构与默认配置
│   ├── import_batch.py             # 批量导入资源列表（支持纯文本/CSV）
│   └── run_health_check.py         # 手动触发全量可用性检测
├── tests/                          # 单元测试与集成测试目录
│   ├── unit/                       # 针对核心函数与工具类的单元测试
│   └── integration/                # 针对 API 与数据库交互的集成测试
├── docs/                           # 项目文档源码（Markdown 格式）
│   ├── quickstart.md               # 快速入门指南
│   ├── configuration.md            # 详细配置说明
│   ├── api_reference.md            # API 端点完整参考
│   └── operations.md               # 生产环境运维手册
├── web/                            # 内置 Web 管理界面（可选组件）
│   ├── static/                     # CSS、JavaScript 与图片资源
│   └── templates/                  # Jinja2 模板文件
├── config.yaml.example             # 配置文件示例，包含所有可调参数
├── requirements.txt                # Python 依赖列表（固定版本）
├── app.py                          # 应用入口文件，启动 Flask 开发服务器
└── README.md                       # 项目说明文档（当前文件）
```

## 贡献指南

1. 阅读项目行为准则与贡献者协议，确保遵守开源社区基本规范。所有贡献者需签署轻量级开发者原创声明，保证所提交代码未侵犯第三方权益。
2. 在 GitHub Issue 列表中查找或新建与你的改动相关的任务，并等待项目维护者确认需求或缺陷的有效性。建议先通过 Issue 讨论设计方案，避免大量无效代码提交。
3. Fork 主仓库至个人账户，创建以功能或修复命名的分支（例如 feature/batch-import-optimization 或 fix/checker-timeout），并在该分支上进行开发。
4. 编写或更新对应的单元测试与集成测试，确保所有测试用例通过。新增功能需包含足够的测试覆盖，修复缺陷需添加回归测试用例。
5. 提交 Pull Request 至主仓库的 develop 分支，在描述中清晰关联对应的 Issue 编号，并列举主要改动点与测试结果摘要。等待至少一位维护者进行代码评审与合并。

## 常见问题

Q: 资源检测任务对目标服务器是否会造成较大压力？

A: ResourceBridge 默认采用并发度可配置的检测策略，默认并发数为 10，且每个请求均设置 5 秒超时与 3 次重试间隔递增。对于大规模资源列表，建议在配置文件中调整检测间隔与并发数，或仅在非高峰时段执行全量检测。此外，检测引擎遵循 robots.txt 规则，不对目标站点发起频繁或高流量请求。

Q: 项目是否支持从现有书签或导航站迁移数据？

A: 当前版本支持从纯文本列表（每行一个 URL）和标准 CSV 文件（需包含 url、title、description 列）进行批量导入。未来版本计划增加对浏览器书签 HTML 导出格式和主流导航站数据格式的直接解析支持。如需从其他特定系统迁移，可参考 API 手册中的批量写入接口进行二次开发。

Q: 如何确保资源列表的导出格式与不同文档站点兼容？

A: 导出模块目前支持 Markdown 无序列表、CSV 和 JSON 三种通用格式。其中 Markdown 导出严格遵循每行单个 URL 的格式要求，并保留原始协议与域名，适合直接粘贴至 README 或技术文档中。对于更复杂的布局需求，建议使用 JSON 导出后自行通过模板引擎渲染。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
