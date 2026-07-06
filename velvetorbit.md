# LinkMaster Pro

LinkMaster Pro 是一个面向技术内容聚合与外部资源管理的开源链接导航系统。该项目定位于为开发者、技术博主、研究机构及知识管理团队提供一套标准化的外链组织、分类、检索与展示方案。LinkMaster Pro 并非简单的书签管理器，而是一个具备元数据扩展能力、批量导入导出、分类视图与访问统计能力的轻量级技术资源目录引擎。

目标用户包括需要维护大量技术参考链接的文档工程师、进行行业信息汇总的分析师、以及搭建内部技术知识库的运维团队。LinkMaster Pro 解决了分散链接难以系统化管理、缺乏上下文描述、无法快速定位有效资源的问题，通过结构化的数据组织与清晰的用户界面，将碎片化的 URL 转化为可复用、可传承的知识资产。

## 功能概览

批量链接导入：支持从纯文本、CSV 及 JSON 格式批量导入外部链接，自动解析 URL 并提取基础信息，减少手动录入成本。

分类与标签体系：提供无限层级的目录分类与自由标签系统，允许用户为每个链接赋予多个维度的属性标记，实现多角度检索。

元数据扩展字段：内置标题、摘要、关键词、来源站点、收录时间、最后访问时间等标准元数据，并支持自定义扩展字段，适配不同业务场景。

全文与字段级检索：基于 SQLite 或 PostgreSQL 后端的全文检索引擎，支持对标题、摘要、分类、标签及自定义字段的精确与模糊查询。

访问状态监测：定时对已收录链接进行 HTTP 状态检查，自动标记失效链接、重定向链接及响应异常的链接，辅助用户清理无效资源。

数据导入导出：支持将链接数据导出为 Markdown 表格、CSV 及结构化 JSON 格式，便于备份、迁移或集成至其他文档系统。

权限与多用户支持：基于角色的访问控制，允许管理员、编辑者与查看者三种角色协同工作，适合团队内部共享资源库。

可视化统计面板：提供链接总数、分类分布、标签云、访问成功率及每日新增趋势等统计图表，帮助管理者了解资源库整体状况。

## 应用场景

技术文档中心资源汇总：技术文档团队可使用 LinkMaster Pro 统一管理 API 参考文档、SDK 下载地址、第三方库主页及社区讨论帖链接，在编写新版本文档时快速引用外部依据。

行业研究报告素材整理：行业分析师在撰写深度报告时，需收集大量新闻报道、统计数据、白皮书及竞品分析页面。LinkMaster Pro 的分类与标签功能可帮助分析师按主题、时间线及重要程度组织素材，确保报告引用准确可溯。

运维知识库外部依赖记录：运维团队负责维护服务部署、监控告警及故障处理手册，其中包含大量对外部依赖服务状态页、补丁下载地址及官方公告的引用。LinkMaster Pro 的访问状态监测功能可自动提醒依赖地址变更或失效，减少故障排查时的信息滞后。

开源项目 README 链接维护：开源项目维护者通常需要在 README 中列出相关资源、教程及社区链接。LinkMaster Pro 可生成标准化的 Markdown 链接列表，直接复制至项目文档，确保格式统一且版本可追踪。

## 快速开始

以下命令适用于 Linux 与 macOS 环境。Windows 用户建议使用 WSL2 或 Git Bash 执行。

```bash
# 克隆代码仓库
git clone https://github.com/your-org/linkmaster-pro.git

# 进入项目目录
cd linkmaster-pro

# 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化 SQLite 数据库并创建默认分类
python manage.py migrate
python manage.py init_categories

# 运行开发服务器
python manage.py runserver --host 0.0.0.0 --port 8080
```

