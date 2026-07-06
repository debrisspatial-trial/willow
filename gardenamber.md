# WebLink Archive Collector

WebLink Archive Collector 是一个面向技术研究、内容追溯与互联网存档分析的开源外链归档与结构化检索工具。该项目主要服务于数字内容研究者、网站运维人员、信息分析工程师以及需要批量处理历史文章链接的开发者群体。其核心定位在于将散落在各类内容平台中的文章级 URL 进行系统化采集、分类存储和元数据增强，并提供统一的查询接口与导出能力，以解决手工整理链接效率低下、缺乏版本追踪、难以批量校验可用性等实际问题。

该项目本身不依赖任何第三方内容源，所有链接均以原始形态入库，保留完整的协议、域名和路径信息。用户可通过该项目构建私有化的外链资源仓库，用于长期保存、定期巡检或进一步的数据挖掘。WebLink Archive Collector 适用于单机部署和轻量级服务器环境，尤其适合需要维护大量外链清单的长期项目。

## 功能概览

批量链接导入 支持从纯文本文件、CSV 或直接粘贴的 URL 列表中批量导入链接记录，自动解析协议、域名、路径与查询参数。

结构化存储引擎 每条链接以独立条目存储，包含原始 URL、采集时间、校验状态、响应码和内容摘要哈希值，便于后续去重与变更检测。

状态监控与可用性检查 提供可配置的定时任务，对已入库的 URL 执行 HTTP 请求测试，记录响应状态、重定向链和加载耗时，生成可用性报表。

分类标签管理 允许用户为链接添加自定义标签和备注字段，支持多标签筛选和组合查询，方便按项目、主题或优先级归类。

全文检索与过滤 基于路径关键词、域名后缀、采集日期范围等多维条件进行快速检索，支持正则表达式匹配，满足精细化筛选需求。

数据导出接口 支持将查询结果导出为 JSON、CSV 或纯文本列表格式，便于对接其他数据处理流水线或生成静态资源清单。

审计日志记录 完整记录所有链接的增删改操作、校验历史以及用户登录行为，满足内部审计与操作追溯要求。

## 应用场景

内容归档项目的链接清单维护 研究机构或自媒体运营者在整理历史文章时，可将涉及的外部引用链接统一录入系统，定期检查链接是否失效，及时更新或替换已损坏的资源引用。

网站迁移前的资源普查 在进行站点重构或域名更换前，使用该项目批量扫描旧站点中所有内嵌外链，生成完整清单用于评估迁移影响范围和制定重定向策略。

信息安全团队的威胁情报收集 安全分析人员可将可疑域名或文章链接导入系统，通过定时状态监控观察其存活周期、页面变动情况，辅助判断威胁活跃程度。

搜索引擎优化（SEO）的外链审计 运维人员利用该工具对自身站点的外部反向链接进行系统化记录，定期比对链接状态变化，识别被删除或篡改的引用来源。

## 快速开始

以下步骤指导用户在本地环境中完成项目的克隆、安装与初次运行。

