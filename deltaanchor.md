# ReadX Resource Aggregator

ReadX Resource Aggregator 是一个面向技术研究、学术文献采集与互联网信息归档的轻量级外链资源汇总系统。该项目定位于帮助研究人员、开发者与内容策展人高效收集、分类、检索和展示来自特定内容源的海量文章链接，提供一致化的访问入口与元数据管理能力。

本项目不生产内容，而是作为结构化链接索引层，对上游来源（read.xwpxi.com）进行系统性整理，并通过简洁的 Web 界面或 API 输出可机读的资源清单。目标用户包括需要批量获取参考链接的爬虫开发者、人工审核团队以及搭建垂直领域导航站点的运维人员。

## 功能概览

自动抓取索引：基于配置的 URL 规则，周期性拉取目标域名下的文章链接，提取标题、发布时间、内容摘要等基础元数据。

去重与校验：对采集到的 URL 进行 MD5 去重，自动剔除状态码非 200 的失效链接，保证资源库活性。

标签分类：支持通过正则表达式或关键词匹配为每条链接打上多级标签，便于按主题筛选。

全文检索：集成 SQLite FTS5 或 Elasticsearch 可选后端，支持对文章标题与摘要的快速模糊查询。

批量导出：提供 JSON、CSV、Markdown 列表三种导出格式，满足不同下游工具链的输入需求。

定时任务调度：内置基于 cron 表达式的调度器，支持每日、每周或自定义间隔自动更新资源池。

访问统计：记录每个外链的点击次数与最后访问时间，辅助判断内容热度与衰退趋势。

Web 管理面板：提供轻量级 Flask 管理界面，支持手动添加、编辑、删除链接，以及查看抓取日志。

## 应用场景

技术博客聚合导航：技术团队可基于本系统定期采集特定技术社区的文章链接，构建内部知识库的推荐阅读列表，避免重复手动搜集。

学术文献辅助整理：研究人员在撰写文献综述时，可利用本项目的批量导出功能，将来源站点的相关文章链接快速导入 Zotero 或 EndNote 等文献管理工具。

网站内容迁移辅助：在网站改版或域名迁移过程中，通过本系统导出完整的旧站文章 URL 清单，配合重写规则实现批量 301 跳转映射。

爬虫任务队列构建：开发者可将导出的 URL 列表直接作为 Scrapy 或 Puppeteer 爬虫的起始种子队列，加速垂直领域数据采集任务的部署。

人工审核工作台：内容审核团队可通过 Web 面板逐条查看链接状态与标题，快速标记违规或低质内容，形成审核报告。

## 快速开始

以下步骤适用于 Linux 与 macOS 环境，Windows 用户建议通过 WSL2 或 Git Bash 执行。

```bash
# 克隆项目仓库
git clone https://github.com/readx-project/readx-aggregator.git
cd readx-aggregator

# 创建并激活 Python 虚拟环境
python3 -m venv venv
source venv/bin/activate  # Windows 下为 venv\Scripts\activate

# 安装核心依赖
pip install --upgrade pip
pip install -r requirements.txt

# 初始化 SQLite 数据库与 FTS 索引
python manage.py init-db
python manage.py rebuild-index

# 启动 Web 服务（默认监听 127.0.0.1:5000）
python manage.py runserver
```

访问 http://127.0.0.1:5000 即可进入资源列表首页。首次启动时系统会自动导入示例数据，完整资源导入需执行后续同步命令。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 - 3.12 | 核心运行环境，低于 3.9 将无法解析类型注解 |
| SQLite | 3.35.0 及以上 | 用于主数据库存储，需支持外键约束与 JSON 函数 |
| Flask | 2.3.x | Web 管理面板与 API 服务框架 |
| requests | 2.31.x | 执行 HTTP 抓取请求，处理重定向与超时 |
| beautifulsoup4 | 4.12.x | 解析文章页面 HTML，提取标题与摘要信息 |
| APScheduler | 3.10.x | 提供后台定时任务调度能力 |
| lxml | 4.9.x | 高性能 XML/HTML 解析器，为 BeautifulSoup 的底层加速 |
| uWSGI | 2.0.x | 生产环境部署推荐网关服务器（可选） |
| Elasticsearch | 8.x 客户端库 | 仅在使用 ES 作为检索后端时需要（可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门 | docs/quickstart.md | 如何快速运行并看到第一条资源数据？如何配置抓取目标？ |
| 运维 | docs/deployment.md | 生产环境如何用 uWSGI + Nginx 部署？如何设置 systemd 守护进程？ |
| 开发 | docs/api_reference.md | 对外提供了哪些 REST API？请求参数与返回格式是怎样的？ |
| 进阶 | docs/custom_parser.md | 如何针对不同来源站点的 HTML 结构编写自定义解析器？ |

