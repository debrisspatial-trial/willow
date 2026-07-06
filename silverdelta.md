# LinkVault 资源聚合系统

LinkVault 是一个面向技术社区与开发者的轻量级外链资源聚合与导航系统。该项目旨在解决信息碎片化时代下技术文档、文章、教程及参考链接分散于各平台的问题，通过统一索引与分类管理，帮助用户快速定位高质量外部资源。LinkVault 适用于个人知识库构建、团队技术文档中心、开源项目推荐页及资讯聚合站点等场景，提供标准化的链接入库、检索、标签过滤及访问统计能力。

## 功能概览

**批量链接导入与解析**：支持从文本文件、CSV 或直接粘贴的 URL 列表中批量导入链接，自动解析网页标题、Meta 描述及关键词，生成索引条目。

**多维度标签与分类体系**：允许用户为每个资源链接添加自定义标签（如 "Python"、"性能优化"、"安全"），并支持层级分类，实现精细化的资源管理。

**全文检索与过滤**：基于 SQLite FTS5 或 Elasticsearch 适配器，提供对标题、描述、标签的全文搜索，同时支持按分类、域名、日期范围等多条件组合过滤。

**访问量统计与热度排序**：记录每个外链的点击次数，支持按访问量、添加时间或手动置顶排序，帮助识别热门资源。

**响应式预览卡片**：在资源列表中自动抓取目标页面的 Open Graph 信息，生成包含标题、摘要、缩略图的预览卡片，提升浏览体验。

**定期健康检查**：后台任务定期检测已收录链接的可访问性，标记失效或超时的链接，生成健康报告供管理员处理。

**RESTful API 接口**：提供完整的 JSON API，支持第三方应用对资源库进行增删改查、标签管理及统计查询，便于集成到现有工作流。

**数据导入导出**：支持将资源列表导出为 Markdown、JSON 或 CSV 格式，便于迁移或备份；同时支持从浏览器书签 HTML 文件导入。

## 应用场景

**技术团队内部知识库**：开发团队可将日常遇到的优秀技术博客、API 文档、故障排查案例统一收录至 LinkVault，按项目或技术栈分类，新成员入职时可快速了解团队常用的技术资源体系。

**开源项目推荐页**：开源项目维护者可使用 LinkVault 构建一个 "生态资源" 页面，集中列出社区贡献的教程、插件、扩展及第三方工具链接，降低新用户的生态认知门槛。

**个人开发者学习路线管理**：在学习新技术（如 Rust、Kubernetes）时，使用 LinkVault 整理所有课程链接、官方文档、实践项目及社区论坛，配合标签和搜索功能，形成结构化的学习路径。

**内容聚合与 Newsletter 素材库**：技术内容创作者可将日常阅读中发现的优质文章存入 LinkVault，定期筛选并导出为 Markdown 列表，快速生成 Newsletter 或周报的素材清单。

## 快速开始

以下步骤将在本地环境启动 LinkVault 开发实例，默认使用 SQLite 数据库。

```bash
# 克隆代码仓库
git clone https://github.com/your-org/linkvault.git
cd linkvault

# 安装 Python 依赖（推荐使用虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化数据库（创建表结构及默认标签）
python manage.py migrate
python manage.py loaddata initial_tags

# 导入示例资源数据
python manage.py import_links --file samples/tech_links.csv

# 启动开发服务器
python manage.py runserver --host 0.0.0.0 --port 8080
```

