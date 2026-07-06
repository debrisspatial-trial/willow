# LinkVault 技术资源索引系统

LinkVault 是一个面向开发者与技术研究人员的结构化外链资源汇总与导航系统。该项目旨在解决技术文档、教程、案例分析与深度文章分散于互联网各处难以系统化检索的问题，通过人工筛选与标签化组织，将高质量技术内容聚合为可检索、可分类、可版本化的资源库。本系统适用于技术团队内部知识沉淀、开源项目文档外链管理、以及个人技术阅读清单的自动化构建。

## 功能概览

- 自动抓取与解析：系统通过可配置的爬虫模块定期抓取已收录 URL 的页面标题、摘要与发布时间，自动更新本地元数据缓存。
- 多维度标签分类：每个资源条目支持多个自定义标签（如 Python、分布式系统、数据库调优、前端工程化），便于按主题筛选。
- 全文检索支持：基于 SQLite FTS5 扩展或 Elasticsearch 适配器，提供对标题与摘要的快速关键词检索。
- 资源状态监控：定期检查已收录链接的可访问性（HTTP 状态码、响应时间），标记失效或重定向链接。
- 批量导入与导出：支持通过 CSV、JSON 或 OPML 格式批量导入外部链接列表，并可导出为 Markdown 表格或 HTML 书签文件。
- 版本化变更记录：每次资源增删改操作均记录变更日志，支持回滚至历史版本，便于团队协作审核。
- API 接口开放：提供 RESTful API 用于查询资源列表、获取详情、按标签聚合统计，可集成至 CI/CD 或文档生成流水线。
- 自定义视图模板：用户可编写 Jinja2 模板生成静态站点或 PDF 报告，将资源列表渲染为技术周报或学习路径指南。

## 应用场景

- 技术团队内部知识库建设：团队管理者可将项目文档、内部工具链地址、运维手册等链接统一录入 LinkVault，并通过标签区分环境（生产/预发布/测试），新成员入职时可一键获取全部必备资源清单。
- 开源项目外链托管：开源项目维护者常在 README 中放置大量参考链接，但难以维护更新。使用 LinkVault 管理所有外链，并通过 API 动态生成 README 中的资源列表，确保文档始终与资源库同步。
- 个人技术阅读工作流：技术爱好者可定期将阅读过的博客、论文、视频教程地址导入系统，利用标签构建个人知识图谱，配合检索功能快速回溯历史阅读内容，避免重复查找。
- 技术活动或课程资料汇总：线下 meetup、线上公开课或企业内训的讲师可将所有讲义链接、代码仓库地址、课后阅读材料统一收录，生成专属访问页面供学员查阅。
- 合规性审计与链接巡检：对于需要满足外部监管要求的金融或政务系统，运维人员可使用 LinkVault 定期扫描外链存活状态，生成合规性报告，确保所有引用的外部资源持续可用。

## 快速开始

以下命令可在 Ubuntu 22.04 / macOS 13 环境下完成 LinkVault 的克隆、安装与启动。

```bash
# 克隆代码仓库
git clone https://github.com/your-org/linkvault.git
cd linkvault

# 创建 Python 虚拟环境并激活
python3 -m venv venv
source venv/bin/activate

# 安装生产依赖
pip install --upgrade pip
pip install -r requirements.txt

# 初始化 SQLite 数据库与 FTS 索引
python scripts/init_db.py --config config/prod.yaml

# 启动开发服务器（默认监听 127.0.0.1:5000）
python app.py
```