## 资源列表

- http://www.read.xwpxi.com/Article/28194.shtml
- http://www.read.xwpxi.com/Article/7637.shtml
- http://www.read.xwpxi.com/Article/9265.shtml
- http://www.read.xwpxi.com/Article/7022221.shtml
- http://www.read.xwpxi.com/Article/0883.shtml
- http://www.read.xwpxi.com/Article/5234137.shtml
- http://www.read.xwpxi.com/Article/2816.shtml
- http://www.read.xwpxi.com/Article/999984.shtml
- http://www.read.xwpxi.com/Article/188302.shtml
- http://www.read.xwpxi.com/Article/1483355.shtml
- http://www.read.xwpxi.com/Article/13518.shtml
- http://www.read.xwpxi.com/Article/28306.shtml
- http://www.read.xwpxi.com/Article/7378.shtml
- http://www.read.xwpxi.com/Article/75529.shtml
- http://www.read.xwpxi.com/Article/1719376.shtml
- http://www.read.xwpxi.com/Article/85190.shtml
- http://www.read.xwpxi.com/Article/130554.shtml
- http://www.read.xwpxi.com/Article/32086.shtml
- http://www.read.xwpxi.com/Article/22688.shtml
- http://www.read.xwpxi.com/Article/3249435.shtml
- http://www.read.xwpxi.com/Article/04754.shtml
- http://www.read.xwpxi.com/Article/053982.shtml
- http://www.read.xwpxi.com/Article/018609.shtml
- http://www.read.xwpxi.com/Article/5901.shtml
- http://www.read.xwpxi.com/Article/75756.shtml
- http://www.read.xwpxi.com/Article/15134.shtml
- http://www.read.xwpxi.com/Article/370093.shtml
- http://www.read.xwpxi.com/Article/46143.shtml
- http://www.read.xwpxi.com/Article/4750.shtml
- http://www.read.xwpxi.com/Article/195959.shtml
- http://www.read.xwpxi.com/Article/728362.shtml
- http://www.read.xwpxi.com/Article/24326.shtml
- http://www.read.xwpxi.com/Article/4348.shtml
- http://www.read.xwpxi.com/Article/6756.shtml
- http://www.read.xwpxi.com/Article/2901.shtml
- http://www.read.xwpxi.com/Article/84216.shtml
- http://www.read.xwpxi.com/Article/632480.shtml
- http://www.read.xwpxi.com/Article/7363.shtml
- http://www.read.xwpxi.com/Article/9575533.shtml
- http://www.read.xwpxi.com/Article/0210.shtml
- http://www.read.xwpxi.com/Article/637854.shtml
- http://www.read.xwpxi.com/Article/6344666.shtml
- http://www.read.xwpxi.com/Article/6157.shtml
- http://www.read.xwpxi.com/Article/5223.shtml
- http://www.read.xwpxi.com/Article/7772030.shtml
- http://www.read.xwpxi.com/Article/29138.shtml
- http://www.read.xwpxi.com/Article/7692.shtml
- http://www.read.xwpxi.com/Article/2388021.shtml
- http://www.read.xwpxi.com/Article/0656.shtml
- http://www.read.xwpxi.com/Article/89646.shtml
- http://www.read.xwpxi.com/Article/535264.shtml
- http://www.read.xwpxi.com/Article/060255.shtml
- http://www.read.xwpxi.com/Article/0052.shtml
- http://www.read.xwpxi.com/Article/584873.shtml
- http://www.read.xwpxi.com/Article/3967444.shtml
- http://www.read.xwpxi.com/Article/190286.shtml
- http://www.read.xwpxi.com/Article/0788.shtml
- http://www.read.xwpxi.com/Article/6139763.shtml
- http://www.read.xwpxi.com/Article/9963.shtml
- http://www.read.xwpxi.com/Article/6683763.shtml
- http://www.read.xwpxi.com/Article/6488866.shtml
- http://www.read.xwpxi.com/Article/97694.shtml
- http://www.read.xwpxi.com/Article/4298572.shtml
- http://www.read.xwpxi.com/Article/31604.shtml
- http://www.read.xwpxi.com/Article/4640.shtml
- http://www.read.xwpxi.com/Article/7494165.shtml
- http://www.read.xwpxi.com/Article/0178996.shtml
- http://www.read.xwpxi.com/Article/6008.shtml
- http://www.read.xwpxi.com/Article/7149.shtml
- http://www.read.xwpxi.com/Article/8095984.shtml
- http://www.read.xwpxi.com/Article/15810.shtml
- http://www.read.xwpxi.com/Article/06668.shtml
- http://www.read.xwpxi.com/Article/9434211.shtml
- http://www.read.xwpxi.com/Article/87857.shtml
- http://www.read.xwpxi.com/Article/1573.shtml
- http://www.read.xwpxi.com/Article/1783.shtml
- http://www.read.xwpxi.com/Article/98211.shtml
- http://www.read.xwpxi.com/Article/8503286.shtml
- http://www.read.xwpxi.com/Article/7314.shtml
- http://www.read.xwpxi.com/Article/0675560.shtml
- http://www.read.xwpxi.com/Article/2240.shtml
- http://www.read.xwpxi.com/Article/74394.shtml
- http://www.read.xwpxi.com/Article/5554907.shtml
- http://www.read.xwpxi.com/Article/49506.shtml
- http://www.read.xwpxi.com/Article/66782.shtml
- http://www.read.xwpxi.com/Article/14221.shtml
- http://www.read.xwpxi.com/Article/014778.shtml
- http://www.read.xwpxi.com/Article/5895492.shtml
- http://www.read.xwpxi.com/Article/362439.shtml
- http://www.read.xwpxi.com/Article/05739.shtml
- http://www.read.xwpxi.com/Article/8150310.shtml
- http://www.read.xwpxi.com/Article/4565940.shtml
- http://www.read.xwpxi.com/Article/64763.shtml
- http://www.read.xwpxi.com/Article/888976.shtml
- http://www.read.xwpxi.com/Article/488088.shtml
- http://www.read.xwpxi.com/Article/2371920.shtml
- http://www.read.xwpxi.com/Article/076881.shtml
- http://www.read.xwpxi.com/Article/0042728.shtml
- http://www.read.xwpxi.com/Article/23032.shtml
- http://www.read.xwpxi.com/Article/946535.shtml
- http://www.read.xwpxi.com/Article/4981.shtml
- http://www.read.xwpxi.com/Article/1129.shtml
- http://www.read.xwpxi.com/Article/974045.shtml
- http://www.read.xwpxi.com/Article/6434973.shtml
- http://www.read.xwpxi.com/Article/238331.shtml
- http://www.read.xwpxi.com/Article/26219.shtml
- http://www.read.xwpxi.com/Article/1665539.shtml
- http://www.read.xwpxi.com/Article/9682702.shtml
- http://www.read.xwpxi.com/Article/8464.shtml
- http://www.read.xwpxi.com/Article/53962.shtml
- http://www.read.xwpxi.com/Article/7710.shtml
- http://www.read.xwpxi.com/Article/8006.shtml
- http://www.read.xwpxi.com/Article/217651.shtml
- http://www.read.xwpxi.com/Article/653497.shtml
- http://www.read.xwpxi.com/Article/5672.shtml
- http://www.read.xwpxi.com/Article/373009.shtml
- http://www.read.xwpxi.com/Article/92915.shtml
- http://www.read.xwpxi.com/Article/3706.shtml
- http://www.read.xwpxi.com/Article/818794.shtml
- http://www.read.xwpxi.com/Article/73642.shtml
- http://www.read.xwpxi.com/Article/4338.shtml
- http://www.read.xwpxi.com/Article/9696.shtml
- http://www.read.xwpxi.com/Article/5137.shtml
- http://www.read.xwpxi.com/Article/6407.shtml
- http://www.read.xwpxi.com/Article/5884319.shtml
- http://www.read.xwpxi.com/Article/6143755.shtml
- http://www.read.xwpxi.com/Article/922639.shtml
- http://www.read.xwpxi.com/Article/10324.shtml
- http://www.read.xwpxi.com/Article/1711.shtml
- http://www.read.xwpxi.com/Article/7081.shtml
- http://www.read.xwpxi.com/Article/3039408.shtml
- http://www.read.xwpxi.com/Article/102542.shtml
- http://www.read.xwpxi.com/Article/4811462.shtml
- http://www.read.xwpxi.com/Article/7862.shtml
- http://www.read.xwpxi.com/Article/5634.shtml
- http://www.read.xwpxi.com/Article/50150.shtml
- http://www.read.xwpxi.com/Article/3240.shtml
- http://www.read.xwpxi.com/Article/0491.shtml
- http://www.read.xwpxi.com/Article/1335213.shtml
- http://www.read.xwpxi.com/Article/1015.shtml
- http://www.read.xwpxi.com/Article/2138.shtml
- http://www.read.xwpxi.com/Article/5259986.shtml
- http://www.read.xwpxi.com/Article/1440.shtml
- http://www.read.xwpxi.com/Article/195938.shtml
- http://www.read.xwpxi.com/Article/5645.shtml
- http://www.read.xwpxi.com/Article/953333.shtml
- http://www.read.xwpxi.com/Article/018837.shtml
- http://www.read.xwpxi.com/Article/12316.shtml
- http://www.read.xwpxi.com/Article/3775.shtml
- http://www.read.xwpxi.com/Article/7050570.shtml
- http://www.read.xwpxi.com/Article/37783.shtml
- http://www.read.xwpxi.com/Article/9765.shtml
- http://www.read.xwpxi.com/Article/81866.shtml
- http://www.read.xwpxi.com/Article/77330.shtml
- http://www.read.xwpxi.com/Article/969181.shtml
- http://www.read.xwpxi.com/Article/78922.shtml
- http://www.read.xwpxi.com/Article/20072.shtml
- http://www.read.xwpxi.com/Article/36906.shtml
- http://www.read.xwpxi.com/Article/992422.shtml
- http://www.read.xwpxi.com/Article/69507.shtml
- http://www.read.xwpxi.com/Article/643225.shtml
- http://www.read.xwpxi.com/Article/9673300.shtml
- http://www.read.xwpxi.com/Article/8507730.shtml
- http://www.read.xwpxi.com/Article/6495.shtml
- http://www.read.xwpxi.com/Article/2545088.shtml
- http://www.read.xwpxi.com/Article/062478.shtml
- http://www.read.xwpxi.com/Article/6647.shtml
- http://www.read.xwpxi.com/Article/6540.shtml
- http://www.read.xwpxi.com/Article/43974.shtml
- http://www.read.xwpxi.com/Article/7629.shtml
- http://www.read.xwpxi.com/Article/071344.shtml
- http://www.read.xwpxi.com/Article/12320.shtml
- http://www.read.xwpxi.com/Article/6297.shtml
- http://www.read.xwpxi.com/Article/5092.shtml
- http://www.read.xwpxi.com/Article/7613753.shtml
- http://www.read.xwpxi.com/Article/5738787.shtml
- http://www.read.xwpxi.com/Article/1937.shtml
- http://www.read.xwpxi.com/Article/3383931.shtml
- http://www.read.xwpxi.com/Article/3328366.shtml
- http://www.read.xwpxi.com/Article/455485.shtml
- http://www.read.xwpxi.com/Article/139911.shtml
- http://www.read.xwpxi.com/Article/5724147.shtml
- http://www.read.xwpxi.com/Article/2397034.shtml
- http://www.read.xwpxi.com/Article/538169.shtml
- http://www.read.xwpxi.com/Article/11842.shtml
- http://www.read.xwpxi.com/Article/89126.shtml
- http://www.read.xwpxi.com/Article/7343.shtml
- http://www.read.xwpxi.com/Article/3590071.shtml
- http://www.read.xwpxi.com/Article/25983.shtml
- http://www.read.xwpxi.com/Article/12727.shtml
- http://www.read.xwpxi.com/Article/6315021.shtml
- http://www.read.xwpxi.com/Article/280286.shtml
- http://www.read.xwpxi.com/Article/15707.shtml
- http://www.read.xwpxi.com/Article/7523212.shtml
- http://www.read.xwpxi.com/Article/26022.shtml
- http://www.read.xwpxi.com/Article/25899.shtml
- http://www.read.xwpxi.com/Article/15881.shtml
- http://www.read.xwpxi.com/Article/3180.shtml
- http://www.read.xwpxi.com/Article/6647788.shtml
- http://www.read.xwpxi.com/Article/0957.shtml
- http://www.read.xwpxi.com/Article/9654.shtml
- http://www.read.xwpxi.com/Article/93975.shtml
- http://www.read.xwpxi.com/Article/659609.shtml
- http://www.read.xwpxi.com/Article/9690.shtml
- http://www.read.xwpxi.com/Article/0299047.shtml
- http://www.read.xwpxi.com/Article/0937910.shtml
- http://www.read.xwpxi.com/Article/971021.shtml
- http://www.read.xwpxi.com/Article/40665.shtml
- http://www.read.xwpxi.com/Article/395465.shtml
- http://www.read.xwpxi.com/Article/2322.shtml
- http://www.read.xwpxi.com/Article/4295145.shtml
- http://www.read.xwpxi.com/Article/5309903.shtml
- http://www.read.xwpxi.com/Article/34035.shtml
- http://www.read.xwpxi.com/Article/691013.shtml
- http://www.read.xwpxi.com/Article/4317655.shtml
- http://www.read.xwpxi.com/Article/10036.shtml
- http://www.read.xwpxi.com/Article/7876273.shtml
- http://www.read.xwpxi.com/Article/411458.shtml
- http://www.read.xwpxi.com/Article/4270.shtml
- http://www.read.xwpxi.com/Article/5112.shtml
- http://www.read.xwpxi.com/Article/58702.shtml
- http://www.read.xwpxi.com/Article/756871.shtml
- http://www.read.xwpxi.com/Article/442449.shtml
- http://www.read.xwpxi.com/Article/953887.shtml
- http://www.read.xwpxi.com/Article/26793.shtml
- http://www.read.xwpxi.com/Article/0117.shtml
- http://www.read.xwpxi.com/Article/9527145.shtml
- http://www.read.xwpxi.com/Article/426442.shtml
- http://www.read.xwpxi.com/Article/8217.shtml
- http://www.read.xwpxi.com/Article/59563.shtml
- http://www.read.xwpxi.com/Article/151761.shtml
- http://www.read.xwpxi.com/Article/4774681.shtml
- http://www.read.xwpxi.com/Article/2706.shtml
- http://www.read.xwpxi.com/Article/3322728.shtml
- http://www.read.xwpxi.com/Article/20050.shtml
- http://www.read.xwpxi.com/Article/1265391.shtml
- http://www.read.xwpxi.com/Article/1298663.shtml
- http://www.read.xwpxi.com/Article/1353.shtml
- http://www.read.xwpxi.com/Article/7572335.shtml
- http://www.read.xwpxi.com/Article/252587.shtml
- http://www.read.xwpxi.com/Article/331917.shtml
- http://www.read.xwpxi.com/Article/583494.shtml
- http://www.read.xwpxi.com/Article/0967228.shtml
- http://www.read.xwpxi.com/Article/8045.shtml
- http://www.read.xwpxi.com/Article/5340007.shtml
- http://www.read.xwpxi.com/Article/01373.shtml
- http://www.read.xwpxi.com/Article/1017163.shtml
- http://www.read.xwpxi.com/Article/50383.shtml
- http://www.read.xwpxi.com/Article/82085.shtml
- http://www.read.xwpxi.com/Article/369683.shtml

