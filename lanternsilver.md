# LinkPilot

LinkPilot 是一个面向技术社区与内容创作者的轻量级外链资源聚合与导航系统。该项目旨在解决个人或团队在维护大量外部文章、文档、工具站及参考链接时面临的分类混乱、检索低效与重复劳动问题。LinkPilot 定位于中大型技术文档库的辅助基础设施，可作为静态站点生成器的数据源，也可嵌入现有 CMS 或知识管理平台，实现对零散 URL 资源的集中化梳理与稳定输出。目标用户包括开源项目维护者、技术博主、在线教育机构以及企业内部知识库管理员。

## 功能概览

- 批量导入与自动去重：支持从 CSV、JSON 或纯文本列表批量导入 URL，自动检测并合并重复条目，保留最早添加时间与最高优先级标签。
- 智能分类与标签系统：基于 URL 路径、域名及可自定义的正则规则，对链接进行自动打标与分类，支持层级标签（如 programming/python/web）。
- 链接可用性健康检查：内置异步 HTTP 探测模块，定期检查每个资源链接的可访问状态与响应时间，自动标记失效或重定向链接。
- 全文元数据提取：自动抓取目标页面的标题、描述、关键词及主要图片，生成摘要卡片，支持手动编辑修正。
- 多格式数据导出：支持导出为 Markdown 表格、JSON API、RSS 订阅源及静态 HTML 目录页，便于与其他工具链集成。
- 权限与协作管理：提供基于角色的访问控制（管理员、编辑者、只读用户），支持操作日志审计，适合团队共同维护资源库。
- 自定义视图与检索：提供高级筛选器（按域名、标签、更新时间、健康状态），并支持全文模糊搜索与正则表达式精确匹配。

## 应用场景

- 技术文档站的外链附录管理：技术书籍或大型项目文档往往需要引用数百篇外部文章。LinkPilot 可为每篇文档生成独立的引用链接列表，自动检查链接有效性，避免出版物中出现死链。
- 企业 onboarding 知识包整理：新员工入职需要阅读大量内部与外部资料。团队可使用 LinkPilot 快速建立按岗位分类的阅读清单，并通过健康检查确保所有资源在培训期间可访问。
- 开源项目学习路线图配套：开源社区维护者可利用 LinkPilot 整理从入门到进阶的教程、视频与示例项目链接，按阶段分类，并通过导出功能生成 README 或官网的学习资源章节。
- 个人知识库的素材缓存层：结合 Obsidian 或 Notion 等工具，LinkPilot 可作为中间层，集中存放所有待阅读或已归档的文章链接，并提供元数据检索，避免浏览器书签的混乱。

## 快速开始

以下步骤帮助您在本地环境中快速启动 LinkPilot 服务。

```bash
# 克隆项目仓库
git clone https://github.com/linkpilot/linkpilot.git
cd linkpilot

# 安装依赖（使用 pip 和虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化数据库并创建管理员账户
python manage.py init_db
python manage.py create_admin --username admin --password your_secure_password

# 运行开发服务器
python manage.py runserver --host 0.0.0.0 --port 8080
```

访问 `http://localhost:8080` 即可进入仪表盘。首次启动将自动创建示例数据分类供测试。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，推荐使用 3.11 以获得更好性能 |
| SQLite | 3.35 及以上 | 默认内置数据库，用于元数据与索引存储，生产环境可切换至 PostgreSQL |
| Redis | 6.0 及以上 | 可选，用于缓存健康检查结果与加速频繁查询，非必需但强烈推荐 |
| Node.js | 18.0 及以上 | 仅用于前端静态资源构建，若使用预编译包则无需安装 |
| Nginx | 1.18 及以上 | 生产环境反向代理推荐，用于提供静态文件与负载均衡 |
| 系统内存 | 512 MB 以上 | 不含浏览器前端占用，实际运行建议 1 GB 以上 |
| 磁盘空间 | 1 GB 以上 | 用于存储 SQLite 数据库及抓取的内容摘要缓存 |
| 网络环境 | 外网可访问 | 用于链接健康检查的 HTTP 探测，内网部署可配置代理 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/quickstart.md | 如何安装、配置首次启动、添加第一批链接？ |
| 操作手册 | docs/usage.md | 如何进行批量导入、分类管理、健康检查调度？ |
| 集成指南 | docs/integration.md | 如何通过 API 导出数据、嵌入 iframe 或生成静态站点？ |
| 运维参考 | docs/operations.md | 如何备份数据库、迁移至 PostgreSQL、配置邮件报警？ |