访问 http://127.0.0.1:5000 即可看到资源列表主页。如需导入示例数据，可执行 `python scripts/seed_demo.py` 载入 50 条测试链接。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 - 3.11 | 核心运行环境，3.12 暂未完全兼容 |
| SQLite | 3.35.0 及以上 | 内置数据库，需启用 FTS5 扩展支持 |
| requests | 2.31.0 | HTTP 客户端库，用于资源抓取与状态检查 |
| beautifulsoup4 | 4.12.0 | HTML 解析器，用于提取页面标题与正文摘要 |
| PyYAML | 6.0 | 配置文件解析，支持 YAML 格式的站点规则定义 |
| Flask | 2.3.0 | Web 服务框架，提供 API 与管理界面 |
| apscheduler | 3.10.0 | 定时任务调度器，用于周期性链接巡检 |
| jinja2 | 3.1.0 | 模板引擎，用于生成静态视图与报告 |
| pytest | 7.4.0 | 单元测试框架（仅开发环境需要） |
| black | 23.0.0 | 代码格式化工具（仅开发环境需要） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | docs/getting_started.md | 如何快速配置第一个资源源、如何添加标签、如何生成第一个静态列表页 |
| 配置手册 | docs/configuration.md | 环境变量、YAML 配置文件各项参数含义、调度器间隔设置、邮件告警配置 |
| API 参考 | docs/api_reference.md | 所有 RESTful 接口的请求/响应格式、鉴权方式、分页参数说明及示例代码 |
| 运维指南 | docs/operations.md | 生产环境部署建议（Nginx + Gunicorn）、日志轮转策略、数据库备份与恢复流程 |

## 资源列表