访问 `http://localhost:8080` 即可进入 LinkVault 控制台。默认管理员账号为 `admin`，密码为 `linkvault2024`，首次登录后请及时修改。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 - 3.12 | 核心运行环境，不支持 3.8 以下版本 |
| SQLite | 3.35.0 及以上 | 内置数据库，需启用 FTS5 扩展（默认启用） |
| Redis | 6.0 及以上 | 可选依赖，用于缓存与后台任务队列（生产环境推荐） |
| Node.js | 18.x 及以上 | 仅用于前端资源构建（开发模式可跳过） |
| Nginx | 1.18 及以上 | 生产环境反向代理与静态文件服务推荐 |
| Elasticsearch | 7.x 或 8.x | 可选全文检索引擎，用于替代 SQLite FTS5 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/` | 如何添加链接、创建分类、使用搜索、查看统计报表？ |
| 管理员指南 | `/docs/admin-guide/` | 如何配置健康检查、管理用户权限、调整系统参数？ |
| API 参考 | `/docs/api-reference/` | 有哪些可用端点、请求参数格式、鉴权方式是什么？ |
| 部署运维 | `/docs/deployment/` | 如何配置生产环境、使用 Docker 部署、设置 HTTPS 与反向代理？ |
| 开发贡献 | `/docs/contributing/` | 代码风格规范、提交信息格式、测试用例如何编写？ |

## 资源列表

- http://www.read.xwpxi.com/Article/7633872.shtml
- http://www.read.xwpxi.com/Article/91199.shtml
- http://www.read.xwpxi.com/Article/1150.shtml
- http://www.read.xwpxi.com/Article/344962.shtml
- http://www.read.xwpxi.com/Article/628526.shtml
- http://www.read.xwpxi.com/Article/42981.shtml
- http://www.read.xwpxi.com/Article/87557.shtml
- http://www.read.xwpxi.com/Article/001187.shtml
- http://www.read.xwpxi.com/Article/6995850.shtml
- http://www.read.xwpxi.com/Article/8071333.shtml
- http://www.read.xwpxi.com/Article/7927633.shtml
- http://www.read.xwpxi.com/Article/3212.shtml
- http://www.read.xwpxi.com/Article/41598.shtml
- http://www.read.xwpxi.com/Article/231761.shtml
- http://www.read.xwpxi.com/Article/347325.shtml
- http://www.read.xwpxi.com/Article/7504180.shtml
- http://www.read.xwpxi.com/Article/6810.shtml
- http://www.read.xwpxi.com/Article/20240.shtml
- http://www.read.xwpxi.com/Article/8251.shtml
- http://www.read.xwpxi.com/Article/04555.shtml
- http://www.read.xwpxi.com/Article/9644545.shtml
- http://www.read.xwpxi.com/Article/1155661.shtml
- http://www.read.xwpxi.com/Article/40051.shtml
- http://www.read.xwpxi.com/Article/839427.shtml
- http://www.read.xwpxi.com/Article/8327.shtml
- http://www.read.xwpxi.com/Article/88037.shtml
- http://www.read.xwpxi.com/Article/20877.shtml
- http://www.read.xwpxi.com/Article/04105.shtml
- http://www.read.xwpxi.com/Article/23083.shtml
- http://www.read.xwpxi.com/Article/17960.shtml
- http://www.read.xwpxi.com/Article/94588.shtml
- http://www.read.xwpxi.com/Article/1964.shtml
- http://www.read.xwpxi.com/Article/356256.shtml
- http://www.read.xwpxi.com/Article/4881673.shtml
- http://www.read.xwpxi.com/Article/174673.shtml
- http://www.read.xwpxi.com/Article/6656.shtml
- http://www.read.xwpxi.com/Article/6232739.shtml
- http://www.read.xwpxi.com/Article/392728.shtml
- http://www.read.xwpxi.com/Article/8455293.shtml
- http://www.read.xwpxi.com/Article/3851250.shtml
- http://www.read.xwpxi.com/Article/875481.shtml
- http://www.read.xwpxi.com/Article/84907.shtml
- http://www.read.xwpxi.com/Article/909929.shtml
- http://www.read.xwpxi.com/Article/7067.shtml
- http://www.read.xwpxi.com/Article/890183.shtml
- http://www.read.xwpxi.com/Article/3321318.shtml
- http://www.read.xwpxi.com/Article/7328346.shtml
- http://www.read.xwpxi.com/Article/49304.shtml
- http://www.read.xwpxi.com/Article/025080.shtml
- http://www.read.xwpxi.com/Article/36191.shtml
- http://www.read.xwpxi.com/Article/89966.shtml
- http://www.read.xwpxi.com/Article/5432066.shtml
- http://www.read.xwpxi.com/Article/23851.shtml
- http://www.read.xwpxi.com/Article/764523.shtml
- http://www.read.xwpxi.com/Article/3390.shtml
- http://www.read.xwpxi.com/Article/769989.shtml
- http://www.read.xwpxi.com/Article/51067.shtml
- http://www.read.xwpxi.com/Article/70959.shtml
- http://www.read.xwpxi.com/Article/2013.shtml
- http://www.read.xwpxi.com/Article/3322472.shtml
- http://www.read.xwpxi.com/Article/935056.shtml
- http://www.read.xwpxi.com/Article/277771.shtml
- http://www.read.xwpxi.com/Article/1540962.shtml
- http://www.read.xwpxi.com/Article/340712.shtml
- http://www.read.xwpxi.com/Article/1395.shtml
- http://www.read.xwpxi.com/Article/7086.shtml
- http://www.read.xwpxi.com/Article/39621.shtml
- http://www.read.xwpxi.com/Article/54405.shtml
- http://www.read.xwpxi.com/Article/5699.shtml
- http://www.read.xwpxi.com/Article/8906221.shtml
- http://www.read.xwpxi.com/Article/3667.shtml
- http://www.read.xwpxi.com/Article/4643563.shtml
- http://www.read.xwpxi.com/Article/7635280.shtml
- http://www.read.xwpxi.com/Article/15836.shtml
- http://www.read.xwpxi.com/Article/0911171.shtml
- http://www.read.xwpxi.com/Article/7273.shtml
- http://www.read.xwpxi.com/Article/19837.shtml
- http://www.read.xwpxi.com/Article/06284.shtml
- http://www.read.xwpxi.com/Article/91650.shtml
- http://www.read.xwpxi.com/Article/346099.shtml
- http://www.read.xwpxi.com/Article/7872573.shtml
- http://www.read.xwpxi.com/Article/0358318.shtml
- http://www.read.xwpxi.com/Article/3464772.shtml
- http://www.read.xwpxi.com/Article/2765862.shtml
- http://www.read.xwpxi.com/Article/68969.shtml
- http://www.read.xwpxi.com/Article/6226.shtml
- http://www.read.xwpxi.com/Article/37500.shtml
- http://www.read.xwpxi.com/Article/38456.shtml
- http://www.read.xwpxi.com/Article/669522.shtml
- http://www.read.xwpxi.com/Article/9271.shtml
- http://www.read.xwpxi.com/Article/3741.shtml
- http://www.read.xwpxi.com/Article/82732.shtml
- http://www.read.xwpxi.com/Article/2647.shtml
- http://www.read.xwpxi.com/Article/562419.shtml
- http://www.read.xwpxi.com/Article/5974.shtml
- http://www.read.xwpxi.com/Article/06296.shtml
- http://www.read.xwpxi.com/Article/989944.shtml
- http://www.read.xwpxi.com/Article/1500.shtml
- http://www.read.xwpxi.com/Article/3521801.shtml
- http://www.read.xwpxi.com/Article/3609.shtml
- http://www.read.xwpxi.com/Article/61949.shtml
- http://www.read.xwpxi.com/Article/7926.shtml
- http://www.read.xwpxi.com/Article/8420456.shtml
- http://www.read.xwpxi.com/Article/55695.shtml
- http://www.read.xwpxi.com/Article/9308.shtml
- http://www.read.xwpxi.com/Article/6930708.shtml
- http://www.read.xwpxi.com/Article/0383698.shtml
- http://www.read.xwpxi.com/Article/089922.shtml
- http://www.read.xwpxi.com/Article/19771.shtml
- http://www.read.xwpxi.com/Article/5277133.shtml
- http://www.read.xwpxi.com/Article/8992.shtml
- http://www.read.xwpxi.com/Article/4696958.shtml
- http://www.read.xwpxi.com/Article/8554470.shtml
- http://www.read.xwpxi.com/Article/7535.shtml
- http://www.read.xwpxi.com/Article/208608.shtml
- http://www.read.xwpxi.com/Article/42016.shtml
- http://www.read.xwpxi.com/Article/60286.shtml
- http://www.read.xwpxi.com/Article/568254.shtml
- http://www.read.xwpxi.com/Article/3275135.shtml
- http://www.read.xwpxi.com/Article/2859.shtml
- http://www.read.xwpxi.com/Article/604345.shtml
- http://www.read.xwpxi.com/Article/670203.shtml
- http://www.read.xwpxi.com/Article/2443.shtml
- http://www.read.xwpxi.com/Article/45991.shtml
- http://www.read.xwpxi.com/Article/74360.shtml
- http://www.read.xwpxi.com/Article/0369109.shtml
- http://www.read.xwpxi.com/Article/9439.shtml
- http://www.read.xwpxi.com/Article/59444.shtml
- http://www.read.xwpxi.com/Article/723102.shtml
- http://www.read.xwpxi.com/Article/3059.shtml
- http://www.read.xwpxi.com/Article/090578.shtml
- http://www.read.xwpxi.com/Article/6020486.shtml
- http://www.read.xwpxi.com/Article/967779.shtml
- http://www.read.xwpxi.com/Article/9187725.shtml
- http://www.read.xwpxi.com/Article/53949.shtml
- http://www.read.xwpxi.com/Article/49936.shtml
- http://www.read.xwpxi.com/Article/58668.shtml
- http://www.read.xwpxi.com/Article/8683.shtml
- http://www.read.xwpxi.com/Article/78196.shtml
- http://www.read.xwpxi.com/Article/0884640.shtml
- http://www.read.xwpxi.com/Article/1721950.shtml
- http://www.read.xwpxi.com/Article/365136.shtml
- http://www.read.xwpxi.com/Article/2770175.shtml
- http://www.read.xwpxi.com/Article/60316.shtml
- http://www.read.xwpxi.com/Article/78204.shtml
- http://www.read.xwpxi.com/Article/123613.shtml
- http://www.read.xwpxi.com/Article/20114.shtml
- http://www.read.xwpxi.com/Article/5849.shtml
- http://www.read.xwpxi.com/Article/93857.shtml
- http://www.read.xwpxi.com/Article/565024.shtml
- http://www.read.xwpxi.com/Article/428948.shtml
- http://www.read.xwpxi.com/Article/493655.shtml
- http://www.read.xwpxi.com/Article/52652.shtml
- http://www.read.xwpxi.com/Article/9019081.shtml
- http://www.read.xwpxi.com/Article/7141325.shtml
- http://www.read.xwpxi.com/Article/9968409.shtml
- http://www.read.xwpxi.com/Article/2720544.shtml
- http://www.read.xwpxi.com/Article/80482.shtml
- http://www.read.xwpxi.com/Article/69314.shtml
- http://www.read.xwpxi.com/Article/3821.shtml
- http://www.read.xwpxi.com/Article/2393359.shtml
- http://www.read.xwpxi.com/Article/9202.shtml
- http://www.read.xwpxi.com/Article/64211.shtml
- http://www.read.xwpxi.com/Article/936084.shtml
- http://www.read.xwpxi.com/Article/51317.shtml
- http://www.read.xwpxi.com/Article/5944162.shtml
- http://www.read.xwpxi.com/Article/8501320.shtml
- http://www.read.xwpxi.com/Article/227944.shtml
- http://www.read.xwpxi.com/Article/66735.shtml
- http://www.read.xwpxi.com/Article/85314.shtml
- http://www.read.xwpxi.com/Article/564132.shtml
- http://www.read.xwpxi.com/Article/0287.shtml
- http://www.read.xwpxi.com/Article/5851.shtml
- http://www.read.xwpxi.com/Article/887790.shtml
- http://www.read.xwpxi.com/Article/5604.shtml
- http://www.read.xwpxi.com/Article/394629.shtml
- http://www.read.xwpxi.com/Article/86568.shtml
- http://www.read.xwpxi.com/Article/3694528.shtml
- http://www.read.xwpxi.com/Article/54419.shtml
- http://www.read.xwpxi.com/Article/1838.shtml
- http://www.read.xwpxi.com/Article/8940.shtml
- http://www.read.xwpxi.com/Article/972604.shtml
- http://www.read.xwpxi.com/Article/463348.shtml
- http://www.read.xwpxi.com/Article/311213.shtml
- http://www.read.xwpxi.com/Article/98927.shtml
- http://www.read.xwpxi.com/Article/5796.shtml
- http://www.read.xwpxi.com/Article/95425.shtml
- http://www.read.xwpxi.com/Article/4523.shtml
- http://www.read.xwpxi.com/Article/655948.shtml
- http://www.read.xwpxi.com/Article/1713414.shtml
- http://www.read.xwpxi.com/Article/2929.shtml
- http://www.read.xwpxi.com/Article/24722.shtml
- http://www.read.xwpxi.com/Article/919328.shtml
- http://www.read.xwpxi.com/Article/7434990.shtml
- http://www.read.xwpxi.com/Article/741740.shtml
- http://www.read.xwpxi.com/Article/3330261.shtml
- http://www.read.xwpxi.com/Article/2318.shtml
- http://www.read.xwpxi.com/Article/7430.shtml
- http://www.read.xwpxi.com/Article/08618.shtml
- http://www.read.xwpxi.com/Article/281422.shtml
- http://www.read.xwpxi.com/Article/01873.shtml
- http://www.read.xwpxi.com/Article/512620.shtml
- http://www.read.xwpxi.com/Article/0991.shtml
- http://www.read.xwpxi.com/Article/2622.shtml
- http://www.read.xwpxi.com/Article/61197.shtml
- http://www.read.xwpxi.com/Article/7175.shtml
- http://www.read.xwpxi.com/Article/38467.shtml
- http://www.read.xwpxi.com/Article/86273.shtml
- http://www.read.xwpxi.com/Article/651336.shtml
- http://www.read.xwpxi.com/Article/905365.shtml
- http://www.read.xwpxi.com/Article/209160.shtml
- http://www.read.xwpxi.com/Article/2060140.shtml
- http://www.read.xwpxi.com/Article/2888.shtml
- http://www.read.xwpxi.com/Article/492075.shtml
- http://www.read.xwpxi.com/Article/76944.shtml
- http://www.read.xwpxi.com/Article/9416688.shtml
- http://www.read.xwpxi.com/Article/33515.shtml
- http://www.read.xwpxi.com/Article/6362964.shtml
- http://www.read.xwpxi.com/Article/114136.shtml
- http://www.read.xwpxi.com/Article/6498816.shtml
- http://www.read.xwpxi.com/Article/8381750.shtml
- http://www.read.xwpxi.com/Article/1375168.shtml
- http://www.read.xwpxi.com/Article/470257.shtml
- http://www.read.xwpxi.com/Article/8121396.shtml
- http://www.read.xwpxi.com/Article/1381636.shtml
- http://www.read.xwpxi.com/Article/50666.shtml
- http://www.read.xwpxi.com/Article/51236.shtml
- http://www.read.xwpxi.com/Article/9099.shtml
- http://www.read.xwpxi.com/Article/6645984.shtml
- http://www.read.xwpxi.com/Article/355395.shtml
- http://www.read.xwpxi.com/Article/632619.shtml
- http://www.read.xwpxi.com/Article/13378.shtml
- http://www.read.xwpxi.com/Article/2151539.shtml
- http://www.read.xwpxi.com/Article/67233.shtml
- http://www.read.xwpxi.com/Article/8999.shtml
- http://www.read.xwpxi.com/Article/5073.shtml
- http://www.read.xwpxi.com/Article/2779943.shtml
- http://www.read.xwpxi.com/Article/0246428.shtml
- http://www.read.xwpxi.com/Article/2076.shtml
- http://www.read.xwpxi.com/Article/4023499.shtml
- http://www.read.xwpxi.com/Article/23870.shtml
- http://www.read.xwpxi.com/Article/443669.shtml
- http://www.read.xwpxi.com/Article/6033.shtml
- http://www.read.xwpxi.com/Article/576270.shtml
- http://www.read.xwpxi.com/Article/245771.shtml
- http://www.read.xwpxi.com/Article/36480.shtml
- http://www.read.xwpxi.com/Article/375241.shtml
- http://www.read.xwpxi.com/Article/584134.shtml
- http://www.read.xwpxi.com/Article/29221.shtml
- http://www.read.xwpxi.com/Article/6701441.shtml

## 项目结构

```
linkvault/
├── manage.py                  # Django 项目入口，包含 CLI 命令扩展
├── requirements.txt           # Python 依赖清单（Django 4.2 + Celery + lxml）
├── docker-compose.yml         # 生产环境容器编排（含 Redis + PostgreSQL 可选）
├── .env.example               # 环境变量模板（数据库连接、密钥、调试模式）
│
├── linkvault/
│   ├── settings/              # 多环境配置模块
│   │   ├── base.py            # 基础配置（应用注册、中间件、模板引擎）
│   │   ├── development.py     # 开发环境配置（SQLite、DEBUG=True）
│   │   └── production.py      # 生产环境配置（PostgreSQL/Redis、缓存、日志）
│   ├── urls.py                # 根路由（API v1 + 管理后台 + 健康检查）
│   └── celery.py              # Celery 应用定义（周期性健康检查任务）
│
├── apps/
│   ├── links/                 # 链接资源核心模块
│   │   ├── models.py          # Link, Tag, Category, ClickLog 数据模型
│   │   ├── admin.py           # Django Admin 定制（列表过滤、批量操作）
│   │   ├── services/          # 业务逻辑层
│   │   │   ├── importer.py    # CSV/JSON/HTML 书签导入器
│   │   │   ├── crawler.py     # Open Graph 信息抓取与标题解析
│   │   │   └── health.py      # 链接可用性检查与状态更新
│   │   └── api/               # DRF 视图集与序列化器
│   │       ├── views.py       # LinkViewSet, TagViewSet
│   │       └── serializers.py # 资源输出格式控制
│   │
│   ├── search/                # 全文检索模块（支持 SQLite FTS5 与 Elasticsearch 适配）
│   │   ├── backends/          # 可插拔检索引擎适配器
│   │   └── indexes.py         # 索引配置与重建脚本
│   │
│   ├── stats/                 # 访问统计与趋势分析
│   │   ├── middleware.py      # 点击计数中间件（异步写入 Redis）
│   │   └── aggregator.py      # 按日/周/月聚合统计任务
│   │
│   └── users/                 # 用户认证与权限管理（基于 Django 内置扩展）
│       ├── models.py          # Profile 扩展字段（API Key、偏好设置）
│       └── permissions.py     # 自定义权限类（只读/编辑/管理员）
│
├── frontend/                  # 前端资源（Vue 3 + Vite）
│   ├── src/
│   │   ├── components/        # 卡片列表、搜索栏、标签过滤器
│   │   ├── views/             # 控制台、资源详情、导入页面
│   │   └── stores/            # Pinia 状态管理（搜索条件、分页）
│   └── dist/                  # 生产构建输出（由 Nginx 托管）
│
├── scripts/                   # 运维辅助脚本
│   ├── backup_db.sh           # 数据库定时备份脚本
│   ├── import_bulk.sh         # 批量链接导入命令行封装
│   └── health_check_cron.py   # 独立健康检查任务（可脱离 Celery 运行）
│
├── tests/                     # 单元测试与集成测试（pytest）
│   ├── test_models.py
│   ├── test_api.py
│   └── test_crawler.py
│
└── docs/                      # 完整文档（Sphinx + reStructuredText）
    ├── user-guide.rst
    ├── admin-guide.rst
    ├── api-reference.rst
    └── deployment.rst