## 资源列表

- http://www.read.rswzr.com/Article/118547.shtml
- http://www.read.rswzr.com/Article/056546.shtml
- http://www.read.rswzr.com/Article/2518.shtml
- http://www.read.rswzr.com/Article/48503.shtml
- http://www.read.rswzr.com/Article/476482.shtml
- http://www.read.rswzr.com/Article/31479.shtml
- http://www.read.rswzr.com/Article/1051262.shtml
- http://www.read.rswzr.com/Article/64883.shtml
- http://www.read.rswzr.com/Article/8771.shtml
- http://www.read.rswzr.com/Article/811530.shtml
- http://www.read.rswzr.com/Article/042015.shtml
- http://www.read.rswzr.com/Article/74696.shtml
- http://www.read.rswzr.com/Article/0344193.shtml
- http://www.read.rswzr.com/Article/41437.shtml
- http://www.read.rswzr.com/Article/377417.shtml
- http://www.read.rswzr.com/Article/7453.shtml
- http://www.read.rswzr.com/Article/2301.shtml
- http://www.read.rswzr.com/Article/018351.shtml
- http://www.read.rswzr.com/Article/4544.shtml
- http://www.read.rswzr.com/Article/2201.shtml
- http://www.read.rswzr.com/Article/090351.shtml
- http://www.read.rswzr.com/Article/8318.shtml
- http://www.read.rswzr.com/Article/2077158.shtml
- http://www.read.rswzr.com/Article/3265.shtml
- http://www.read.rswzr.com/Article/7982957.shtml
- http://www.read.rswzr.com/Article/3908.shtml
- http://www.read.rswzr.com/Article/1900747.shtml
- http://www.read.rswzr.com/Article/8073129.shtml
- http://www.read.rswzr.com/Article/01487.shtml
- http://www.read.rswzr.com/Article/6862.shtml
- http://www.read.rswzr.com/Article/2596549.shtml
- http://www.read.rswzr.com/Article/4972.shtml
- http://www.read.rswzr.com/Article/588303.shtml
- http://www.read.rswzr.com/Article/4772587.shtml
- http://www.read.rswzr.com/Article/83821.shtml
- http://www.read.rswzr.com/Article/8532149.shtml
- http://www.read.rswzr.com/Article/5982226.shtml
- http://www.read.rswzr.com/Article/5086.shtml
- http://www.read.rswzr.com/Article/974461.shtml
- http://www.read.rswzr.com/Article/630227.shtml
- http://www.read.rswzr.com/Article/278384.shtml
- http://www.read.rswzr.com/Article/9971.shtml
- http://www.read.rswzr.com/Article/973240.shtml
- http://www.read.rswzr.com/Article/90055.shtml
- http://www.read.rswzr.com/Article/2088559.shtml
- http://www.read.rswzr.com/Article/1745.shtml
- http://www.read.rswzr.com/Article/7012701.shtml
- http://www.read.rswzr.com/Article/9093.shtml
- http://www.read.rswzr.com/Article/8466499.shtml
- http://www.read.rswzr.com/Article/2128.shtml
- http://www.read.rswzr.com/Article/9739364.shtml
- http://www.read.rswzr.com/Article/1632.shtml
- http://www.read.rswzr.com/Article/6469.shtml
- http://www.read.rswzr.com/Article/9720289.shtml
- http://www.read.rswzr.com/Article/4908020.shtml
- http://www.read.rswzr.com/Article/900798.shtml
- http://www.read.rswzr.com/Article/640981.shtml
- http://www.read.rswzr.com/Article/5455807.shtml
- http://www.read.rswzr.com/Article/0358.shtml
- http://www.read.rswzr.com/Article/014561.shtml
- http://www.read.rswzr.com/Article/281112.shtml
- http://www.read.rswzr.com/Article/5522.shtml
- http://www.read.rswzr.com/Article/1474111.shtml
- http://www.read.rswzr.com/Article/7999305.shtml
- http://www.read.rswzr.com/Article/451776.shtml
- http://www.read.rswzr.com/Article/8098.shtml
- http://www.read.rswzr.com/Article/583349.shtml
- http://www.read.rswzr.com/Article/6335.shtml
- http://www.read.rswzr.com/Article/5986.shtml
- http://www.read.rswzr.com/Article/8201075.shtml
- http://www.read.rswzr.com/Article/163549.shtml
- http://www.read.rswzr.com/Article/58256.shtml
- http://www.read.rswzr.com/Article/411099.shtml
- http://www.read.rswzr.com/Article/907174.shtml
- http://www.read.rswzr.com/Article/0848855.shtml
- http://www.read.rswzr.com/Article/699866.shtml
- http://www.read.rswzr.com/Article/2040.shtml
- http://www.read.rswzr.com/Article/1373869.shtml
- http://www.read.rswzr.com/Article/6667.shtml
- http://www.read.rswzr.com/Article/5123739.shtml
- http://www.read.rswzr.com/Article/9799.shtml
- http://www.read.rswzr.com/Article/8288618.shtml
- http://www.read.rswzr.com/Article/5032.shtml
- http://www.read.rswzr.com/Article/2988057.shtml
- http://www.read.rswzr.com/Article/4298600.shtml
- http://www.read.rswzr.com/Article/163643.shtml
- http://www.read.rswzr.com/Article/423492.shtml
- http://www.read.rswzr.com/Article/33734.shtml
- http://www.read.rswzr.com/Article/7779768.shtml
- http://www.read.rswzr.com/Article/1819.shtml
- http://www.read.rswzr.com/Article/656087.shtml
- http://www.read.rswzr.com/Article/474019.shtml
- http://www.read.rswzr.com/Article/960532.shtml
- http://www.read.rswzr.com/Article/2824.shtml
- http://www.read.rswzr.com/Article/7698869.shtml
- http://www.read.rswzr.com/Article/7668388.shtml
- http://www.read.rswzr.com/Article/4295475.shtml
- http://www.read.rswzr.com/Article/0468.shtml
- http://www.read.rswzr.com/Article/82652.shtml
- http://www.read.rswzr.com/Article/0506115.shtml
- http://www.read.rswzr.com/Article/6728252.shtml
- http://www.read.rswzr.com/Article/258751.shtml
- http://www.read.rswzr.com/Article/895904.shtml
- http://www.read.rswzr.com/Article/1600630.shtml
- http://www.read.rswzr.com/Article/8562089.shtml
- http://www.read.rswzr.com/Article/0484.shtml
- http://www.read.rswzr.com/Article/4626.shtml
- http://www.read.rswzr.com/Article/171261.shtml
- http://www.read.rswzr.com/Article/832724.shtml
- http://www.read.rswzr.com/Article/171256.shtml
- http://www.read.rswzr.com/Article/456855.shtml
- http://www.read.rswzr.com/Article/6551820.shtml
- http://www.read.rswzr.com/Article/0508.shtml
- http://www.read.rswzr.com/Article/586209.shtml
- http://www.read.rswzr.com/Article/07988.shtml
- http://www.read.rswzr.com/Article/74159.shtml
- http://www.read.rswzr.com/Article/7690687.shtml
- http://www.read.rswzr.com/Article/5171.shtml
- http://www.read.rswzr.com/Article/6910876.shtml
- http://www.read.rswzr.com/Article/5980998.shtml
- http://www.read.rswzr.com/Article/17262.shtml
- http://www.read.rswzr.com/Article/97434.shtml
- http://www.read.rswzr.com/Article/2541534.shtml
- http://www.read.rswzr.com/Article/9802194.shtml
- http://www.read.rswzr.com/Article/9911949.shtml
- http://www.read.rswzr.com/Article/484305.shtml
- http://www.read.rswzr.com/Article/652725.shtml
- http://www.read.rswzr.com/Article/256000.shtml
- http://www.read.rswzr.com/Article/176848.shtml
- http://www.read.rswzr.com/Article/656986.shtml
- http://www.read.rswzr.com/Article/3559753.shtml
- http://www.read.rswzr.com/Article/93560.shtml
- http://www.read.rswzr.com/Article/711341.shtml
- http://www.read.rswzr.com/Article/25961.shtml
- http://www.read.rswzr.com/Article/0750.shtml
- http://www.read.rswzr.com/Article/583941.shtml
- http://www.read.rswzr.com/Article/521478.shtml
- http://www.read.rswzr.com/Article/400487.shtml
- http://www.read.rswzr.com/Article/130502.shtml
- http://www.read.rswzr.com/Article/4944141.shtml
- http://www.read.rswzr.com/Article/057837.shtml
- http://www.read.rswzr.com/Article/548031.shtml
- http://www.read.rswzr.com/Article/8703.shtml
- http://www.read.rswzr.com/Article/407180.shtml
- http://www.read.rswzr.com/Article/0691.shtml
- http://www.read.rswzr.com/Article/5350.shtml
- http://www.read.rswzr.com/Article/0326.shtml
- http://www.read.rswzr.com/Article/8581615.shtml
- http://www.read.rswzr.com/Article/5050.shtml
- http://www.read.rswzr.com/Article/4695877.shtml
- http://www.read.rswzr.com/Article/27368.shtml
- http://www.read.rswzr.com/Article/1174.shtml
- http://www.read.rswzr.com/Article/28598.shtml
- http://www.read.rswzr.com/Article/9993472.shtml
- http://www.read.rswzr.com/Article/81048.shtml
- http://www.read.rswzr.com/Article/251018.shtml
- http://www.read.rswzr.com/Article/80738.shtml
- http://www.read.rswzr.com/Article/8861854.shtml
- http://www.read.rswzr.com/Article/430672.shtml
- http://www.read.rswzr.com/Article/1412871.shtml
- http://www.read.rswzr.com/Article/1227313.shtml
- http://www.read.rswzr.com/Article/5940657.shtml
- http://www.read.rswzr.com/Article/980364.shtml
- http://www.read.rswzr.com/Article/4580.shtml
- http://www.read.rswzr.com/Article/50165.shtml
- http://www.read.rswzr.com/Article/7630.shtml
- http://www.read.rswzr.com/Article/5082.shtml
- http://www.read.rswzr.com/Article/3750899.shtml
- http://www.read.rswzr.com/Article/1112.shtml
- http://www.read.rswzr.com/Article/87628.shtml
- http://www.read.rswzr.com/Article/1708474.shtml
- http://www.read.rswzr.com/Article/13794.shtml
- http://www.read.rswzr.com/Article/745288.shtml
- http://www.read.rswzr.com/Article/014770.shtml
- http://www.read.rswzr.com/Article/7548819.shtml
- http://www.read.rswzr.com/Article/5112.shtml
- http://www.read.rswzr.com/Article/74088.shtml
- http://www.read.rswzr.com/Article/29063.shtml
- http://www.read.rswzr.com/Article/7538.shtml
- http://www.read.rswzr.com/Article/0593.shtml
- http://www.read.rswzr.com/Article/14305.shtml
- http://www.read.rswzr.com/Article/6211.shtml
- http://www.read.rswzr.com/Article/46342.shtml
- http://www.read.rswzr.com/Article/4417407.shtml
- http://www.read.rswzr.com/Article/961264.shtml
- http://www.read.rswzr.com/Article/6498.shtml
- http://www.read.rswzr.com/Article/752367.shtml
- http://www.read.rswzr.com/Article/9330450.shtml
- http://www.read.rswzr.com/Article/4939041.shtml
- http://www.read.rswzr.com/Article/4001970.shtml
- http://www.read.rswzr.com/Article/534728.shtml
- http://www.read.rswzr.com/Article/1071169.shtml
- http://www.read.rswzr.com/Article/78505.shtml
- http://www.read.rswzr.com/Article/3108141.shtml
- http://www.read.rswzr.com/Article/36249.shtml
- http://www.read.rswzr.com/Article/1343.shtml
- http://www.read.rswzr.com/Article/807538.shtml
- http://www.read.rswzr.com/Article/27957.shtml
- http://www.read.rswzr.com/Article/987269.shtml
- http://www.read.rswzr.com/Article/5227158.shtml
- http://www.read.rswzr.com/Article/5774.shtml
- http://www.read.rswzr.com/Article/8841989.shtml
- http://www.read.rswzr.com/Article/8886069.shtml
- http://www.read.rswzr.com/Article/0991205.shtml
- http://www.read.rswzr.com/Article/569425.shtml
- http://www.read.rswzr.com/Article/189736.shtml
- http://www.read.rswzr.com/Article/015915.shtml
- http://www.read.rswzr.com/Article/165178.shtml
- http://www.read.rswzr.com/Article/66643.shtml
- http://www.read.rswzr.com/Article/7943.shtml
- http://www.read.rswzr.com/Article/2561073.shtml
- http://www.read.rswzr.com/Article/39836.shtml
- http://www.read.rswzr.com/Article/8563.shtml
- http://www.read.rswzr.com/Article/8620.shtml
- http://www.read.rswzr.com/Article/9364.shtml
- http://www.read.rswzr.com/Article/9255143.shtml
- http://www.read.rswzr.com/Article/906342.shtml
- http://www.read.rswzr.com/Article/8652490.shtml
- http://www.read.rswzr.com/Article/9090487.shtml
- http://www.read.rswzr.com/Article/588345.shtml
- http://www.read.rswzr.com/Article/6421579.shtml
- http://www.read.rswzr.com/Article/6477.shtml
- http://www.read.rswzr.com/Article/86888.shtml
- http://www.read.rswzr.com/Article/9619.shtml
- http://www.read.rswzr.com/Article/7385896.shtml
- http://www.read.rswzr.com/Article/1877994.shtml
- http://www.read.rswzr.com/Article/685214.shtml
- http://www.read.rswzr.com/Article/02980.shtml
- http://www.read.rswzr.com/Article/477785.shtml
- http://www.read.rswzr.com/Article/1395.shtml
- http://www.read.rswzr.com/Article/002055.shtml
- http://www.read.rswzr.com/Article/080179.shtml
- http://www.read.rswzr.com/Article/695256.shtml
- http://www.read.rswzr.com/Article/7770.shtml
- http://www.read.rswzr.com/Article/7228.shtml
- http://www.read.rswzr.com/Article/52967.shtml
- http://www.read.rswzr.com/Article/463311.shtml
- http://www.read.rswzr.com/Article/9048061.shtml
- http://www.read.rswzr.com/Article/44682.shtml
- http://www.read.rswzr.com/Article/840517.shtml
- http://www.read.rswzr.com/Article/6060.shtml
- http://www.read.rswzr.com/Article/398899.shtml
- http://www.read.rswzr.com/Article/031282.shtml
- http://www.read.rswzr.com/Article/9425.shtml
- http://www.read.rswzr.com/Article/1487766.shtml
- http://www.read.rswzr.com/Article/6620124.shtml
- http://www.read.rswzr.com/Article/2702.shtml
- http://www.read.rswzr.com/Article/5302643.shtml
- http://www.read.rswzr.com/Article/3467.shtml
- http://www.read.rswzr.com/Article/3090.shtml