- http://www.read.xwpxi.com/Article/12052.shtml
- http://www.read.xwpxi.com/Article/6019596.shtml
- http://www.read.xwpxi.com/Article/1069.shtml
- http://www.read.xwpxi.com/Article/2627960.shtml
- http://www.read.xwpxi.com/Article/3647.shtml
- http://www.read.xwpxi.com/Article/51038.shtml
- http://www.read.xwpxi.com/Article/669995.shtml
- http://www.read.xwpxi.com/Article/67707.shtml
- http://www.read.xwpxi.com/Article/1014.shtml
- http://www.read.xwpxi.com/Article/1975826.shtml
- http://www.read.xwpxi.com/Article/2716.shtml
- http://www.read.xwpxi.com/Article/52189.shtml
- http://www.read.xwpxi.com/Article/723131.shtml
- http://www.read.xwpxi.com/Article/22669.shtml
- http://www.read.xwpxi.com/Article/3487093.shtml
- http://www.read.xwpxi.com/Article/71786.shtml
- http://www.read.xwpxi.com/Article/1552.shtml
- http://www.read.xwpxi.com/Article/0831153.shtml
- http://www.read.xwpxi.com/Article/056962.shtml
- http://www.read.xwpxi.com/Article/27097.shtml
- http://www.read.xwpxi.com/Article/6976.shtml
- http://www.read.xwpxi.com/Article/4390690.shtml
- http://www.read.xwpxi.com/Article/5716958.shtml
- http://www.read.xwpxi.com/Article/726104.shtml
- http://www.read.xwpxi.com/Article/9248860.shtml
- http://www.read.xwpxi.com/Article/3161685.shtml
- http://www.read.xwpxi.com/Article/3787.shtml
- http://www.read.xwpxi.com/Article/618625.shtml
- http://www.read.xwpxi.com/Article/05724.shtml
- http://www.read.xwpxi.com/Article/573061.shtml
- http://www.read.xwpxi.com/Article/4962.shtml
- http://www.read.xwpxi.com/Article/043772.shtml
- http://www.read.xwpxi.com/Article/2924303.shtml
- http://www.read.xwpxi.com/Article/71574.shtml
- http://www.read.xwpxi.com/Article/715665.shtml
- http://www.read.xwpxi.com/Article/8038921.shtml
- http://www.read.xwpxi.com/Article/1995.shtml
- http://www.read.xwpxi.com/Article/3004087.shtml
- http://www.read.xwpxi.com/Article/8186.shtml
- http://www.read.xwpxi.com/Article/9906340.shtml
- http://www.read.xwpxi.com/Article/2443758.shtml
- http://www.read.xwpxi.com/Article/6259.shtml
- http://www.read.xwpxi.com/Article/27332.shtml
- http://www.read.xwpxi.com/Article/78866.shtml
- http://www.read.xwpxi.com/Article/4817.shtml
- http://www.read.xwpxi.com/Article/08889.shtml
- http://www.read.xwpxi.com/Article/954615.shtml
- http://www.read.xwpxi.com/Article/0878.shtml
- http://www.read.xwpxi.com/Article/65846.shtml
- http://www.read.xwpxi.com/Article/1695823.shtml
- http://www.read.xwpxi.com/Article/6228581.shtml
- http://www.read.xwpxi.com/Article/633046.shtml
- http://www.read.xwpxi.com/Article/1969.shtml
- http://www.read.xwpxi.com/Article/2568667.shtml
- http://www.read.xwpxi.com/Article/3161467.shtml
- http://www.read.xwpxi.com/Article/2411.shtml
- http://www.read.xwpxi.com/Article/6065411.shtml
- http://www.read.xwpxi.com/Article/9130461.shtml
- http://www.read.xwpxi.com/Article/7723103.shtml
- http://www.read.xwpxi.com/Article/0365.shtml
- http://www.read.xwpxi.com/Article/48022.shtml
- http://www.read.xwpxi.com/Article/0817717.shtml
- http://www.read.xwpxi.com/Article/9793.shtml
- http://www.read.xwpxi.com/Article/0103482.shtml
- http://www.read.xwpxi.com/Article/27648.shtml
- http://www.read.xwpxi.com/Article/4968734.shtml
- http://www.read.xwpxi.com/Article/000111.shtml
- http://www.read.xwpxi.com/Article/45317.shtml
- http://www.read.xwpxi.com/Article/1228.shtml
- http://www.read.xwpxi.com/Article/0228.shtml
- http://www.read.xwpxi.com/Article/6106102.shtml
- http://www.read.xwpxi.com/Article/6738217.shtml
- http://www.read.xwpxi.com/Article/5600.shtml
- http://www.read.xwpxi.com/Article/495613.shtml
- http://www.read.xwpxi.com/Article/7925342.shtml
- http://www.read.xwpxi.com/Article/49428.shtml
- http://www.read.xwpxi.com/Article/99822.shtml
- http://www.read.xwpxi.com/Article/7782.shtml
- http://www.read.xwpxi.com/Article/723846.shtml
- http://www.read.xwpxi.com/Article/41237.shtml
- http://www.read.xwpxi.com/Article/0792631.shtml
- http://www.read.xwpxi.com/Article/927624.shtml
- http://www.read.xwpxi.com/Article/3472.shtml
- http://www.read.xwpxi.com/Article/224220.shtml
- http://www.read.xwpxi.com/Article/756541.shtml
- http://www.read.xwpxi.com/Article/4032.shtml
- http://www.read.xwpxi.com/Article/7126529.shtml
- http://www.read.xwpxi.com/Article/2671460.shtml
- http://www.read.xwpxi.com/Article/2095.shtml
- http://www.read.xwpxi.com/Article/420395.shtml
- http://www.read.xwpxi.com/Article/7657203.shtml
- http://www.read.xwpxi.com/Article/6911971.shtml
- http://www.read.xwpxi.com/Article/60390.shtml
- http://www.read.xwpxi.com/Article/0056083.shtml
- http://www.read.xwpxi.com/Article/46928.shtml
- http://www.read.xwpxi.com/Article/8092.shtml
- http://www.read.xwpxi.com/Article/508358.shtml
- http://www.read.xwpxi.com/Article/6863431.shtml
- http://www.read.xwpxi.com/Article/0129315.shtml
- http://www.read.xwpxi.com/Article/21031.shtml
- http://www.read.xwpxi.com/Article/84213.shtml
- http://www.read.xwpxi.com/Article/44078.shtml
- http://www.read.xwpxi.com/Article/669374.shtml
- http://www.read.xwpxi.com/Article/692379.shtml
- http://www.read.xwpxi.com/Article/12547.shtml
- http://www.read.xwpxi.com/Article/4980773.shtml
- http://www.read.xwpxi.com/Article/2530.shtml
- http://www.read.xwpxi.com/Article/154677.shtml
- http://www.read.xwpxi.com/Article/559221.shtml
- http://www.read.xwpxi.com/Article/3949105.shtml
- http://www.read.xwpxi.com/Article/71247.shtml
- http://www.read.xwpxi.com/Article/559021.shtml
- http://www.read.xwpxi.com/Article/8425.shtml
- http://www.read.xwpxi.com/Article/027273.shtml
- http://www.read.xwpxi.com/Article/31495.shtml
- http://www.read.xwpxi.com/Article/473308.shtml
- http://www.read.xwpxi.com/Article/0713567.shtml
- http://www.read.xwpxi.com/Article/15455.shtml
- http://www.read.xwpxi.com/Article/0946.shtml
- http://www.read.xwpxi.com/Article/50541.shtml
- http://www.read.xwpxi.com/Article/762354.shtml
- http://www.read.xwpxi.com/Article/54847.shtml
- http://www.read.xwpxi.com/Article/507310.shtml
- http://www.read.xwpxi.com/Article/0185.shtml
- http://www.read.xwpxi.com/Article/9746.shtml
- http://www.read.xwpxi.com/Article/9448.shtml
- http://www.read.xwpxi.com/Article/0922935.shtml
- http://www.read.xwpxi.com/Article/85344.shtml
- http://www.read.xwpxi.com/Article/3116947.shtml
- http://www.read.xwpxi.com/Article/67957.shtml
- http://www.read.xwpxi.com/Article/7506.shtml
- http://www.read.xwpxi.com/Article/319349.shtml
- http://www.read.xwpxi.com/Article/59151.shtml
- http://www.read.xwpxi.com/Article/9022.shtml
- http://www.read.xwpxi.com/Article/800706.shtml
- http://www.read.xwpxi.com/Article/577562.shtml
- http://www.read.xwpxi.com/Article/6712808.shtml
- http://www.read.xwpxi.com/Article/4032451.shtml
- http://www.read.xwpxi.com/Article/2479365.shtml
- http://www.read.xwpxi.com/Article/817928.shtml
- http://www.read.xwpxi.com/Article/96335.shtml
- http://www.read.xwpxi.com/Article/348196.shtml
- http://www.read.xwpxi.com/Article/1607613.shtml
- http://www.read.xwpxi.com/Article/9380.shtml
- http://www.read.xwpxi.com/Article/47341.shtml
- http://www.read.xwpxi.com/Article/87361.shtml
- http://www.read.xwpxi.com/Article/0199631.shtml
- http://www.read.xwpxi.com/Article/188022.shtml
- http://www.read.xwpxi.com/Article/3383.shtml
- http://www.read.xwpxi.com/Article/0361816.shtml
- http://www.read.xwpxi.com/Article/9369165.shtml
- http://www.read.xwpxi.com/Article/5580711.shtml
- http://www.read.xwpxi.com/Article/994624.shtml
- http://www.read.xwpxi.com/Article/60221.shtml
- http://www.read.xwpxi.com/Article/5730340.shtml
- http://www.read.xwpxi.com/Article/9943880.shtml
- http://www.read.xwpxi.com/Article/36603.shtml
- http://www.read.xwpxi.com/Article/601597.shtml
- http://www.read.xwpxi.com/Article/9452.shtml
- http://www.read.xwpxi.com/Article/393082.shtml
- http://www.read.xwpxi.com/Article/312986.shtml
- http://www.read.xwpxi.com/Article/504027.shtml
- http://www.read.xwpxi.com/Article/2068758.shtml
- http://www.read.xwpxi.com/Article/935839.shtml
- http://www.read.xwpxi.com/Article/973377.shtml
- http://www.read.xwpxi.com/Article/8830.shtml
- http://www.read.xwpxi.com/Article/5556.shtml
- http://www.read.xwpxi.com/Article/247477.shtml
- http://www.read.xwpxi.com/Article/27606.shtml
- http://www.read.xwpxi.com/Article/0974122.shtml
- http://www.read.xwpxi.com/Article/015134.shtml
- http://www.read.xwpxi.com/Article/143204.shtml
- http://www.read.xwpxi.com/Article/6993.shtml
- http://www.read.xwpxi.com/Article/6008682.shtml
- http://www.read.xwpxi.com/Article/7125158.shtml
- http://www.read.xwpxi.com/Article/2979765.shtml
- http://www.read.xwpxi.com/Article/632181.shtml
- http://www.read.xwpxi.com/Article/31799.shtml
- http://www.read.xwpxi.com/Article/4758387.shtml
- http://www.read.xwpxi.com/Article/567342.shtml
- http://www.read.xwpxi.com/Article/25109.shtml
- http://www.read.xwpxi.com/Article/9239685.shtml
- http://www.read.xwpxi.com/Article/187135.shtml
- http://www.read.xwpxi.com/Article/4906.shtml
- http://www.read.xwpxi.com/Article/3411675.shtml
- http://www.read.xwpxi.com/Article/15748.shtml
- http://www.read.xwpxi.com/Article/788733.shtml
- http://www.read.xwpxi.com/Article/8242334.shtml
- http://www.read.xwpxi.com/Article/1592425.shtml
- http://www.read.xwpxi.com/Article/465948.shtml
- http://www.read.xwpxi.com/Article/55232.shtml
- http://www.read.xwpxi.com/Article/4517.shtml
- http://www.read.xwpxi.com/Article/58359.shtml
- http://www.read.xwpxi.com/Article/0350854.shtml
- http://www.read.xwpxi.com/Article/08256.shtml
- http://www.read.xwpxi.com/Article/41470.shtml
- http://www.read.xwpxi.com/Article/7804614.shtml
- http://www.read.xwpxi.com/Article/54616.shtml
- http://www.read.xwpxi.com/Article/47050.shtml
- http://www.read.xwpxi.com/Article/36993.shtml
- http://www.read.xwpxi.com/Article/7319.shtml
- http://www.read.xwpxi.com/Article/571674.shtml
- http://www.read.xwpxi.com/Article/5965503.shtml
- http://www.read.xwpxi.com/Article/6295.shtml
- http://www.read.xwpxi.com/Article/8396.shtml
- http://www.read.xwpxi.com/Article/24554.shtml
- http://www.read.xwpxi.com/Article/19894.shtml
- http://www.read.xwpxi.com/Article/033027.shtml
- http://www.read.xwpxi.com/Article/3723.shtml
- http://www.read.xwpxi.com/Article/0903.shtml
- http://www.read.xwpxi.com/Article/2784248.shtml
- http://www.read.xwpxi.com/Article/3827.shtml
- http://www.read.xwpxi.com/Article/963915.shtml
- http://www.read.xwpxi.com/Article/4092.shtml
- http://www.read.xwpxi.com/Article/685086.shtml
- http://www.read.xwpxi.com/Article/468482.shtml
- http://www.read.xwpxi.com/Article/02722.shtml
- http://www.read.xwpxi.com/Article/8728431.shtml
- http://www.read.xwpxi.com/Article/101760.shtml
- http://www.read.xwpxi.com/Article/325426.shtml
- http://www.read.xwpxi.com/Article/352282.shtml
- http://www.read.xwpxi.com/Article/6059239.shtml
- http://www.read.xwpxi.com/Article/16263.shtml
- http://www.read.xwpxi.com/Article/040905.shtml
- http://www.read.xwpxi.com/Article/8289.shtml
- http://www.read.xwpxi.com/Article/0381072.shtml
- http://www.read.xwpxi.com/Article/394040.shtml
- http://www.read.xwpxi.com/Article/135019.shtml
- http://www.read.xwpxi.com/Article/8749.shtml
- http://www.read.xwpxi.com/Article/8941.shtml
- http://www.read.xwpxi.com/Article/9024408.shtml
- http://www.read.xwpxi.com/Article/324053.shtml
- http://www.read.xwpxi.com/Article/9094997.shtml
- http://www.read.xwpxi.com/Article/9202992.shtml
- http://www.read.xwpxi.com/Article/92208.shtml
- http://www.read.xwpxi.com/Article/062557.shtml
- http://www.read.xwpxi.com/Article/59836.shtml
- http://www.read.xwpxi.com/Article/0995656.shtml
- http://www.read.xwpxi.com/Article/3336.shtml
- http://www.read.xwpxi.com/Article/9326.shtml
- http://www.read.xwpxi.com/Article/7776.shtml
- http://www.read.xwpxi.com/Article/575214.shtml
- http://www.read.xwpxi.com/Article/003490.shtml
- http://www.read.xwpxi.com/Article/028289.shtml
- http://www.read.xwpxi.com/Article/9655.shtml
- http://www.read.xwpxi.com/Article/398346.shtml
- http://www.read.xwpxi.com/Article/75843.shtml
- http://www.read.xwpxi.com/Article/3411.shtml
- http://www.read.xwpxi.com/Article/76771.shtml
- http://www.read.xwpxi.com/Article/8618264.shtml

