# WebIndex Curator

WebIndex Curator 是一个面向技术研究者、信息分析人员和内容聚合者的外链资源归集与导航系统。该项目并非简单的书签管理工具，而是一个专注于对松散、海量的外部文章链接进行结构化整理、元数据提取与分类检索的轻量级平台。其核心定位是帮助用户在信息过载的环境中，从大量原始 URL 中快速定位具备阅读价值的特定文章，并通过标签化与快照摘要机制提升后续查阅效率。

本项目适用于需要定期处理大批量链接（例如来自订阅源、爬虫结果或协作分享池）的个体开发者或小型团队。WebIndex Curator 不提供全文代理或内容缓存服务，而是聚焦于链接的准入控制、基础信息清洗与导航层级构建，确保用户能够以最低的时间成本完成从原始链接到有效知识条目的转化流程。

## 功能概览

批量链接导入引擎 支持以纯文本或简单 CSV 格式一次性导入大量 URL，系统自动进行去重与协议规范性检查，剔除无效或不可达的链接条目。

智能元数据抽取 对每条导入的链接自动发起轻量级 HEAD 请求，获取内容类型、最后修改时间及服务器标识，并依据 URL 路径特征生成初步分类标签。

自定义分类树构建 允许用户根据技术领域、主题关键词或项目阶段创建多层级的目录结构，并将链接灵活挂载至一个或多个分类节点下。

全文检索与过滤 基于链接标题、来源域名、抽取标签及用户备注提供即时关键词搜索，同时支持按导入时间、内容类型和访问状态进行组合过滤。

快照摘要卡片 对每个链接自动抓取页面标题与 meta 描述，生成统一格式的摘要卡片，便于用户在不离开系统的情况下快速评估文章相关性。

协作批注与状态标记 支持多用户环境下的批注添加与阅读状态标记（如待读、已读、需跟进、已归档），方便团队共享链接池的进度管理。

数据导入导出标准化 提供 JSON 与 Markdown 两种格式的导出方案，导出的数据可无缝迁移至其他文档系统或静态站点生成器，确保数据的可移植性。

## 应用场景

技术团队周报汇总 开发团队每周需要整理数十篇技术博客、开源公告与性能测试报告。WebIndex Curator 可作为周报预处理层，团队成员将各自发现的链接统一提交至系统，由系统完成分类与摘要生成后，直接导出为 Markdown 格式的周报附件，减少人工编排成本。

爬虫结果人工复审 数据采集流程通常会产生大量候选 URL。运营人员可将爬虫输出的原始链接列表导入 WebIndex Curator，通过系统的元数据抽取与状态标记功能，快速筛除低质量页面，仅保留高价值链接进行深度阅读或二次处理。

个人知识库入口管理 研究者或工程师在浏览信息流时频繁遇到值得后续细读的文章。使用 WebIndex Curator 作为临时收容站，将散落于各处的链接统一收集，并利用分类树和全文检索功能构建个人化的阅读清单，避免依赖浏览器书签的扁平化混乱。

离线文档资源映射 针对需要引用大量外部参考文档的技术写作项目，作者可将所有参考链接导入系统，按章节或论点建立分类映射，并在写作过程中随时通过检索功能找到对应来源，提升引用的规范性与回溯效率。

## 快速开始

以下步骤指导您在本地环境中快速启动 WebIndex Curator 实例。

```bash
# 克隆项目仓库至本地
git clone https://github.com/webindex-curator/webindex-curator.git

# 进入项目根目录
cd webindex-curator

# 安装核心依赖（使用 pip 进行 Python 包管理）
pip install -r requirements.txt

# 执行数据库初始化脚本，创建 SQLite 数据表结构
python scripts/init_db.py

# 启动开发服务器，默认监听 127.0.0.1:5000
python app.py
```