访问 http://localhost:8080 即可进入 LinkMaster Pro 管理界面。默认管理员账号为 admin，密码为 admin123，首次登录后请立即修改。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，建议使用 3.10 LTS 版本 |
| SQLite | 3.35 及以上 | 默认数据库，适用于小型及中型部署场景 |
| PostgreSQL | 14.0 及以上 | 生产环境推荐，支持高并发与高级全文检索功能 |
| Redis | 6.2 及以上 | 可选，用于缓存统计数据和任务队列，提升性能 |
| Node.js | 18.0 及以上 | 仅用于前端静态资源构建，后端运行不依赖 |
| Nginx | 1.22 及以上 | 生产环境反向代理与静态文件服务建议部署 |
| Supervisor | 4.0 及以上 | 进程守护工具，用于生产环境保持服务持续运行 |
| Git | 2.30 及以上 | 代码版本管理与增量更新必需 |
| Docker | 20.10 及以上 | 容器化部署方式可选，提供一致的运行环境 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/quickstart.md | 如何在三分钟内完成安装并导入第一批链接 |
| 用户手册 | docs/user-guide/ | 分类管理、标签编辑、批量操作、检索与导出等全部用户功能详解 |
| 管理员手册 | docs/admin-guide/ | 用户权限配置、数据库备份、状态监测任务调度及系统性能调优 |
| 开发者文档 | docs/developer/ | API 接口规范、插件扩展机制、自定义元数据模型及前端主题开发指南 |
| 部署运维 | docs/deployment/ | 基于 Docker Compose 的生产环境部署、日志收集、监控告警配置 |
| 常见问题 | docs/faq.md | 收录运行时错误、数据库迁移失败、性能瓶颈等高频问题的解决方案 |

## 资源列表