## 项目结构

```
readx-aggregator/
├── manage.py                 # 统一命令行入口（init-db, runserver, crawl, export）
├── requirements.txt          # Python 依赖清单（生产与开发环境合并）
├── .env.example              # 环境变量模板（数据库路径、调度间隔、日志级别）
├── readx/
│   ├── __init__.py           # 包初始化，暴露核心工厂函数 create_app
│   ├── config.py             # 配置类（开发、测试、生产三模式，支持 .env 覆盖）
│   ├── models.py             # SQLAlchemy ORM 模型定义（Resource, Tag, CrawlLog）
│   ├── schemas.py            # Pydantic 校验模型（API 请求/响应结构）
│   ├── extensions.py         # 扩展实例化（db, scheduler, cache 等）
│   ├── crawler/
│   │   ├── __init__.py       # 爬虫子模块导出
│   │   ├── fetcher.py        # 基于 requests + 重试机制的页面抓取器
│   │   ├── parser.py         # BeautifulSoup 通用解析器，支持插件式扩展
│   │   └── scheduler.py      # APScheduler 任务注册与启动管理
│   ├── web/
│   │   ├── __init__.py       # 蓝图注册与路由汇总
│   │   ├── views.py          # Flask 路由视图（列表、详情、管理、导出）
│   │   ├── templates/        # Jinja2 模板目录（base.html, index.html, admin.html）
│   │   └── static/           # 静态资源（CSS, JS, 图标）
│   ├── api/
│   │   ├── __init__.py       # API 蓝图初始化
│   │   ├── v1.py             # REST API 端点（/api/v1/resources, /api/v1/tags）
│   │   └── middlewares.py    # 请求日志、限流、异常处理中间件
│   ├── services/
│   │   ├── resource_service.py    # 资源增删改查与去重业务逻辑
│   │   ├── search_service.py      # FTS5 / Elasticsearch 检索服务抽象
│   │   └── export_service.py      # JSON / CSV / Markdown 导出生成器
│   └── utils/
│       ├── validators.py     # URL 校验、标签规范化工具函数
│       └── logger.py         # 统一日志格式（JSON 结构化输出，支持文件轮转）
├── migrations/               # Alembic 数据库迁移脚本（自动生成与手动调整）
├── tests/
│   ├── unit/                 # 单元测试（模型、服务层、工具函数）
│   └── integration/          # 集成测试（API 调用、爬虫端到端流程）
├── scripts/
│   ├── seed_data.py          # 初始化测试数据脚本
│   └── backup_db.sh          # 数据库定时备份 Shell 脚本
└── docs/                     # 详细文档目录（快速开始、部署、API 参考等）
```