## 项目结构

```
linkvault/
├── app/                                # 核心应用模块
│   ├── __init__.py                     # 应用工厂函数，初始化 Flask 与扩展
│   ├── routes/                         # 路由视图层
│   │   ├── api.py                      # RESTful API 端点实现（资源列表、详情、标签聚合）
│   │   └── web.py                      # Web 管理界面路由（仪表盘、批量操作页面）
│   ├── models/                         # 数据模型与 ORM 定义
│   │   ├── resource.py                 # Resource 表结构定义，包含 URL、标题、摘要、标签字段
│   │   ├── snapshot.py                 # 快照表，记录每次抓取的状态码与响应时间
│   │   └── changelog.py                # 变更日志表，记录增删改操作与操作人
│   ├── services/                       # 业务逻辑服务层
│   │   ├── crawler.py                  # 异步爬虫服务，管理请求队列与超时重试
│   │   ├── checker.py                  # 链接状态检查器，周期性巡检并更新状态
│   │   ├── indexer.py                  # FTS 索引维护服务，处理新增/更新资源的索引重建
│   │   └── exporter.py                 # 导出服务，支持 CSV / JSON / OPML / Markdown 格式
│   └── utils/                          # 工具函数集合
│       ├── validators.py               # URL 格式校验、域名白名单过滤
│       ├── parsers.py                  # HTML 标题与摘要提取，使用 BeautifulSoup 实现
│       └── logger.py                   # 日志配置封装，支持文件轮转与结构化输出
├── config/                             # 配置文件目录
│   ├── prod.yaml                       # 生产环境配置（数据库路径、调度间隔、告警阈值）
│   ├── dev.yaml                        # 开发环境配置（启用调试、测试数据库）
│   └── schema.yaml                     # 配置项 JSON Schema 定义，用于校验
├── scripts/                            # 运维与辅助脚本
│   ├── init_db.py                      # 初始化数据库表结构与 FTS 虚拟表
│   ├── seed_demo.py                    # 加载示例数据，便于快速体验
│   ├── backup.sh                       # 数据库备份脚本（配合 cron 使用）
│   └── migrate_v1_to_v2.py             # 版本升级迁移脚本
├── tests/                              # 单元测试与集成测试
│   ├── unit/                           # 单元测试（models, services, utils 各子模块）
│   ├── integration/                    # 集成测试（API 接口测试、数据库事务测试）
│   └── fixtures/                       # 测试固定数据（模拟 HTTP 响应、样本 HTML）
├── docs/                               # 文档源码
│   ├── getting_started.md              # 快速入门指南
│   ├── configuration.md                # 完整配置参数参考
│   ├── api_reference.md                # API 接口文档（含 curl 示例）
│   └── operations.md                   # 生产环境运维手册
├── static/                             # 静态资源（CSS / JavaScript / 图片）
│   ├── css/                            # 管理界面样式（基于 Bootstrap 定制）
│   └── js/                             # 前端交互脚本（表格排序、批量勾选、实时搜索）
├── templates/                          # Jinja2 HTML 模板
│   ├── base.html                       # 基础布局模板
│   ├── index.html                      # 资源列表主页面
│   ├── detail.html                     # 单个资源详情页
│   └── dashboard.html                  # 统计仪表盘（链接总数、存活率、标签分布）
├── requirements.txt                    # 生产环境 Python 依赖列表
├── requirements-dev.txt                # 开发环境额外依赖（pytest, black, mypy）
├── app.py                              # 应用入口文件（开发服务器启动脚本）
├── wsgi.py                             # 生产环境 WSGI 入口（Gunicorn 使用）
└── README.md                           # 项目说明文档（本文件）
```