## 项目结构

```
linkpilot/
├── app/
│   ├── api/                        # RESTful API 路由层
│   │   ├── v1/                     # API 版本 v1 端点
│   │   │   ├── links.py            # 链接资源的增删改查与批量操作
│   │   │   ├── health.py           # 健康检查触发与状态查询
│   │   │   └── export.py           # 导出任务生成与下载
│   │   └── __init__.py
│   ├── core/                       # 核心业务逻辑与数据模型
│   │   ├── models/                 # SQLAlchemy ORM 模型定义
│   │   │   ├── link.py             # 链接实体与标签关联
│   │   │   ├── category.py         # 分类树结构
│   │   │   └── user.py             # 用户与权限表
│   │   ├── scanner/                # 元数据抓取与解析模块
│   │   │   ├── fetcher.py          # 异步 HTTP 请求与重试策略
│   │   │   └── parser.py           # HTML 标题/描述提取（基于 lxml）
│   │   └── checker/                # 链接可用性探测子模块
│   │       ├── probe.py            # TCP/HTTP 探测实现
│   │       └── scheduler.py        # 周期性任务调度（APScheduler）
│   ├── web/                        # 仪表盘 Web 界面
│   │   ├── templates/              # Jinja2 模板文件
│   │   │   ├── dashboard.html      # 主数据面板
│   │   │   └── detail.html         # 链接详情视图
│   │   └── static/                 # 压缩后的 CSS/JS 资源
│   └── utils/                      # 通用工具函数
│       ├── validators.py           # URL 校验与规范化
│       └── logger.py               # 结构化日志配置（JSON 格式）
├── config/                         # 环境配置
│   ├── development.py              # 开发环境参数（debug 开启）
│   ├── production.py               # 生产环境参数（关闭调试、启用缓存）
│   └── test.py                     # 单元测试配置
├── tests/                          # 单元测试与集成测试
│   ├── test_models/                # 数据模型测试
│   └── test_api/                   # API 端点测试（pytest + flask_testing）
├── scripts/                        # 运维辅助脚本
│   ├── init_db.py                  # 数据库初始化与种子数据
│   └── export_static.py            # 生成静态 HTML 目录页
├── requirements.txt                # Python 依赖列表（固定版本）
├── Dockerfile                      # 容器构建定义（基于 python:3.11-slim）
├── docker-compose.yml              # 本地编排（含 Redis 与 Nginx）
└── README.md                       # 项目说明文档（本文件）
```