## 贡献指南

我们欢迎并鼓励社区贡献，无论是报告问题、提交补丁还是完善文档。请遵循以下步骤：

1. 在 GitHub Issues 中查找或新建一个议题，简要描述您要解决的问题或希望添加的功能，避免重复劳动。

2. Fork 本项目至您的个人仓库，并基于 main 分支创建一个新的功能分支，分支命名建议采用 feat/xxx 或 fix/xxx 格式。

3. 编写代码或文档变更时，请确保遵循项目现有的代码风格（使用 black 与 isort 进行格式化），并为新增函数添加 docstring 与类型注解。

4. 在提交 Pull Request 之前，请运行全部测试套件确保无回归（pytest tests/），并补充至少一个与变更相关的测试用例。

5. 提交 Pull Request 时，请清晰引用关联的 Issue 编号，并在描述中说明变更内容、测试覆盖情况以及潜在的影响面。

## 常见问题

Q: 为什么导入资源列表后部分链接显示状态码异常？

A: 这通常是由于目标服务器对批量请求实施了访问频率限制或临时封禁。建议在配置文件中调低 CRAWL_INTERVAL 和 BATCH_SIZE 参数，并启用 PROXY_ROTATION 选项。您也可以手动在管理后台对这些链接执行“重新检查”操作，系统会附带 User-Agent 轮换策略重试。

Q: 如何将现有资源数据迁移至生产环境的 PostgreSQL 数据库？

A: 项目默认使用 SQLite，但已内置 SQLAlchemy 的多数据库支持。您只需在 .env 文件中修改 DATABASE_URL 为 postgresql://user:pass@host/dbname 格式，然后执行 python manage.py migrate 即可自动同步表结构。原有 SQLite 数据可通过 python manage.py dump-data 导出为 JSON，再通过 python manage.py load-data 导入至新数据库。

Q: 定时抓取任务没有按预期执行，可能是什么原因？

A: 首先检查 APScheduler 日志是否记录有异常堆栈。常见原因包括：系统时区与配置的 CRON_TIMEZONE 不一致、Python 虚拟环境未正确激活导致 manage.py 找不到依赖、或者后台进程被系统 OOM Killer 终止。建议在生产环境使用 systemd 服务或 supervisor 托管 manage.py run-scheduler 进程，并配置日志轮转策略以便排查。

## 许可证

本项目采用 MIT 许可证。您可以自由使用、修改、分发本软件，包括用于商业目的，但需保留原始版权声明与许可声明。详细信息请参阅项目根目录下的 LICENSE 文件。

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