```bash
# 克隆项目仓库
git clone https://github.com/weblink-archive/collector.git

# 进入项目目录
cd collector

# 安装项目依赖（基于 Python 3.9+）
pip install -r requirements.txt

# 初始化本地数据库与配置文件
python manage.py init

# 启动内置开发服务器
python manage.py runserver --host 127.0.0.1 --port 8080
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，用于执行采集引擎与 API 服务 |
| SQLite | 3.31.0 及以上 | 默认嵌入式数据库，用于存储链接记录与元数据 |
| requests | 2.28.0 及以上 | 处理 HTTP 请求，用于链接可用性校验 |
| click | 8.1.0 及以上 | 命令行交互框架，提供管理命令解析 |
| PyYAML | 6.0 及以上 | 解析配置文件，支持用户自定义参数 |
| pytest | 7.0 及以上 | 单元测试框架，仅在开发环境中需要 |
| flask | 2.2.0 及以上 | 提供 Web API 接口，用于查询与导出功能 |
| gunicorn | 20.1.0 及以上 | 生产环境推荐的 WSGI 服务器（可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user_guide.md | 如何配置采集规则、执行批量导入以及查看状态报表 |
| 开发者指南 | docs/developer_guide.md | 如何扩展新的校验器、自定义标签插件或修改数据库模型 |
| API 参考 | docs/api_reference.md | 所有 RESTful 接口的请求参数、返回格式与错误码说明 |
| 运维部署 | docs/deployment.md | 如何将项目部署到 Linux 服务器、配置 systemd 服务与 Nginx 反向代理 |

## 资源列表

- http://www.read.xwpxi.com/Article/642035.shtml
- http://www.read.xwpxi.com/Article/0499.shtml
- http://www.read.xwpxi.com/Article/87614.shtml
- http://www.read.xwpxi.com/Article/049073.shtml
- http://www.read.xwpxi.com/Article/291012.shtml
- http://www.read.xwpxi.com/Article/9112.shtml
- http://www.read.xwpxi.com/Article/3699284.shtml
- http://www.read.xwpxi.com/Article/0501100.shtml
- http://www.read.xwpxi.com/Article/4564.shtml
- http://www.read.xwpxi.com/Article/364451.shtml
- http://www.read.xwpxi.com/Article/2091768.shtml
- http://www.read.xwpxi.com/Article/9514169.shtml
- http://www.read.xwpxi.com/Article/6279.shtml
- http://www.read.xwpxi.com/Article/8758723.shtml
- http://www.read.xwpxi.com/Article/061108.shtml
- http://www.read.xwpxi.com/Article/8053398.shtml
- http://www.read.xwpxi.com/Article/5034.shtml
- http://www.read.xwpxi.com/Article/335319.shtml
- http://www.read.xwpxi.com/Article/924015.shtml
- http://www.read.xwpxi.com/Article/6239.shtml
- http://www.read.xwpxi.com/Article/90309.shtml
- http://www.read.xwpxi.com/Article/634698.shtml
- http://www.read.xwpxi.com/Article/6833664.shtml
- http://www.read.xwpxi.com/Article/9647.shtml
- http://www.read.xwpxi.com/Article/0300.shtml
- http://www.read.xwpxi.com/Article/0752248.shtml
- http://www.read.xwpxi.com/Article/7572764.shtml
- http://www.read.xwpxi.com/Article/01711.shtml
- http://www.read.xwpxi.com/Article/7438.shtml
- http://www.read.xwpxi.com/Article/9257.shtml
- http://www.read.xwpxi.com/Article/841796.shtml
- http://www.read.xwpxi.com/Article/915877.shtml
- http://www.read.xwpxi.com/Article/15758.shtml
- http://www.read.xwpxi.com/Article/9449909.shtml
- http://www.read.xwpxi.com/Article/2280.shtml
- http://www.read.xwpxi.com/Article/03261.shtml
- http://www.read.xwpxi.com/Article/429436.shtml
- http://www.read.xwpxi.com/Article/86571.shtml
- http://www.read.xwpxi.com/Article/05469.shtml
- http://www.read.xwpxi.com/Article/92498.shtml
- http://www.read.xwpxi.com/Article/742949.shtml
- http://www.read.xwpxi.com/Article/1569737.shtml
- http://www.read.xwpxi.com/Article/32081.shtml
- http://www.read.xwpxi.com/Article/5917.shtml
- http://www.read.xwpxi.com/Article/4116.shtml
- http://www.read.xwpxi.com/Article/7489.shtml
- http://www.read.xwpxi.com/Article/238585.shtml
- http://www.read.xwpxi.com/Article/18424.shtml
- http://www.read.xwpxi.com/Article/824888.shtml
- http://www.read.xwpxi.com/Article/4298656.shtml
- http://www.read.xwpxi.com/Article/7783.shtml
- http://www.read.xwpxi.com/Article/674705.shtml
- http://www.read.xwpxi.com/Article/564065.shtml
- http://www.read.xwpxi.com/Article/453069.shtml
- http://www.read.xwpxi.com/Article/656751.shtml
- http://www.read.xwpxi.com/Article/892628.shtml
- http://www.read.xwpxi.com/Article/4793.shtml
- http://www.read.xwpxi.com/Article/9692981.shtml
- http://www.read.xwpxi.com/Article/6304.shtml
- http://www.read.xwpxi.com/Article/1123.shtml
- http://www.read.xwpxi.com/Article/52710.shtml
- http://www.read.xwpxi.com/Article/5262.shtml
- http://www.read.xwpxi.com/Article/6489.shtml
- http://www.read.xwpxi.com/Article/6508.shtml
- http://www.read.xwpxi.com/Article/8492503.shtml
- http://www.read.xwpxi.com/Article/304634.shtml
- http://www.read.xwpxi.com/Article/96077.shtml
- http://www.read.xwpxi.com/Article/12684.shtml
- http://www.read.xwpxi.com/Article/63035.shtml
- http://www.read.xwpxi.com/Article/5770.shtml
- http://www.read.xwpxi.com/Article/4157229.shtml
- http://www.read.xwpxi.com/Article/15652.shtml
- http://www.read.xwpxi.com/Article/65023.shtml
- http://www.read.xwpxi.com/Article/77285.shtml
- http://www.read.xwpxi.com/Article/7773310.shtml
- http://www.read.xwpxi.com/Article/8280.shtml
- http://www.read.xwpxi.com/Article/034101.shtml
- http://www.read.xwpxi.com/Article/49427.shtml
- http://www.read.xwpxi.com/Article/754039.shtml
- http://www.read.xwpxi.com/Article/9775763.shtml
- http://www.read.xwpxi.com/Article/204706.shtml
- http://www.read.xwpxi.com/Article/859551.shtml
- http://www.read.xwpxi.com/Article/8223253.shtml
- http://www.read.xwpxi.com/Article/9287925.shtml
- http://www.read.xwpxi.com/Article/037542.shtml
- http://www.read.xwpxi.com/Article/986875.shtml
- http://www.read.xwpxi.com/Article/52931.shtml
- http://www.read.xwpxi.com/Article/4012973.shtml
- http://www.read.xwpxi.com/Article/7452.shtml
- http://www.read.xwpxi.com/Article/8655.shtml
- http://www.read.xwpxi.com/Article/0432.shtml
- http://www.read.xwpxi.com/Article/9287413.shtml
- http://www.read.xwpxi.com/Article/83437.shtml
- http://www.read.xwpxi.com/Article/6259917.shtml
- http://www.read.xwpxi.com/Article/396230.shtml
- http://www.read.xwpxi.com/Article/2795547.shtml
- http://www.read.xwpxi.com/Article/259807.shtml
- http://www.read.xwpxi.com/Article/1941112.shtml
- http://www.read.xwpxi.com/Article/3831.shtml
- http://www.read.xwpxi.com/Article/7641626.shtml
- http://www.read.xwpxi.com/Article/500040.shtml
- http://www.read.xwpxi.com/Article/1697203.shtml
- http://www.read.xwpxi.com/Article/3088.shtml
- http://www.read.xwpxi.com/Article/2024037.shtml
- http://www.read.xwpxi.com/Article/237098.shtml
- http://www.read.xwpxi.com/Article/0507.shtml
- http://www.read.xwpxi.com/Article/6358396.shtml
- http://www.read.xwpxi.com/Article/151564.shtml
- http://www.read.xwpxi.com/Article/4626.shtml
- http://www.read.xwpxi.com/Article/38917.shtml
- http://www.read.xwpxi.com/Article/5742.shtml
- http://www.read.xwpxi.com/Article/40268.shtml
- http://www.read.xwpxi.com/Article/0838210.shtml
- http://www.read.xwpxi.com/Article/6505800.shtml
- http://www.read.xwpxi.com/Article/612650.shtml
- http://www.read.xwpxi.com/Article/206008.shtml
- http://www.read.xwpxi.com/Article/469134.shtml
- http://www.read.xwpxi.com/Article/4618495.shtml
- http://www.read.xwpxi.com/Article/5635873.shtml
- http://www.read.xwpxi.com/Article/13390.shtml
- http://www.read.xwpxi.com/Article/2162.shtml
- http://www.read.xwpxi.com/Article/403837.shtml
- http://www.read.xwpxi.com/Article/8120.shtml
- http://www.read.xwpxi.com/Article/177398.shtml
- http://www.read.xwpxi.com/Article/8260147.shtml
- http://www.read.xwpxi.com/Article/0787.shtml
- http://www.read.xwpxi.com/Article/23579.shtml
- http://www.read.xwpxi.com/Article/712403.shtml
- http://www.read.xwpxi.com/Article/536604.shtml
- http://www.read.xwpxi.com/Article/9206.shtml
- http://www.read.xwpxi.com/Article/25292.shtml
- http://www.read.xwpxi.com/Article/6893.shtml
- http://www.read.xwpxi.com/Article/5650.shtml
- http://www.read.xwpxi.com/Article/6925143.shtml
- http://www.read.xwpxi.com/Article/4729212.shtml
- http://www.read.xwpxi.com/Article/34269.shtml
- http://www.read.xwpxi.com/Article/934388.shtml
- http://www.read.xwpxi.com/Article/7061179.shtml
- http://www.read.xwpxi.com/Article/5578.shtml
- http://www.read.xwpxi.com/Article/4471078.shtml
- http://www.read.xwpxi.com/Article/07533.shtml
- http://www.read.xwpxi.com/Article/8403.shtml
- http://www.read.xwpxi.com/Article/865980.shtml
- http://www.read.xwpxi.com/Article/58377.shtml
- http://www.read.xwpxi.com/Article/2260.shtml
- http://www.read.xwpxi.com/Article/1140919.shtml
- http://www.read.xwpxi.com/Article/079183.shtml
- http://www.read.xwpxi.com/Article/6957423.shtml
- http://www.read.xwpxi.com/Article/808450.shtml
- http://www.read.xwpxi.com/Article/1785.shtml
- http://www.read.xwpxi.com/Article/361784.shtml
- http://www.read.xwpxi.com/Article/559591.shtml
- http://www.read.xwpxi.com/Article/0537.shtml
- http://www.read.xwpxi.com/Article/7845869.shtml
- http://www.read.xwpxi.com/Article/884874.shtml
- http://www.read.xwpxi.com/Article/3256.shtml
- http://www.read.xwpxi.com/Article/946734.shtml
- http://www.read.xwpxi.com/Article/2614445.shtml
- http://www.read.xwpxi.com/Article/3318.shtml
- http://www.read.xwpxi.com/Article/76303.shtml
- http://www.read.xwpxi.com/Article/5517556.shtml
- http://www.read.xwpxi.com/Article/9368.shtml
- http://www.read.xwpxi.com/Article/464600.shtml
- http://www.read.xwpxi.com/Article/637521.shtml
- http://www.read.xwpxi.com/Article/2221.shtml
- http://www.read.xwpxi.com/Article/8934.shtml
- http://www.read.xwpxi.com/Article/06056.shtml
- http://www.read.xwpxi.com/Article/0396508.shtml
- http://www.read.xwpxi.com/Article/7547.shtml
- http://www.read.xwpxi.com/Article/99155.shtml
- http://www.read.xwpxi.com/Article/6578151.shtml
- http://www.read.xwpxi.com/Article/730864.shtml
- http://www.read.xwpxi.com/Article/1188.shtml
- http://www.read.xwpxi.com/Article/0716127.shtml
- http://www.read.xwpxi.com/Article/0916744.shtml
- http://www.read.xwpxi.com/Article/242577.shtml
- http://www.read.xwpxi.com/Article/7002460.shtml
- http://www.read.xwpxi.com/Article/96750.shtml
- http://www.read.xwpxi.com/Article/8711125.shtml
- http://www.read.xwpxi.com/Article/44054.shtml
- http://www.read.xwpxi.com/Article/0855626.shtml
- http://www.read.xwpxi.com/Article/22302.shtml
- http://www.read.xwpxi.com/Article/46826.shtml
- http://www.read.xwpxi.com/Article/9829.shtml
- http://www.read.xwpxi.com/Article/3893.shtml
- http://www.read.xwpxi.com/Article/272940.shtml
- http://www.read.xwpxi.com/Article/956560.shtml
- http://www.read.xwpxi.com/Article/4953.shtml
- http://www.read.xwpxi.com/Article/767877.shtml
- http://www.read.xwpxi.com/Article/17761.shtml
- http://www.read.xwpxi.com/Article/6008860.shtml
- http://www.read.xwpxi.com/Article/0836829.shtml
- http://www.read.xwpxi.com/Article/7856.shtml
- http://www.read.xwpxi.com/Article/23473.shtml
- http://www.read.xwpxi.com/Article/68483.shtml
- http://www.read.xwpxi.com/Article/8973.shtml
- http://www.read.xwpxi.com/Article/6647024.shtml
- http://www.read.xwpxi.com/Article/3181.shtml
- http://www.read.xwpxi.com/Article/55611.shtml
- http://www.read.xwpxi.com/Article/2514.shtml
- http://www.read.xwpxi.com/Article/649961.shtml
- http://www.read.xwpxi.com/Article/17859.shtml
- http://www.read.xwpxi.com/Article/6252.shtml
- http://www.read.xwpxi.com/Article/2828525.shtml
- http://www.read.xwpxi.com/Article/7274.shtml
- http://www.read.xwpxi.com/Article/8956.shtml
- http://www.read.xwpxi.com/Article/1070.shtml
- http://www.read.xwpxi.com/Article/143192.shtml
- http://www.read.xwpxi.com/Article/6446931.shtml
- http://www.read.xwpxi.com/Article/5270.shtml
- http://www.read.xwpxi.com/Article/241207.shtml
- http://www.read.xwpxi.com/Article/6787.shtml
- http://www.read.xwpxi.com/Article/0629.shtml
- http://www.read.xwpxi.com/Article/416444.shtml
- http://www.read.xwpxi.com/Article/64893.shtml
- http://www.read.xwpxi.com/Article/85039.shtml
- http://www.read.xwpxi.com/Article/477723.shtml
- http://www.read.xwpxi.com/Article/1967194.shtml
- http://www.read.xwpxi.com/Article/4576.shtml
- http://www.read.xwpxi.com/Article/97730.shtml
- http://www.read.xwpxi.com/Article/5457.shtml
- http://www.read.xwpxi.com/Article/489590.shtml
- http://www.read.xwpxi.com/Article/409293.shtml
- http://www.read.xwpxi.com/Article/8511.shtml
- http://www.read.xwpxi.com/Article/90255.shtml
- http://www.read.xwpxi.com/Article/562397.shtml
- http://www.read.xwpxi.com/Article/996622.shtml
- http://www.read.xwpxi.com/Article/494722.shtml
- http://www.read.xwpxi.com/Article/566906.shtml
- http://www.read.xwpxi.com/Article/85686.shtml
- http://www.read.xwpxi.com/Article/992881.shtml
- http://www.read.xwpxi.com/Article/0222533.shtml
- http://www.read.xwpxi.com/Article/427765.shtml
- http://www.read.xwpxi.com/Article/43096.shtml
- http://www.read.xwpxi.com/Article/8880.shtml
- http://www.read.xwpxi.com/Article/13899.shtml
- http://www.read.xwpxi.com/Article/0933888.shtml
- http://www.read.xwpxi.com/Article/312056.shtml
- http://www.read.xwpxi.com/Article/2203.shtml
- http://www.read.xwpxi.com/Article/31103.shtml
- http://www.read.xwpxi.com/Article/398902.shtml
- http://www.read.xwpxi.com/Article/32242.shtml
- http://www.read.xwpxi.com/Article/080408.shtml
- http://www.read.xwpxi.com/Article/75962.shtml
- http://www.read.xwpxi.com/Article/9124957.shtml
- http://www.read.xwpxi.com/Article/67853.shtml
- http://www.read.xwpxi.com/Article/101157.shtml
- http://www.read.xwpxi.com/Article/876914.shtml
- http://www.read.xwpxi.com/Article/0640.shtml
- http://www.read.xwpxi.com/Article/7320.shtml

## 项目结构

```
collector/
├── manage.py                 # 项目入口命令行工具，集成初始化、运行与维护指令
├── requirements.txt          # Python 依赖清单，固定所有第三方库版本号
├── config/
│   ├── default.yaml          # 默认配置参数，含数据库路径、校验间隔与日志级别
│   └── custom.yaml.example   # 用户自定义配置模板，用于覆盖默认设置
├── collector/
│   ├── __init__.py           # 包初始化文件，暴露核心 API 接口
│   ├── models.py             # 数据模型定义，包含链接记录表、标签表与审计日志表
│   ├── engine.py             # 采集与校验引擎，负责执行 HTTP 请求和状态更新
│   ├── importer.py           # 批量导入模块，支持多种输入格式解析
│   ├── exporter.py           # 数据导出模块，支持 JSON、CSV 与纯文本输出
│   ├── scheduler.py          # 定时任务调度器，基于 cron 表达式执行定期校验
│   ├── filters.py            # 查询过滤器，实现标签、路径与时间范围的组合筛选
│   └── utils.py              # 通用工具函数，含 URL 解析、哈希计算与日志辅助
├── web/
│   ├── __init__.py           # Web 服务包初始化
│   ├── app.py                # Flask 应用工厂，注册所有路由与蓝图
│   ├── routes/
│   │   ├── api.py            # RESTful API 路由，提供查询、导入与导出接口
│   │   └── dashboard.py      # 管理后台路由，提供简单的 Web 界面（可选）
│   └── templates/            # HTML 模板目录（仅当启用 Web 界面时使用）
├── tests/
│   ├── test_models.py        # 数据模型单元测试
│   ├── test_engine.py        # 采集引擎功能测试
│   └── test_filters.py       # 查询过滤器逻辑测试
├── scripts/
│   ├── migrate_db.py         # 数据库迁移脚本，用于升级表结构
│   └── seed_sample.py        # 示例数据填充脚本，用于快速演示
└── docs/                     # 完整文档目录，含用户手册与 API 参考
    ├── user_guide.md
    ├── developer_guide.md
    ├── api_reference.md
    └── deployment.md
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库至个人账户，并克隆到本地开发环境。确保本地 Python 版本符合要求且已安装所有开发依赖。