## 贡献指南

1. 阅读项目行为准则（CODE_OF_CONDUCT.md）与贡献者许可协议（CLA），确保理解并同意相关条款。所有外部贡献需签署 CLA 方可合并。

2. 从 GitHub 仓库派生（fork）项目至个人账户，在本地克隆派生后的仓库，并添加 upstream 远程源指向主仓库，以便同步最新变更。

3. 创建功能分支（feature/xxx 或 fix/xxx），编写代码或文档。代码需遵循 Black 格式化规范与 PEP 8 风格，新功能应包含对应的单元测试与集成测试用例。

4. 运行完整测试套件确保无回归错误：执行 `pytest tests/ --cov=app --cov-report=html`，覆盖率不低于 85%。所有测试通过后方可提交。

5. 提交 pull request 至主仓库的 develop 分支，描述中需清晰说明变更目的、影响范围、测试结果以及相关 issue 编号。PR 将由维护者进行代码审查，通过后合并至主干。

## 常见问题

Q: 系统是否支持 PostgreSQL 替代 SQLite 作为生产数据库？

A: 支持。LinkVault 使用 SQLAlchemy ORM，理论上可切换至 PostgreSQL、MySQL 等关系型数据库。需在配置文件中修改 `database.url` 参数为对应的连接字符串（如 `postgresql://user:pass@localhost/linkvault`），并安装相应的数据库驱动（如 psycopg2-binary）。但需要注意 FTS 全文检索在不同数据库上的实现差异，PostgreSQL 需使用 tsvector 替代 SQLite FTS5，系统已提供适配器模块 `services/postgres_fts.py` 用于兼容。

Q: 如何自定义资源抓取的频率与并发数？

A: 抓取调度器配置位于 `config/prod.yaml` 的 `crawler` 字段下。`interval_hours` 控制全局抓取间隔（默认 24 小时），`concurrency` 控制同时抓取的线程池大小（默认 4）。对于特定域名或路径，可在 `rules` 小节配置覆盖策略，例如设置 `max_retries`、`timeout_seconds` 以及 `user_agent` 字符串。修改配置后重启服务即可生效，无需重建数据库。

Q: 系统能否处理需要登录或带有反爬机制的网站？

A: LinkVault 核心设计面向公开可访问的静态技术文章与文档页面，不提供内置的 JavaScript 渲染引擎或 Cookie 会话管理。对于需要登录或含有复杂反爬逻辑的网站，建议通过自定义中间件扩展实现。系统预留了 `services/auth_handler.py` 接口，开发者可继承 `BaseAuthHandler` 并实现 `get_session()` 方法返回 requests.Session 对象，然后在配置中指定该 handler 类路径即可启用。但需注意，使用此类功能需遵守目标网站的 robots.txt 及相关法律法规。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