启动成功后，访问 http://127.0.0.1:5000 即可进入系统主界面。首次启动将自动生成管理员账户，初始密码显示于终端日志中，请及时修改。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，建议使用 3.11 长期支持版本 |
| SQLite | 3.35 及以上 | 内嵌数据库，用于存储链接元数据与分类信息 |
| requests | 2.31.0 及以上 | 处理 HTTP 请求，用于元数据抽取过程中的页面头部抓取 |
| beautifulsoup4 | 4.12.0 及以上 | 解析 HTML 页面标题与 meta 描述内容 |
| flask | 2.3.0 及以上 | Web 服务框架，提供 RESTful API 与前端交互接口 |
| flask-cors | 4.0.0 及以上 | 处理跨域资源共享，便于前端独立部署场景 |
| pytest | 7.4.0 及以上 | 单元测试框架，用于运行项目内建测试套件（仅开发环境需要） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/getting-started.md | 如何安装、配置首次启动参数以及登录系统？ |
| 操作手册 | docs/user-guide.md | 如何导入链接、创建分类、生成摘要卡片以及导出数据？ |
| API 参考 | docs/api-reference.md | 系统提供了哪些外部接口供自动化脚本或第三方工具调用？ |
| 架构设计 | docs/architecture.md | 系统的数据模型、模块划分以及元数据抽取流程是如何设计的？ |

## 资源列表