- http://www.read.xwpxi.com/Article/70472.shtml
- http://www.read.xwpxi.com/Article/632972.shtml
- http://www.read.xwpxi.com/Article/4691.shtml
- http://www.read.xwpxi.com/Article/84778.shtml
- http://www.read.xwpxi.com/Article/45188.shtml
- http://www.read.xwpxi.com/Article/858366.shtml
- http://www.read.xwpxi.com/Article/45404.shtml
- http://www.read.xwpxi.com/Article/4401329.shtml
- http://www.read.xwpxi.com/Article/6327.shtml
- http://www.read.xwpxi.com/Article/83905.shtml
- http://www.read.xwpxi.com/Article/898295.shtml
- http://www.read.xwpxi.com/Article/6700.shtml
- http://www.read.xwpxi.com/Article/48426.shtml
- http://www.read.xwpxi.com/Article/07900.shtml
- http://www.read.xwpxi.com/Article/55949.shtml
- http://www.read.xwpxi.com/Article/086087.shtml
- http://www.read.xwpxi.com/Article/7218.shtml
- http://www.read.xwpxi.com/Article/3353209.shtml
- http://www.read.xwpxi.com/Article/352608.shtml
- http://www.read.xwpxi.com/Article/4160141.shtml
- http://www.read.xwpxi.com/Article/1591.shtml
- http://www.read.xwpxi.com/Article/2157126.shtml
- http://www.read.xwpxi.com/Article/8169256.shtml
- http://www.read.xwpxi.com/Article/08892.shtml
- http://www.read.xwpxi.com/Article/592536.shtml
- http://www.read.xwpxi.com/Article/2466.shtml
- http://www.read.xwpxi.com/Article/39557.shtml
- http://www.read.xwpxi.com/Article/459092.shtml
- http://www.read.xwpxi.com/Article/81415.shtml
- http://www.read.xwpxi.com/Article/0493.shtml
- http://www.read.xwpxi.com/Article/35836.shtml
- http://www.read.xwpxi.com/Article/4254082.shtml
- http://www.read.xwpxi.com/Article/964283.shtml
- http://www.read.xwpxi.com/Article/9111.shtml
- http://www.read.xwpxi.com/Article/3546.shtml
- http://www.read.xwpxi.com/Article/994314.shtml
- http://www.read.xwpxi.com/Article/4338451.shtml
- http://www.read.xwpxi.com/Article/18184.shtml
- http://www.read.xwpxi.com/Article/45175.shtml
- http://www.read.xwpxi.com/Article/661721.shtml
- http://www.read.xwpxi.com/Article/51428.shtml
- http://www.read.xwpxi.com/Article/817012.shtml
- http://www.read.xwpxi.com/Article/5324.shtml
- http://www.read.xwpxi.com/Article/17694.shtml
- http://www.read.xwpxi.com/Article/0959677.shtml
- http://www.read.xwpxi.com/Article/6541.shtml
- http://www.read.xwpxi.com/Article/88705.shtml
- http://www.read.xwpxi.com/Article/6038808.shtml
- http://www.read.xwpxi.com/Article/2731.shtml
- http://www.read.xwpxi.com/Article/9991.shtml
- http://www.read.xwpxi.com/Article/1873.shtml
- http://www.read.xwpxi.com/Article/264337.shtml
- http://www.read.xwpxi.com/Article/712139.shtml
- http://www.read.xwpxi.com/Article/9239435.shtml
- http://www.read.xwpxi.com/Article/5226156.shtml
- http://www.read.xwpxi.com/Article/1624.shtml
- http://www.read.xwpxi.com/Article/15677.shtml
- http://www.read.xwpxi.com/Article/82021.shtml
- http://www.read.xwpxi.com/Article/4919.shtml
- http://www.read.xwpxi.com/Article/0416.shtml
- http://www.read.xwpxi.com/Article/8689.shtml
- http://www.read.xwpxi.com/Article/03245.shtml
- http://www.read.xwpxi.com/Article/4255.shtml
- http://www.read.xwpxi.com/Article/5049.shtml
- http://www.read.xwpxi.com/Article/5065716.shtml
- http://www.read.xwpxi.com/Article/4984.shtml
- http://www.read.xwpxi.com/Article/3684747.shtml
- http://www.read.xwpxi.com/Article/150491.shtml
- http://www.read.xwpxi.com/Article/890408.shtml
- http://www.read.xwpxi.com/Article/01869.shtml
- http://www.read.xwpxi.com/Article/3484469.shtml
- http://www.read.xwpxi.com/Article/3689.shtml
- http://www.read.xwpxi.com/Article/5747693.shtml
- http://www.read.xwpxi.com/Article/167165.shtml
- http://www.read.xwpxi.com/Article/4090487.shtml
- http://www.read.xwpxi.com/Article/048991.shtml
- http://www.read.xwpxi.com/Article/161238.shtml
- http://www.read.xwpxi.com/Article/0962.shtml
- http://www.read.xwpxi.com/Article/2428.shtml
- http://www.read.xwpxi.com/Article/551876.shtml
- http://www.read.xwpxi.com/Article/0445662.shtml
- http://www.read.xwpxi.com/Article/4420855.shtml
- http://www.read.xwpxi.com/Article/8572073.shtml
- http://www.read.xwpxi.com/Article/0092.shtml
- http://www.read.xwpxi.com/Article/355064.shtml
- http://www.read.xwpxi.com/Article/296890.shtml
- http://www.read.xwpxi.com/Article/244032.shtml
- http://www.read.xwpxi.com/Article/3731761.shtml
- http://www.read.xwpxi.com/Article/8109011.shtml
- http://www.read.xwpxi.com/Article/4427521.shtml
- http://www.read.xwpxi.com/Article/8938.shtml
- http://www.read.xwpxi.com/Article/8438.shtml
- http://www.read.xwpxi.com/Article/945979.shtml
- http://www.read.xwpxi.com/Article/1882.shtml
- http://www.read.xwpxi.com/Article/6922602.shtml
- http://www.read.xwpxi.com/Article/657551.shtml
- http://www.read.xwpxi.com/Article/3486474.shtml
- http://www.read.xwpxi.com/Article/0502.shtml
- http://www.read.xwpxi.com/Article/888571.shtml
- http://www.read.xwpxi.com/Article/46723.shtml
- http://www.read.xwpxi.com/Article/0536113.shtml
- http://www.read.xwpxi.com/Article/8384.shtml
- http://www.read.xwpxi.com/Article/922814.shtml
- http://www.read.xwpxi.com/Article/6921447.shtml
- http://www.read.xwpxi.com/Article/055599.shtml
- http://www.read.xwpxi.com/Article/278737.shtml
- http://www.read.xwpxi.com/Article/9571.shtml
- http://www.read.xwpxi.com/Article/434752.shtml
- http://www.read.xwpxi.com/Article/7353.shtml
- http://www.read.xwpxi.com/Article/1531845.shtml
- http://www.read.xwpxi.com/Article/43902.shtml
- http://www.read.xwpxi.com/Article/3686.shtml
- http://www.read.xwpxi.com/Article/125819.shtml
- http://www.read.xwpxi.com/Article/282982.shtml
- http://www.read.xwpxi.com/Article/780567.shtml
- http://www.read.xwpxi.com/Article/99518.shtml
- http://www.read.xwpxi.com/Article/494290.shtml
- http://www.read.xwpxi.com/Article/6296490.shtml
- http://www.read.xwpxi.com/Article/4428439.shtml
- http://www.read.xwpxi.com/Article/7869502.shtml
- http://www.read.xwpxi.com/Article/673179.shtml
- http://www.read.xwpxi.com/Article/857412.shtml
- http://www.read.xwpxi.com/Article/4187.shtml
- http://www.read.xwpxi.com/Article/8764.shtml
- http://www.read.xwpxi.com/Article/44574.shtml
- http://www.read.xwpxi.com/Article/83214.shtml
- http://www.read.xwpxi.com/Article/3860238.shtml
- http://www.read.xwpxi.com/Article/605557.shtml
- http://www.read.xwpxi.com/Article/2280636.shtml
- http://www.read.xwpxi.com/Article/0000028.shtml
- http://www.read.xwpxi.com/Article/572975.shtml
- http://www.read.xwpxi.com/Article/0528.shtml
- http://www.read.xwpxi.com/Article/4605996.shtml
- http://www.read.xwpxi.com/Article/3590113.shtml
- http://www.read.xwpxi.com/Article/4501.shtml
- http://www.read.xwpxi.com/Article/5827.shtml
- http://www.read.xwpxi.com/Article/8291223.shtml
- http://www.read.xwpxi.com/Article/50002.shtml
- http://www.read.xwpxi.com/Article/213296.shtml
- http://www.read.xwpxi.com/Article/11344.shtml
- http://www.read.xwpxi.com/Article/2174.shtml
- http://www.read.xwpxi.com/Article/1557.shtml
- http://www.read.xwpxi.com/Article/4484.shtml
- http://www.read.xwpxi.com/Article/345020.shtml
- http://www.read.xwpxi.com/Article/86888.shtml
- http://www.read.xwpxi.com/Article/45904.shtml
- http://www.read.xwpxi.com/Article/07710.shtml
- http://www.read.xwpxi.com/Article/399969.shtml
- http://www.read.xwpxi.com/Article/012919.shtml
- http://www.read.xwpxi.com/Article/5430.shtml
- http://www.read.xwpxi.com/Article/878076.shtml
- http://www.read.xwpxi.com/Article/183180.shtml
- http://www.read.xwpxi.com/Article/80825.shtml
- http://www.read.xwpxi.com/Article/4339.shtml
- http://www.read.xwpxi.com/Article/31983.shtml
- http://www.read.xwpxi.com/Article/9031226.shtml
- http://www.read.xwpxi.com/Article/0563634.shtml
- http://www.read.xwpxi.com/Article/47913.shtml
- http://www.read.xwpxi.com/Article/02785.shtml
- http://www.read.xwpxi.com/Article/199761.shtml
- http://www.read.xwpxi.com/Article/5639.shtml
- http://www.read.xwpxi.com/Article/64658.shtml
- http://www.read.xwpxi.com/Article/64261.shtml
- http://www.read.xwpxi.com/Article/7736.shtml
- http://www.read.xwpxi.com/Article/5031901.shtml
- http://www.read.xwpxi.com/Article/8451927.shtml
- http://www.read.xwpxi.com/Article/159318.shtml
- http://www.read.xwpxi.com/Article/8896944.shtml
- http://www.read.xwpxi.com/Article/710705.shtml
- http://www.read.xwpxi.com/Article/755551.shtml
- http://www.read.xwpxi.com/Article/6615.shtml
- http://www.read.xwpxi.com/Article/7874.shtml
- http://www.read.xwpxi.com/Article/1513151.shtml
- http://www.read.xwpxi.com/Article/6259063.shtml
- http://www.read.xwpxi.com/Article/28321.shtml
- http://www.read.xwpxi.com/Article/6728161.shtml
- http://www.read.xwpxi.com/Article/776647.shtml
- http://www.read.xwpxi.com/Article/5408.shtml
- http://www.read.xwpxi.com/Article/86116.shtml
- http://www.read.xwpxi.com/Article/8893705.shtml
- http://www.read.xwpxi.com/Article/2539345.shtml
- http://www.read.xwpxi.com/Article/1838057.shtml
- http://www.read.xwpxi.com/Article/90398.shtml
- http://www.read.xwpxi.com/Article/19194.shtml
- http://www.read.xwpxi.com/Article/287204.shtml
- http://www.read.xwpxi.com/Article/3478303.shtml
- http://www.read.xwpxi.com/Article/48178.shtml
- http://www.read.xwpxi.com/Article/7294153.shtml
- http://www.read.xwpxi.com/Article/44178.shtml
- http://www.read.xwpxi.com/Article/62301.shtml
- http://www.read.xwpxi.com/Article/8335973.shtml
- http://www.read.xwpxi.com/Article/889891.shtml
- http://www.read.xwpxi.com/Article/7347727.shtml
- http://www.read.xwpxi.com/Article/41868.shtml
- http://www.read.xwpxi.com/Article/517147.shtml
- http://www.read.xwpxi.com/Article/9565749.shtml
- http://www.read.xwpxi.com/Article/7745.shtml
- http://www.read.xwpxi.com/Article/7575815.shtml
- http://www.read.xwpxi.com/Article/4267.shtml
- http://www.read.xwpxi.com/Article/3185.shtml
- http://www.read.xwpxi.com/Article/819986.shtml
- http://www.read.xwpxi.com/Article/7960195.shtml
- http://www.read.xwpxi.com/Article/6678.shtml
- http://www.read.xwpxi.com/Article/088992.shtml
- http://www.read.xwpxi.com/Article/70023.shtml
- http://www.read.xwpxi.com/Article/9406422.shtml
- http://www.read.xwpxi.com/Article/64278.shtml
- http://www.read.xwpxi.com/Article/82461.shtml
- http://www.read.xwpxi.com/Article/10115.shtml
- http://www.read.xwpxi.com/Article/02614.shtml
- http://www.read.xwpxi.com/Article/836062.shtml
- http://www.read.xwpxi.com/Article/06263.shtml
- http://www.read.xwpxi.com/Article/4212.shtml
- http://www.read.xwpxi.com/Article/372767.shtml
- http://www.read.xwpxi.com/Article/63262.shtml
- http://www.read.xwpxi.com/Article/187823.shtml
- http://www.read.xwpxi.com/Article/581283.shtml
- http://www.read.xwpxi.com/Article/609343.shtml
- http://www.read.xwpxi.com/Article/53916.shtml
- http://www.read.xwpxi.com/Article/7690.shtml
- http://www.read.xwpxi.com/Article/78395.shtml
- http://www.read.xwpxi.com/Article/4205803.shtml
- http://www.read.xwpxi.com/Article/05458.shtml
- http://www.read.xwpxi.com/Article/50869.shtml
- http://www.read.xwpxi.com/Article/5535829.shtml
- http://www.read.xwpxi.com/Article/1450.shtml
- http://www.read.xwpxi.com/Article/217384.shtml
- http://www.read.xwpxi.com/Article/7749.shtml
- http://www.read.xwpxi.com/Article/3715538.shtml
- http://www.read.xwpxi.com/Article/15440.shtml
- http://www.read.xwpxi.com/Article/852479.shtml
- http://www.read.xwpxi.com/Article/8682869.shtml
- http://www.read.xwpxi.com/Article/86118.shtml
- http://www.read.xwpxi.com/Article/6130854.shtml
- http://www.read.xwpxi.com/Article/72889.shtml
- http://www.read.xwpxi.com/Article/6711.shtml
- http://www.read.xwpxi.com/Article/8573546.shtml
- http://www.read.xwpxi.com/Article/0646824.shtml
- http://www.read.xwpxi.com/Article/5642.shtml
- http://www.read.xwpxi.com/Article/623731.shtml
- http://www.read.xwpxi.com/Article/126812.shtml
- http://www.read.xwpxi.com/Article/86160.shtml
- http://www.read.xwpxi.com/Article/134277.shtml
- http://www.read.xwpxi.com/Article/174622.shtml
- http://www.read.xwpxi.com/Article/0496857.shtml
- http://www.read.xwpxi.com/Article/62298.shtml
- http://www.read.xwpxi.com/Article/5410.shtml
- http://www.read.xwpxi.com/Article/465021.shtml
- http://www.read.xwpxi.com/Article/9178.shtml
- http://www.read.xwpxi.com/Article/9585600.shtml