2. 创建新的特性分支，分支名称需反映本次修改的简要内容，例如 `feature/add-http2-support` 或 `fix/batch-import-timeout`。禁止在 main 分支上直接修改。

3. 编写或修改代码后，请补充对应的单元测试用例，并确保所有现有测试通过。新增功能需包含使用示例和参数说明。

4. 提交前执行代码风格检查工具（如 black 和 flake8），保持与项目一致的编码规范。提交信息应遵循语义化提交格式（如 `feat: 增加批量导出进度提示`）。

5. 推送分支至远程仓库，并通过 GitHub 界面发起 Pull Request 到 main 分支。PR 描述中需清晰说明修改目的、实现方式及影响范围，等待项目维护者审核与合并。

## 常见问题

Q: 导入大量链接时出现内存占用过高的情况，如何优化？

A: 建议使用分批导入模式。项目提供的 `importer.py` 模块支持 `--batch-size` 参数，可设置每批处理的记录数量（默认 500）。同时，可降低 SQLite 的缓存大小或切换至 PostgreSQL 等更强大的数据库后端，具体配置参见 `config/default.yaml` 中的数据库连接参数。

Q: 定时校验任务未能按预期时间执行，可能是什么原因？

A: 首先检查系统时区设置与 `scheduler.py` 中配置的 cron 表达式是否一致。其次确认运行调度器的进程是否持续存活，建议在生产环境中使用 systemd 或 supervisor 守护进程。最后查看日志文件 `logs/scheduler.log`，其中会记录每次任务启动、完成或异常中断的详细信息。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