- http://www.read.xwpxi.com/Article/900659.shtml
- http://www.read.xwpxi.com/Article/9071978.shtml
- http://www.read.xwpxi.com/Article/7720948.shtml
- http://www.read.xwpxi.com/Article/5933436.shtml
- http://www.read.xwpxi.com/Article/06497.shtml
- http://www.read.xwpxi.com/Article/96219.shtml
- http://www.read.xwpxi.com/Article/3578796.shtml
- http://www.read.xwpxi.com/Article/5268.shtml
- http://www.read.xwpxi.com/Article/887298.shtml
- http://www.read.xwpxi.com/Article/0670.shtml
- http://www.read.xwpxi.com/Article/7516.shtml
- http://www.read.xwpxi.com/Article/14878.shtml
- http://www.read.xwpxi.com/Article/09754.shtml
- http://www.read.xwpxi.com/Article/725990.shtml
- http://www.read.xwpxi.com/Article/49228.shtml
- http://www.read.xwpxi.com/Article/30336.shtml
- http://www.read.xwpxi.com/Article/9103.shtml
- http://www.read.xwpxi.com/Article/40534.shtml
- http://www.read.xwpxi.com/Article/8218884.shtml
- http://www.read.xwpxi.com/Article/72040.shtml
- http://www.read.xwpxi.com/Article/255135.shtml
- http://www.read.xwpxi.com/Article/093705.shtml
- http://www.read.xwpxi.com/Article/4369004.shtml
- http://www.read.xwpxi.com/Article/0227318.shtml
- http://www.read.xwpxi.com/Article/233569.shtml
- http://www.read.xwpxi.com/Article/298294.shtml
- http://www.read.xwpxi.com/Article/5089654.shtml
- http://www.read.xwpxi.com/Article/6672.shtml
- http://www.read.xwpxi.com/Article/1912380.shtml
- http://www.read.xwpxi.com/Article/969542.shtml
- http://www.read.xwpxi.com/Article/1549737.shtml
- http://www.read.xwpxi.com/Article/06944.shtml
- http://www.read.xwpxi.com/Article/461712.shtml
- http://www.read.xwpxi.com/Article/23246.shtml
- http://www.read.xwpxi.com/Article/18905.shtml
- http://www.read.xwpxi.com/Article/4282848.shtml
- http://www.read.xwpxi.com/Article/660455.shtml
- http://www.read.xwpxi.com/Article/3321.shtml
- http://www.read.xwpxi.com/Article/722971.shtml
- http://www.read.xwpxi.com/Article/78784.shtml
- http://www.read.xwpxi.com/Article/98847.shtml
- http://www.read.xwpxi.com/Article/275638.shtml
- http://www.read.xwpxi.com/Article/3599.shtml
- http://www.read.xwpxi.com/Article/92682.shtml
- http://www.read.xwpxi.com/Article/5630.shtml
- http://www.read.xwpxi.com/Article/70159.shtml
- http://www.read.xwpxi.com/Article/4030809.shtml
- http://www.read.xwpxi.com/Article/4045526.shtml
- http://www.read.xwpxi.com/Article/9526.shtml
- http://www.read.xwpxi.com/Article/05768.shtml
- http://www.read.xwpxi.com/Article/1336774.shtml
- http://www.read.xwpxi.com/Article/6584464.shtml
- http://www.read.xwpxi.com/Article/098913.shtml
- http://www.read.xwpxi.com/Article/70993.shtml
- http://www.read.xwpxi.com/Article/6987.shtml
- http://www.read.xwpxi.com/Article/51357.shtml
- http://www.read.xwpxi.com/Article/9515934.shtml
- http://www.read.xwpxi.com/Article/9713.shtml
- http://www.read.xwpxi.com/Article/7991755.shtml
- http://www.read.xwpxi.com/Article/4127063.shtml
- http://www.read.xwpxi.com/Article/8018935.shtml
- http://www.read.xwpxi.com/Article/9682.shtml
- http://www.read.xwpxi.com/Article/70758.shtml
- http://www.read.xwpxi.com/Article/425188.shtml
- http://www.read.xwpxi.com/Article/5145.shtml
- http://www.read.xwpxi.com/Article/8399.shtml
- http://www.read.xwpxi.com/Article/141406.shtml
- http://www.read.xwpxi.com/Article/662405.shtml
- http://www.read.xwpxi.com/Article/9197.shtml
- http://www.read.xwpxi.com/Article/2499.shtml
- http://www.read.xwpxi.com/Article/1729.shtml
- http://www.read.xwpxi.com/Article/766148.shtml
- http://www.read.xwpxi.com/Article/35095.shtml
- http://www.read.xwpxi.com/Article/290686.shtml
- http://www.read.xwpxi.com/Article/9544.shtml
- http://www.read.xwpxi.com/Article/96981.shtml
- http://www.read.xwpxi.com/Article/1567846.shtml
- http://www.read.xwpxi.com/Article/7554357.shtml
- http://www.read.xwpxi.com/Article/6686.shtml
- http://www.read.xwpxi.com/Article/25391.shtml
- http://www.read.xwpxi.com/Article/17764.shtml
- http://www.read.xwpxi.com/Article/482471.shtml
- http://www.read.xwpxi.com/Article/3676918.shtml
- http://www.read.xwpxi.com/Article/55598.shtml
- http://www.read.xwpxi.com/Article/9877.shtml
- http://www.read.xwpxi.com/Article/2286.shtml
- http://www.read.xwpxi.com/Article/58264.shtml
- http://www.read.xwpxi.com/Article/4979.shtml
- http://www.read.xwpxi.com/Article/50158.shtml
- http://www.read.xwpxi.com/Article/4379.shtml
- http://www.read.xwpxi.com/Article/3524.shtml
- http://www.read.xwpxi.com/Article/17836.shtml
- http://www.read.xwpxi.com/Article/78369.shtml
- http://www.read.xwpxi.com/Article/049505.shtml
- http://www.read.xwpxi.com/Article/95248.shtml
- http://www.read.xwpxi.com/Article/126152.shtml
- http://www.read.xwpxi.com/Article/1622.shtml
- http://www.read.xwpxi.com/Article/3843.shtml
- http://www.read.xwpxi.com/Article/44746.shtml
- http://www.read.xwpxi.com/Article/597785.shtml
- http://www.read.xwpxi.com/Article/541917.shtml
- http://www.read.xwpxi.com/Article/016740.shtml
- http://www.read.xwpxi.com/Article/5706.shtml
- http://www.read.xwpxi.com/Article/941385.shtml
- http://www.read.xwpxi.com/Article/54437.shtml
- http://www.read.xwpxi.com/Article/1996906.shtml
- http://www.read.xwpxi.com/Article/7473484.shtml
- http://www.read.xwpxi.com/Article/91586.shtml
- http://www.read.xwpxi.com/Article/727975.shtml
- http://www.read.xwpxi.com/Article/66400.shtml
- http://www.read.xwpxi.com/Article/4309.shtml
- http://www.read.xwpxi.com/Article/94717.shtml
- http://www.read.xwpxi.com/Article/9227.shtml
- http://www.read.xwpxi.com/Article/2992.shtml
- http://www.read.xwpxi.com/Article/1054429.shtml
- http://www.read.xwpxi.com/Article/689918.shtml
- http://www.read.xwpxi.com/Article/6867.shtml
- http://www.read.xwpxi.com/Article/58679.shtml
- http://www.read.xwpxi.com/Article/3183.shtml
- http://www.read.xwpxi.com/Article/551513.shtml
- http://www.read.xwpxi.com/Article/7133.shtml
- http://www.read.xwpxi.com/Article/4430786.shtml
- http://www.read.xwpxi.com/Article/920580.shtml
- http://www.read.xwpxi.com/Article/1899722.shtml
- http://www.read.xwpxi.com/Article/93004.shtml
- http://www.read.xwpxi.com/Article/3533778.shtml
- http://www.read.xwpxi.com/Article/428682.shtml
- http://www.read.xwpxi.com/Article/209473.shtml
- http://www.read.xwpxi.com/Article/94508.shtml
- http://www.read.xwpxi.com/Article/1445.shtml
- http://www.read.xwpxi.com/Article/65768.shtml
- http://www.read.xwpxi.com/Article/0557307.shtml
- http://www.read.xwpxi.com/Article/507213.shtml
- http://www.read.xwpxi.com/Article/308558.shtml
- http://www.read.xwpxi.com/Article/5931.shtml
- http://www.read.xwpxi.com/Article/1488.shtml
- http://www.read.xwpxi.com/Article/67440.shtml
- http://www.read.xwpxi.com/Article/5892.shtml
- http://www.read.xwpxi.com/Article/1379030.shtml
- http://www.read.xwpxi.com/Article/2186.shtml
- http://www.read.xwpxi.com/Article/2132523.shtml
- http://www.read.xwpxi.com/Article/6545092.shtml
- http://www.read.xwpxi.com/Article/86241.shtml
- http://www.read.xwpxi.com/Article/5449.shtml
- http://www.read.xwpxi.com/Article/5099.shtml
- http://www.read.xwpxi.com/Article/0676910.shtml
- http://www.read.xwpxi.com/Article/3532489.shtml
- http://www.read.xwpxi.com/Article/9175.shtml
- http://www.read.xwpxi.com/Article/2248.shtml
- http://www.read.xwpxi.com/Article/78275.shtml
- http://www.read.xwpxi.com/Article/5404427.shtml
- http://www.read.xwpxi.com/Article/73735.shtml
- http://www.read.xwpxi.com/Article/00721.shtml
- http://www.read.xwpxi.com/Article/55300.shtml
- http://www.read.xwpxi.com/Article/6336393.shtml
- http://www.read.xwpxi.com/Article/784128.shtml
- http://www.read.xwpxi.com/Article/5068325.shtml
- http://www.read.xwpxi.com/Article/1836.shtml
- http://www.read.xwpxi.com/Article/17612.shtml
- http://www.read.xwpxi.com/Article/875730.shtml
- http://www.read.xwpxi.com/Article/6174202.shtml
- http://www.read.xwpxi.com/Article/9069883.shtml
- http://www.read.xwpxi.com/Article/2691.shtml
- http://www.read.xwpxi.com/Article/76716.shtml
- http://www.read.xwpxi.com/Article/8896.shtml
- http://www.read.xwpxi.com/Article/063487.shtml
- http://www.read.xwpxi.com/Article/5276.shtml
- http://www.read.xwpxi.com/Article/7352.shtml
- http://www.read.xwpxi.com/Article/58122.shtml
- http://www.read.xwpxi.com/Article/1038032.shtml
- http://www.read.xwpxi.com/Article/6298127.shtml
- http://www.read.xwpxi.com/Article/871207.shtml
- http://www.read.xwpxi.com/Article/3589252.shtml
- http://www.read.xwpxi.com/Article/613888.shtml
- http://www.read.xwpxi.com/Article/4787341.shtml
- http://www.read.xwpxi.com/Article/9651100.shtml
- http://www.read.xwpxi.com/Article/5536493.shtml
- http://www.read.xwpxi.com/Article/32711.shtml
- http://www.read.xwpxi.com/Article/54629.shtml
- http://www.read.xwpxi.com/Article/9163.shtml
- http://www.read.xwpxi.com/Article/03377.shtml
- http://www.read.xwpxi.com/Article/873974.shtml
- http://www.read.xwpxi.com/Article/4382867.shtml
- http://www.read.xwpxi.com/Article/7240408.shtml
- http://www.read.xwpxi.com/Article/480385.shtml
- http://www.read.xwpxi.com/Article/2370783.shtml
- http://www.read.xwpxi.com/Article/4917.shtml
- http://www.read.xwpxi.com/Article/803690.shtml
- http://www.read.xwpxi.com/Article/47487.shtml
- http://www.read.xwpxi.com/Article/57882.shtml
- http://www.read.xwpxi.com/Article/383317.shtml
- http://www.read.xwpxi.com/Article/5282747.shtml
- http://www.read.xwpxi.com/Article/4526.shtml
- http://www.read.xwpxi.com/Article/754449.shtml
- http://www.read.xwpxi.com/Article/0148.shtml
- http://www.read.xwpxi.com/Article/0437810.shtml
- http://www.read.xwpxi.com/Article/22763.shtml
- http://www.read.xwpxi.com/Article/7960.shtml
- http://www.read.xwpxi.com/Article/93000.shtml
- http://www.read.xwpxi.com/Article/37433.shtml
- http://www.read.xwpxi.com/Article/8721938.shtml
- http://www.read.xwpxi.com/Article/68810.shtml
- http://www.read.xwpxi.com/Article/18026.shtml
- http://www.read.xwpxi.com/Article/139424.shtml
- http://www.read.xwpxi.com/Article/3642548.shtml
- http://www.read.xwpxi.com/Article/9158.shtml
- http://www.read.xwpxi.com/Article/519509.shtml
- http://www.read.xwpxi.com/Article/8702913.shtml
- http://www.read.xwpxi.com/Article/9577799.shtml
- http://www.read.xwpxi.com/Article/6389.shtml
- http://www.read.xwpxi.com/Article/2947633.shtml
- http://www.read.xwpxi.com/Article/386046.shtml
- http://www.read.xwpxi.com/Article/4374197.shtml
- http://www.read.xwpxi.com/Article/0161397.shtml
- http://www.read.xwpxi.com/Article/55337.shtml
- http://www.read.xwpxi.com/Article/314355.shtml
- http://www.read.xwpxi.com/Article/620243.shtml
- http://www.read.xwpxi.com/Article/0540.shtml
- http://www.read.xwpxi.com/Article/3941781.shtml
- http://www.read.xwpxi.com/Article/40862.shtml
- http://www.read.xwpxi.com/Article/73573.shtml
- http://www.read.xwpxi.com/Article/0608944.shtml
- http://www.read.xwpxi.com/Article/7125511.shtml
- http://www.read.xwpxi.com/Article/9475660.shtml
- http://www.read.xwpxi.com/Article/04173.shtml
- http://www.read.xwpxi.com/Article/17097.shtml
- http://www.read.xwpxi.com/Article/01633.shtml
- http://www.read.xwpxi.com/Article/71261.shtml
- http://www.read.xwpxi.com/Article/184228.shtml
- http://www.read.xwpxi.com/Article/852274.shtml
- http://www.read.xwpxi.com/Article/4038.shtml
- http://www.read.xwpxi.com/Article/1083.shtml
- http://www.read.xwpxi.com/Article/9156.shtml
- http://www.read.xwpxi.com/Article/37921.shtml
- http://www.read.xwpxi.com/Article/46821.shtml
- http://www.read.xwpxi.com/Article/206119.shtml
- http://www.read.xwpxi.com/Article/691650.shtml
- http://www.read.xwpxi.com/Article/6056629.shtml
- http://www.read.xwpxi.com/Article/090658.shtml
- http://www.read.xwpxi.com/Article/779387.shtml
- http://www.read.xwpxi.com/Article/6306996.shtml
- http://www.read.xwpxi.com/Article/37616.shtml
- http://www.read.xwpxi.com/Article/1790.shtml
- http://www.read.xwpxi.com/Article/8252646.shtml
- http://www.read.xwpxi.com/Article/0654.shtml
- http://www.read.xwpxi.com/Article/3123.shtml
- http://www.read.xwpxi.com/Article/9813319.shtml
- http://www.read.xwpxi.com/Article/2254.shtml
- http://www.read.xwpxi.com/Article/77245.shtml
- http://www.read.xwpxi.com/Article/78135.shtml