## 项目结构

```
linkmaster-pro/
├── backend/                           # 后端核心代码目录
│   ├── api/                           # RESTful API 路由与视图函数
│   │   ├── v1/                        # API 版本 v1 端点
│   │   │   ├── links.py               # 链接资源的增删改查及导入导出接口
│   │   │   ├── categories.py          # 分类管理接口，支持树形结构
│   │   │   └── stats.py               # 统计与状态监测数据接口
│   │   └── middleware/                # 认证、日志、跨域等中间件
│   ├── core/                          # 核心业务逻辑层
│   │   ├── link_parser.py             # URL 解析、元数据提取与去重算法
│   │   ├── health_checker.py          # 异步 HTTP 状态监测任务调度器
│   │   └── export_generator.py        # Markdown/CSV/JSON 导出格式生成器
│   ├── models/                        # 数据库模型定义
│   │   ├── link.py                    # 链接主表，包含 URL、标题、摘要等字段
│   │   ├── category.py                # 分类表，支持父子级关联
│   │   └── user.py                    # 用户表及角色权限关联
│   ├── migrations/                    # 数据库迁移脚本（Alembic 管理）
│   └── config/                        # 环境配置（开发、测试、生产）
├── frontend/                          # 前端静态资源与模板
│   ├── templates/                     # Jinja2 后端渲染模板
│   │   ├── dashboard.html             # 统计面板页面模板
│   │   ├── link_list.html             # 链接列表与检索页面
│   │   └── import_export.html         # 批量导入导出操作页面
│   ├── static/                        # 编译后的 CSS、JavaScript 及图片资源
│   │   ├── css/                       # 基于 Tailwind 的自定义样式
│   │   └── js/                        # 前端交互逻辑，包含搜索与分页组件
│   └── components/                    # 可复用的 Vue 组件（若使用前端框架）
├── scripts/                           # 运维与辅助脚本
│   ├── backup_db.sh                   # 数据库每日备份脚本
│   ├── batch_import.py                # 命令行批量导入工具
│   └── health_check_cron.py           # 状态监测定时任务入口
├── tests/                             # 单元测试与集成测试
│   ├── test_models.py                 # 模型层测试用例
│   ├── test_api.py                    # API 端点测试
│   └── test_parser.py                 # 链接解析器测试
├── docs/                              # 完整项目文档（参见文档导航章节）
├── docker-compose.yml                 # 生产级容器编排配置（包含 PostgreSQL + Redis）
├── Dockerfile                         # 后端服务容器构建文件
├── requirements.txt                   # Python 依赖清单
├── manage.py                          # 命令行管理入口（迁移、创建用户、初始化数据）
└── README.md                          # 本文件
```