```

## 贡献指南

1. 在 GitHub 仓库中提交 Issue 说明要修复的问题或新增的功能，等待维护者确认需求合理性，避免无效开发。

2. Fork 本仓库到个人账号，创建功能分支，分支命名采用 `feature/描述` 或 `fix/描述` 格式，例如 `feature/add-elasticsearch-adapter`。

3. 开发过程中请遵循项目代码风格（使用 Black 格式化 Python 代码，ESLint 处理前端代码），并在 `tests/` 目录下补充对应的测试用例，确保所有测试通过。

4. 提交 Pull Request 时，请填写完整的 PR 模板，描述变更内容、测试覆盖情况以及是否影响已有 API 或数据库结构。PR 需要至少一位维护者审核。

5. 文档更新与代码变更同等重要，任何新增功能或修改行为都需同步更新 `docs/` 下的对应文档，并确保文档中的示例代码可运行。

## 常见问题

**Q：导入大量链接时页面卡顿或超时，应该如何处理？**

A：推荐使用命令行导入工具而非 Web 界面上传。运行 `python manage.py import_links --file your_file.csv --batch-size 200`，该命令会以批量事务方式写入数据库，并自动处理重复 URL 的跳过逻辑。如果链接数量超过 5000 条，建议先在本地测试环境中试运行，确认无误后再迁移至生产环境。

**Q：健康检查任务标记了多个链接为失效，但手动访问这些链接是正常的，怎么解决？**

A：健康检查默认使用 Requests 库的 `timeout=10` 和 `allow_redirects=True` 参数，某些站点可能响应较慢或启用了防爬机制。您可以在 Admin 后台的 "系统设置" 中调整超时时间和 User-Agent 字符串，或暂时将误报链接加入白名单。如果问题持续出现，建议检查网络环境，确保服务器能够正常访问外网。

**Q：是否可以迁移到 PostgreSQL 或 MySQL 生产环境？**

A：可以。LinkVault 的 ORM 层兼容 PostgreSQL、MySQL 和 SQLite。您只需在环境变量中配置 `DATABASE_URL=postgresql://user:pass@host:port/dbname` 或 `mysql://...`，然后运行 `python manage.py migrate` 即可完成迁移。部分使用 SQLite 特有 FTS5 的查询在 PostgreSQL 下会自动切换为 `tsvector` 方式，无需额外改造。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