## 项目结构

```
webindex-curator/
├── app/                                # 核心应用包
│   ├── __init__.py                     # 应用工厂函数，初始化 Flask 与扩展
│   ├── routes/                         # 路由蓝本模块
│   │   ├── api.py                      # RESTful API 端点，处理链接增删改查
│   │   └── web.py                      # 页面渲染路由，返回前端 HTML 模板
│   ├── models/                         # 数据模型定义
│   │   ├── link.py                     # Link 实体模型，包含 URL、标题、摘要等字段
│   │   ├── category.py                 # 分类树节点模型，支持无限层级
│   │   └── tag.py                      # 标签模型，用于多对多关联链接
│   ├── services/                       # 业务逻辑服务层
│   │   ├── fetcher.py                  # 元数据抽取服务，负责远程请求与解析
│   │   ├── importer.py                 # 批量导入服务，处理 CSV 与纯文本格式
│   │   └── exporter.py                 # 数据导出服务，生成 JSON 与 Markdown
│   ├── utils/                          # 通用工具函数
│   │   ├── validator.py                # URL 协议校验与规范化工具
│   │   └── logger.py                   # 日志配置与审计记录工具
│   └── static/                         # 前端静态资源
│       ├── css/                        # 样式表文件
│       └── js/                         # 前端交互脚本
├── tests/                              # 单元测试与集成测试套件
│   ├── test_fetcher.py                 # 元数据抽取模块的测试用例
│   └── test_importer.py                # 批量导入功能的测试用例
├── scripts/                            # 运维与辅助脚本
│   ├── init_db.py                      # 数据库初始化与表结构创建脚本
│   └── seed_data.py                    # 预置演示数据填充脚本
├── config/                             # 配置文件目录
│   ├── development.py                  # 开发环境配置
│   └── production.py                   # 生产环境配置模板
├── docs/                               # 项目文档源码
│   ├── getting-started.md              # 入门指南文档
│   └── architecture.md                 # 架构设计说明文档
├── requirements.txt                    # Python 依赖清单
├── setup.py                            # 项目打包与分发配置
└── README.md                           # 项目说明文件（即本文档）
```