## 贡献指南

确认现有 Issue 与 Pull Request：在提交新功能或修复之前，请查阅 GitHub Issues 与 Pull Requests 列表，确认无人正在处理相同问题，避免重复工作。

Fork 仓库并创建功能分支：从主仓库 Fork 至个人账户，然后基于 main 分支创建新的功能分支，分支命名遵循 feature/xxx 或 fix/xxx 格式。

编写测试用例并通过全部测试：新增代码需同步编写对应的单元测试，确保 tests/ 目录下的测试覆盖率不低于现有水平。执行 pytest 命令验证所有测试通过。

提交清晰规范的 Commit 信息：Commit 消息采用 Conventional Commits 格式，例如 feat: add batch import from JSON，并附上简要说明改动原因与影响范围。

发起 Pull Request 并描述改动：向主仓库的 main 分支发起 PR，在描述中详细说明改动目的、实现方式及测试情况，至少需要一位项目维护者审核通过方可合并。

## 常见问题

Q：导入包含大量链接的 CSV 文件时出现超时错误，如何解决？

A：LinkMaster Pro 默认单次导入上限为 500 条记录，超过此数量建议使用命令行导入工具 scripts/batch_import.py，该工具支持分批次提交并显示进度。若仍需通过 Web 界面导入，可修改 backend/config/settings.py 中的 IMPORT_BATCH_SIZE 参数，调低每批处理数量，同时增加 nginx 与 uwsgi 的超时时间配置。

Q：状态监测任务发现大量链接被标记为失效，但手动访问浏览器可以打开，原因是什么？

A：状态监测默认使用 HEAD 请求方法检查响应码，部分网站对 HEAD 请求返回 405 或 403，但对 GET 请求正常响应。您可以在后台管理界面的监测配置中将请求方法切换为 GET，或设置自定义 User-Agent 以模拟浏览器访问。此外，若目标站点存在反爬机制，可适当增加监测间隔时间，避免频繁请求触发限制。

Q：如何将 LinkMaster Pro 的数据迁移至另一台服务器？

A：迁移工作分为数据库与静态文件两部分。数据库方面，若使用 SQLite，直接复制 db.sqlite3 文件至新服务器即可；若使用 PostgreSQL，执行 pg_dump 导出再导入。静态文件（如用户上传的附件或自定义图标）位于 storage/ 目录，建议使用 rsync 同步。完成数据迁移后，新服务器需重新执行 python manage.py migrate 确保表结构一致，并检查配置文件中数据库连接字符串与存储路径是否正确。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