## 贡献指南

1. 阅读项目行为准则（CODE_OF_CONDUCT.md）并在提交前签署贡献者许可协议（CLA）。
2. 在 GitHub Issues 中查找标记为 `good-first-issue` 或 `help-wanted` 的任务，或新建 Issue 描述您要解决的问题。
3. Fork 项目仓库，在本地新建功能分支（feature/xxx 或 fix/xxx），保持分支名称简洁明了。
4. 编写代码时请遵循 PEP 8 风格规范，并为新增功能或修复编写对应的单元测试，测试覆盖率不低于 85%。
5. 提交前运行 `make lint` 与 `make test` 确保所有检查通过，然后推送分支并创建 Pull Request，描述中需关联相关 Issue 编号。

## 常见问题

**问：导入大量 URL 时页面卡顿或超时怎么办？**

答：LinkPilot 默认使用同步导入处理少量链接（少于 100 条）。对于大批量导入（超过 500 条），建议使用命令行工具 `python manage.py import_bulk --file links.csv --async`，该模式将任务推入后台队列，并返回任务 ID 供查询进度。您也可以通过增加 Redis 队列 worker 数量来并行处理。

**问：健康检查显示链接失效，但浏览器访问正常？**

答：这通常是由于目标网站配置了反爬机制或要求特定的 User-Agent 头。您可以在配置文件中调整 `CHECKER_USER_AGENT` 为常见浏览器字符串，并启用 `CHECKER_VERIFY_SSL=False` 忽略证书问题。若仍失败，可手动将链接标记为“忽略检查”，该状态将覆盖自动探测结果。

**问：如何从旧版 SQLite 迁移到 PostgreSQL？**

答：项目内置迁移脚本 `scripts/migrate_to_pg.py`。您需要在配置中设置 `SQLALCHEMY_DATABASE_URI` 指向 PostgreSQL 目标库，然后运行迁移脚本。该过程将自动转换表结构与索引，并保留所有元数据与标签关系。建议在低峰期执行，并在执行前使用 `--dry-run` 参数进行预检。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