## 贡献指南

我们欢迎并鼓励社区贡献者参与 WebIndex Curator 的改进。请遵循以下流程提交您的贡献：

1. 查阅项目 Issue 列表，寻找标记为「help wanted」或「good first issue」的任务。若您有新的功能建议或缺陷报告，请先新建 Issue 并详细描述您的需求或发现，等待核心维护者的反馈与确认。

2. 将项目仓库复刻至您的个人账户，并在本地基于主分支创建新的功能分支。分支命名建议采用 `feature/功能简述` 或 `fix/问题简述` 格式，以便于识别变更目的。

3. 在开发过程中，请遵循项目内建的代码风格规范（PEP 8 标准），并为新增的功能模块编写对应的单元测试用例。确保在提交前运行完整的测试套件，验证所有现有功能未出现回归问题。

4. 提交代码变更时，请编写清晰且具备语义的提交信息，描述本次变更的动机与具体实现方式。若提交关联到某个 Issue，请在提交信息中引用该 Issue 编号。

5. 向主仓库的 `main` 分支发起合并请求。合并请求描述中应包含变更的简要概述、测试覆盖情况以及任何可能影响现有接口的破坏性改动。核心维护者将在代码审查通过后完成合并。

## 常见问题

问题：导入大量链接时，系统响应速度明显变慢，甚至出现超时错误。如何解决？

回答：此现象通常源于元数据抽取过程中的同步远程请求阻塞。系统默认对每条链接依次发起 HEAD 请求，当链接数量超过 100 条时，总耗时将显著增加。建议您使用异步导入模式：在导入界面勾选「异步处理」选项，系统将立即返回导入任务 ID，所有链接将进入后台队列逐一处理。您可通过任务状态页面查看进度，处理完成后系统会发送通知。此外，您也可以调整 `config/development.py` 中的 `FETCH_TIMEOUT` 和 `BATCH_SIZE` 参数来优化性能。

问题：导出的 Markdown 文件中包含大量无关的 HTML 转义字符，影响阅读体验。如何配置导出格式？

回答：默认导出策略会保留原始摘要中的格式化标签。若您需要纯文本输出，请在导出设置中选择「纯文本模式」。该模式将自动剥离所有 HTML 标签，仅保留换行符与基本标点。同时，您可以在导出前通过批量编辑功能移除特定链接的摘要字段，或使用系统提供的自定义模板功能定义您自己的 Markdown 渲染结构，模板语法基于 Jinja2，支持灵活控制每个字段的输出方式。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
