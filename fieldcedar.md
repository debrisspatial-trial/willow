# WebRead 技术文章索引与资源聚合系统

WebRead 是一个面向技术研究者、开源贡献者和内容创作者的轻量化外链资源聚合与导航系统。该项目不生产内容，而是通过人工筛选与自动化采集相结合的方式，将分散在互联网各处的优质技术文章、教程、案例分析和开发文档进行结构化归档，形成可检索、可分类、可追溯的持久化外链资源池。

WebRead 的核心定位是「技术阅读资源的中转站与索引层」。它解决的是技术从业者在信息过载环境下，面对大量分散链接难以有效整理、回溯和分享的问题。系统提供基础的 URL 元数据提取、标签分类、全文检索和状态监控能力，让用户能够快速建立个人或团队的外链知识库，并支持通过 Markdown、JSON 和 CSV 格式批量导入导出资源清单。

本项目适用于需要长期维护技术阅读清单的开发者、需要沉淀团队外部知识资产的技术管理者，以及希望构建轻量级导航站点的开源项目维护者。WebRead 本身不依赖数据库，所有资源索引基于文件系统与 Git 版本管理，具备极低的运维门槛和良好的可移植性。

## 功能概览

批量资源导入 支持通过 Markdown 列表、JSON 数组或纯文本行批量添加外部 URL，自动去重并生成唯一资源 ID。

元数据自动提取 对每个提交的 URL 进行基础元数据抓取，包括页面标题、摘要文本、内容类型和预估阅读时长。

标签与分类管理 允许用户为每个资源自定义多级标签，支持按标签树进行筛选和聚合浏览。

资源状态监控 定时检测已收录 URL 的可访问性，自动标记失效链接并生成异常报告。

全文检索与过滤 基于资源标题、摘要、标签和自定义备注进行关键词检索，支持按收录时间、访问状态和标签组合过滤。

数据导入导出 支持将整个资源索引导出为 Markdown 列表、JSON 或 CSV 格式，也支持从上述格式恢复或合并数据。

版本化变更追踪 所有资源的增删改操作均通过 Git 提交记录进行版本管理，支持回溯任意时间点的资源清单状态。

## 应用场景

个人技术阅读清单管理 开发者可以使用 WebRead 维护自己的技术文章阅读队列，将日常浏览中发现的优质外链统一收录，并按「待读」、「在读」、「已读」等状态标签进行分类，避免链接散落在浏览器书签或临时笔记中无法有效管理。

团队外部知识库沉淀 技术团队可以将项目开发过程中参考的官方文档、技术博客、解决方案案例等外链资源集中录入 WebRead，形成团队共享的外部知识索引。新成员入职时可通过该索引快速了解团队常用的技术参考来源。

开源项目文档外链导航 开源项目维护者可以使用 WebRead 构建项目 README 或 Wiki 中的「相关资源」章节，将项目依赖的规范文档、社区教程、扩展工具等外链统一管理，在版本发布时同步更新资源列表。

技术资讯聚合与筛选 内容创作者或技术博主可以利用 WebRead 作为素材收集工具，将日常阅读中发现的值得引用的文章和案例先行收录，在撰写技术报告或专题文章时从索引中快速检索相关支撑材料。

## 快速开始

以下命令可在 Linux、macOS 或 Windows WSL 环境下完成 WebRead 的克隆、安装与初次运行。

```bash
git clone https://github.com/webread-dev/webread.git
cd webread
pip install -r requirements.txt
cp .env.example .env
python scripts/init_db.py
python app.py --port 8080
```

执行上述命令后，WebRead 将启动一个本地 HTTP 服务，默认监听 8080 端口。打开浏览器访问 http://127.0.0.1:8080 即可进入资源管理界面。首次启动会自动创建示例资源清单和默认分类标签。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心运行环境，推荐使用 3.11 或 3.12 |
| pip | 22.0 及以上 | Python 包管理工具，用于安装项目依赖 |
| Git | 2.30 及以上 | 用于版本化变更追踪和项目克隆更新 |
| BeautifulSoup4 | 4.12.0 及以上 | HTML 解析与元数据提取核心库 |
| requests | 2.31.0 及以上 | HTTP 请求客户端，用于资源状态检查和元数据抓取 |
| markdown | 3.5.0 及以上 | 用于解析 Markdown 格式的资源列表导入 |
| python-dotenv | 1.0.0 及以上 | 环境变量配置加载，用于敏感参数管理 |
| pytest | 7.4.0 及以上 | 单元测试框架，仅在开发环境需要 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | docs/user-guide/ | 如何添加资源、如何分类管理、如何导入导出数据、如何配置监控 |
| 部署指南 | docs/deployment/ | 如何在服务器上部署 WebRead 服务、如何配置反向代理、如何设置定时任务 |
| 开发者文档 | docs/developer/ | 项目架构说明、API 接口规范、如何扩展元数据提取器、如何贡献代码 |
| 运维参考 | docs/operations/ | 日志管理、数据备份策略、性能调优参数、常见故障排查 |

## 资源列表

- http://www.read.xwpxi.com/Article/271744.shtml
- http://www.read.xwpxi.com/Article/63564.shtml
- http://www.read.xwpxi.com/Article/1749.shtml
- http://www.read.xwpxi.com/Article/0690.shtml
- http://www.read.xwpxi.com/Article/96165.shtml
- http://www.read.xwpxi.com/Article/2997712.shtml
- http://www.read.xwpxi.com/Article/7667533.shtml
- http://www.read.xwpxi.com/Article/2183350.shtml
- http://www.read.xwpxi.com/Article/2464529.shtml
- http://www.read.xwpxi.com/Article/3833.shtml
- http://www.read.xwpxi.com/Article/7752365.shtml
- http://www.read.xwpxi.com/Article/0700.shtml
- http://www.read.xwpxi.com/Article/356999.shtml
- http://www.read.xwpxi.com/Article/365949.shtml
- http://www.read.xwpxi.com/Article/9255.shtml
- http://www.read.xwpxi.com/Article/72639.shtml
- http://www.read.xwpxi.com/Article/16966.shtml
- http://www.read.xwpxi.com/Article/543109.shtml
- http://www.read.xwpxi.com/Article/0262.shtml
- http://www.read.xwpxi.com/Article/15091.shtml
- http://www.read.xwpxi.com/Article/841487.shtml
- http://www.read.xwpxi.com/Article/3885259.shtml
- http://www.read.xwpxi.com/Article/4549.shtml
- http://www.read.xwpxi.com/Article/7663408.shtml
- http://www.read.xwpxi.com/Article/14806.shtml
- http://www.read.xwpxi.com/Article/5252627.shtml
- http://www.read.xwpxi.com/Article/820810.shtml
- http://www.read.xwpxi.com/Article/7901602.shtml
- http://www.read.xwpxi.com/Article/166019.shtml
- http://www.read.xwpxi.com/Article/2573803.shtml
- http://www.read.xwpxi.com/Article/3811712.shtml
- http://www.read.xwpxi.com/Article/15596.shtml
- http://www.read.xwpxi.com/Article/7408.shtml
- http://www.read.xwpxi.com/Article/004235.shtml
- http://www.read.xwpxi.com/Article/29359.shtml
- http://www.read.xwpxi.com/Article/393313.shtml
- http://www.read.xwpxi.com/Article/396681.shtml
- http://www.read.xwpxi.com/Article/6120.shtml
- http://www.read.xwpxi.com/Article/4120800.shtml
- http://www.read.xwpxi.com/Article/2569.shtml
- http://www.read.xwpxi.com/Article/8810438.shtml
- http://www.read.xwpxi.com/Article/55810.shtml
- http://www.read.xwpxi.com/Article/9305.shtml
- http://www.read.xwpxi.com/Article/144261.shtml
- http://www.read.xwpxi.com/Article/0416947.shtml
- http://www.read.xwpxi.com/Article/069741.shtml
- http://www.read.xwpxi.com/Article/1932110.shtml
- http://www.read.xwpxi.com/Article/443000.shtml
- http://www.read.xwpxi.com/Article/337332.shtml
- http://www.read.xwpxi.com/Article/0738654.shtml
- http://www.read.xwpxi.com/Article/2740447.shtml
- http://www.read.xwpxi.com/Article/4063973.shtml
- http://www.read.xwpxi.com/Article/8603.shtml
- http://www.read.xwpxi.com/Article/78388.shtml
- http://www.read.xwpxi.com/Article/0762506.shtml
- http://www.read.xwpxi.com/Article/890536.shtml
- http://www.read.xwpxi.com/Article/35832.shtml
- http://www.read.xwpxi.com/Article/962723.shtml
- http://www.read.xwpxi.com/Article/12028.shtml
- http://www.read.xwpxi.com/Article/2090212.shtml
- http://www.read.xwpxi.com/Article/281262.shtml
- http://www.read.xwpxi.com/Article/1627.shtml
- http://www.read.xwpxi.com/Article/29777.shtml
- http://www.read.xwpxi.com/Article/1996885.shtml
- http://www.read.xwpxi.com/Article/8209.shtml
- http://www.read.xwpxi.com/Article/2257154.shtml
- http://www.read.xwpxi.com/Article/2732.shtml
- http://www.read.xwpxi.com/Article/7299392.shtml
- http://www.read.xwpxi.com/Article/6943.shtml
- http://www.read.xwpxi.com/Article/8766.shtml
- http://www.read.xwpxi.com/Article/0496389.shtml
- http://www.read.xwpxi.com/Article/4617917.shtml
- http://www.read.xwpxi.com/Article/296562.shtml
- http://www.read.xwpxi.com/Article/3630488.shtml
- http://www.read.xwpxi.com/Article/398776.shtml
- http://www.read.xwpxi.com/Article/2085.shtml
- http://www.read.xwpxi.com/Article/3376.shtml
- http://www.read.xwpxi.com/Article/6324.shtml
- http://www.read.xwpxi.com/Article/56980.shtml
- http://www.read.xwpxi.com/Article/8968.shtml
- http://www.read.xwpxi.com/Article/543674.shtml
- http://www.read.xwpxi.com/Article/413390.shtml
- http://www.read.xwpxi.com/Article/32757.shtml
- http://www.read.xwpxi.com/Article/39879.shtml
- http://www.read.xwpxi.com/Article/4470.shtml
- http://www.read.xwpxi.com/Article/9543842.shtml
- http://www.read.xwpxi.com/Article/2889.shtml
- http://www.read.xwpxi.com/Article/7542.shtml
- http://www.read.xwpxi.com/Article/376472.shtml
- http://www.read.xwpxi.com/Article/102548.shtml
- http://www.read.xwpxi.com/Article/5756214.shtml
- http://www.read.xwpxi.com/Article/4185340.shtml
- http://www.read.xwpxi.com/Article/1736.shtml
- http://www.read.xwpxi.com/Article/64141.shtml
- http://www.read.xwpxi.com/Article/356643.shtml
- http://www.read.xwpxi.com/Article/312555.shtml
- http://www.read.xwpxi.com/Article/23483.shtml
- http://www.read.xwpxi.com/Article/5074356.shtml
- http://www.read.xwpxi.com/Article/10589.shtml
- http://www.read.xwpxi.com/Article/22134.shtml
- http://www.read.xwpxi.com/Article/443278.shtml
- http://www.read.xwpxi.com/Article/4743504.shtml
- http://www.read.xwpxi.com/Article/4912850.shtml
- http://www.read.xwpxi.com/Article/7225.shtml
- http://www.read.xwpxi.com/Article/28032.shtml
- http://www.read.xwpxi.com/Article/13494.shtml
- http://www.read.xwpxi.com/Article/245227.shtml
- http://www.read.xwpxi.com/Article/4804945.shtml
- http://www.read.xwpxi.com/Article/3382327.shtml
- http://www.read.xwpxi.com/Article/970337.shtml
- http://www.read.xwpxi.com/Article/58594.shtml
- http://www.read.xwpxi.com/Article/8269.shtml
- http://www.read.xwpxi.com/Article/937858.shtml
- http://www.read.xwpxi.com/Article/77001.shtml
- http://www.read.xwpxi.com/Article/367402.shtml
- http://www.read.xwpxi.com/Article/011275.shtml
- http://www.read.xwpxi.com/Article/2281.shtml
- http://www.read.xwpxi.com/Article/9648.shtml
- http://www.read.xwpxi.com/Article/8061309.shtml
- http://www.read.xwpxi.com/Article/491094.shtml
- http://www.read.xwpxi.com/Article/73977.shtml
- http://www.read.xwpxi.com/Article/7330.shtml
- http://www.read.xwpxi.com/Article/7685.shtml
- http://www.read.xwpxi.com/Article/563344.shtml
- http://www.read.xwpxi.com/Article/48596.shtml
- http://www.read.xwpxi.com/Article/0382.shtml
- http://www.read.xwpxi.com/Article/1316723.shtml
- http://www.read.xwpxi.com/Article/9522714.shtml
- http://www.read.xwpxi.com/Article/8100010.shtml
- http://www.read.xwpxi.com/Article/373377.shtml
- http://www.read.xwpxi.com/Article/434052.shtml
- http://www.read.xwpxi.com/Article/44944.shtml
- http://www.read.xwpxi.com/Article/1551.shtml
- http://www.read.xwpxi.com/Article/537356.shtml
- http://www.read.xwpxi.com/Article/62039.shtml
- http://www.read.xwpxi.com/Article/6252428.shtml
- http://www.read.xwpxi.com/Article/60818.shtml
- http://www.read.xwpxi.com/Article/8287.shtml
- http://www.read.xwpxi.com/Article/74314.shtml
- http://www.read.xwpxi.com/Article/5161545.shtml
- http://www.read.xwpxi.com/Article/57592.shtml
- http://www.read.xwpxi.com/Article/893142.shtml
- http://www.read.xwpxi.com/Article/51956.shtml
- http://www.read.xwpxi.com/Article/3962397.shtml
- http://www.read.xwpxi.com/Article/35497.shtml
- http://www.read.xwpxi.com/Article/5054.shtml
- http://www.read.xwpxi.com/Article/085878.shtml
- http://www.read.xwpxi.com/Article/939962.shtml
- http://www.read.xwpxi.com/Article/97598.shtml
- http://www.read.xwpxi.com/Article/8442.shtml
- http://www.read.xwpxi.com/Article/69177.shtml
- http://www.read.xwpxi.com/Article/431768.shtml
- http://www.read.xwpxi.com/Article/1150337.shtml
- http://www.read.xwpxi.com/Article/500400.shtml
- http://www.read.xwpxi.com/Article/485633.shtml
- http://www.read.xwpxi.com/Article/85227.shtml
- http://www.read.xwpxi.com/Article/5793.shtml
- http://www.read.xwpxi.com/Article/23956.shtml
- http://www.read.xwpxi.com/Article/938849.shtml
- http://www.read.xwpxi.com/Article/7158.shtml
- http://www.read.xwpxi.com/Article/9284.shtml
- http://www.read.xwpxi.com/Article/7896087.shtml
- http://www.read.xwpxi.com/Article/7582.shtml
- http://www.read.xwpxi.com/Article/599896.shtml
- http://www.read.xwpxi.com/Article/0425666.shtml
- http://www.read.xwpxi.com/Article/011639.shtml
- http://www.read.xwpxi.com/Article/953308.shtml
- http://www.read.xwpxi.com/Article/2538081.shtml
- http://www.read.xwpxi.com/Article/335624.shtml
- http://www.read.xwpxi.com/Article/580082.shtml
- http://www.read.xwpxi.com/Article/43278.shtml
- http://www.read.xwpxi.com/Article/86956.shtml
- http://www.read.xwpxi.com/Article/17289.shtml
- http://www.read.xwpxi.com/Article/7397554.shtml
- http://www.read.xwpxi.com/Article/557500.shtml
- http://www.read.xwpxi.com/Article/1576.shtml
- http://www.read.xwpxi.com/Article/21403.shtml
- http://www.read.xwpxi.com/Article/99852.shtml
- http://www.read.xwpxi.com/Article/662806.shtml
- http://www.read.xwpxi.com/Article/37038.shtml
- http://www.read.xwpxi.com/Article/16784.shtml
- http://www.read.xwpxi.com/Article/81916.shtml
- http://www.read.xwpxi.com/Article/2120151.shtml
- http://www.read.xwpxi.com/Article/955263.shtml
- http://www.read.xwpxi.com/Article/2921508.shtml
- http://www.read.xwpxi.com/Article/7393433.shtml
- http://www.read.xwpxi.com/Article/8232423.shtml
- http://www.read.xwpxi.com/Article/80319.shtml
- http://www.read.xwpxi.com/Article/361787.shtml
- http://www.read.xwpxi.com/Article/0643404.shtml
- http://www.read.xwpxi.com/Article/64527.shtml
- http://www.read.xwpxi.com/Article/37508.shtml
- http://www.read.xwpxi.com/Article/201995.shtml
- http://www.read.xwpxi.com/Article/81437.shtml
- http://www.read.xwpxi.com/Article/962154.shtml
- http://www.read.xwpxi.com/Article/4125424.shtml
- http://www.read.xwpxi.com/Article/2611.shtml
- http://www.read.xwpxi.com/Article/5545831.shtml
- http://www.read.xwpxi.com/Article/937174.shtml
- http://www.read.xwpxi.com/Article/7506409.shtml
- http://www.read.xwpxi.com/Article/047622.shtml
- http://www.read.xwpxi.com/Article/815088.shtml
- http://www.read.xwpxi.com/Article/0289792.shtml
- http://www.read.xwpxi.com/Article/092489.shtml
- http://www.read.xwpxi.com/Article/931630.shtml
- http://www.read.xwpxi.com/Article/2978.shtml
- http://www.read.xwpxi.com/Article/245649.shtml
- http://www.read.xwpxi.com/Article/416114.shtml
- http://www.read.xwpxi.com/Article/561162.shtml
- http://www.read.xwpxi.com/Article/57536.shtml
- http://www.read.xwpxi.com/Article/29848.shtml
- http://www.read.xwpxi.com/Article/03774.shtml
- http://www.read.xwpxi.com/Article/7660.shtml
- http://www.read.xwpxi.com/Article/428776.shtml
- http://www.read.xwpxi.com/Article/82583.shtml
- http://www.read.xwpxi.com/Article/053467.shtml
- http://www.read.xwpxi.com/Article/24873.shtml
- http://www.read.xwpxi.com/Article/0202602.shtml
- http://www.read.xwpxi.com/Article/4845931.shtml
- http://www.read.xwpxi.com/Article/43053.shtml
- http://www.read.xwpxi.com/Article/65056.shtml
- http://www.read.xwpxi.com/Article/09377.shtml
- http://www.read.xwpxi.com/Article/5074723.shtml
- http://www.read.xwpxi.com/Article/3595.shtml
- http://www.read.xwpxi.com/Article/1348.shtml
- http://www.read.xwpxi.com/Article/64628.shtml
- http://www.read.xwpxi.com/Article/0152.shtml
- http://www.read.xwpxi.com/Article/6928973.shtml
- http://www.read.xwpxi.com/Article/0346425.shtml
- http://www.read.xwpxi.com/Article/3792633.shtml
- http://www.read.xwpxi.com/Article/538108.shtml
- http://www.read.xwpxi.com/Article/4282440.shtml
- http://www.read.xwpxi.com/Article/6445210.shtml
- http://www.read.xwpxi.com/Article/1206.shtml
- http://www.read.xwpxi.com/Article/96635.shtml
- http://www.read.xwpxi.com/Article/7287759.shtml
- http://www.read.xwpxi.com/Article/544599.shtml
- http://www.read.xwpxi.com/Article/3858524.shtml
- http://www.read.xwpxi.com/Article/06033.shtml
- http://www.read.xwpxi.com/Article/03375.shtml
- http://www.read.xwpxi.com/Article/279767.shtml
- http://www.read.xwpxi.com/Article/02137.shtml
- http://www.read.xwpxi.com/Article/5304778.shtml
- http://www.read.xwpxi.com/Article/65785.shtml
- http://www.read.xwpxi.com/Article/7360.shtml
- http://www.read.xwpxi.com/Article/6463.shtml
- http://www.read.xwpxi.com/Article/591612.shtml
- http://www.read.xwpxi.com/Article/753498.shtml
- http://www.read.xwpxi.com/Article/6055.shtml
- http://www.read.xwpxi.com/Article/32046.shtml

## 项目结构

```
webread/
├── app.py                          # 主应用入口，初始化 HTTP 服务与路由注册
├── requirements.txt                # Python 依赖声明文件，锁定所有第三方库版本
├── .env.example                    # 环境变量配置模板，包含端口、缓存路径与监控间隔
├── core/                           # 核心业务逻辑模块
│   ├── resource_manager.py         # 资源增删改查、去重与 ID 生成
│   ├── metadata_fetcher.py         # 页面元数据抓取与解析，含超时与重试机制
│   ├── health_checker.py           # 定时与按需资源可访问性检测
│   └── index_builder.py            # 标签索引与全文检索索引的构建与更新
├── storage/                        # 数据持久化层
│   ├── file_repository.py          # 基于 JSON 文件的资源存储与读写操作
│   ├── git_tracker.py              # Git 变更提交与历史回滚封装
│   └── import_export.py            # Markdown / JSON / CSV 格式的导入导出转换器
├── web/                            # Web 界面与 API 路由
│   ├── routes/                     # 路由处理器
│   │   ├── resources.py            # 资源列表、详情、新增、编辑、删除接口
│   │   ├── tags.py                 # 标签树管理与分类聚合接口
│   │   └── dashboard.py            # 概览统计与最近动态接口
│   ├── templates/                  # Jinja2 模板文件
│   │   ├── base.html               # 基础布局模板
│   │   ├── index.html              # 资源列表主页
│   │   └── detail.html             # 单条资源详情与元数据显示页
│   └── static/                     # 前端静态资源
│       ├── style.css               # 基础样式与响应式布局
│       └── app.js                  # 前端交互逻辑，含检索与过滤
├── scripts/                        # 辅助脚本与运维工具
│   ├── init_db.py                  # 初始化存储目录与示例数据
│   ├── batch_import.py             # 批量导入命令行工具，支持 Markdown 列表解析
│   └── export_snapshot.py          # 生成当前资源索引的快照文件
├── tests/                          # 单元测试与集成测试
│   ├── test_resource_manager.py    # 资源管理模块测试用例
│   ├── test_metadata_fetcher.py    # 元数据抓取器测试，含 Mock HTTP 响应
│   └── test_health_checker.py      # 健康检查模块测试
├── docs/                           # 项目文档
│   ├── user-guide/                 # 用户手册分章节
│   ├── developer/                  # 开发者文档与 API 规范
│   └── operations/                 # 运维与部署指南
└── data/                           # 运行时数据目录（不纳入版本控制）
    ├── resources.json              # 主资源索引文件
    ├── tags.json                   # 标签定义与层级关系
    └── logs/                       # 应用日志与健康检查报告
```

## 贡献指南

1. 在 GitHub Issues 中查阅现有任务或提交新需求，确认所贡献内容未被他人认领。建议先就较大规模改动发起讨论，避免重复工作或方向偏离。

2. 从主分支派生个人开发分支，命名格式为 `feature/描述` 或 `fix/描述`。本地开发时请确保运行 `pytest` 通过所有现有测试用例，并为新增功能补充对应的测试代码。

3. 代码风格遵循 PEP 8 规范，提交前执行 `flake8 core/ web/ scripts/` 进行静态检查。所有公共函数和类需包含 docstring，说明参数、返回值和可能抛出的异常。

4. 提交变更时使用语义化提交信息格式：`<类型>: <简短描述>`，类型包括 `feat`、`fix`、`docs`、`refactor`、`test`、`chore`。提交信息需用英文书写。

5. 向主分支发起 Pull Request，并在描述中关联相关 Issue 编号。PR 需至少一名项目维护者审核通过后合并。合并后 CI 流程将自动更新文档站点并触发资源索引重建。

## 常见问题

Q: 系统支持同时管理多少个外链资源？性能是否会下降？

A: WebRead 在当前设计下，单份 JSON 索引文件可稳定支持 50000 条资源的存储与检索操作。检索响应时间在 10000 条资源级别下约 80 毫秒，在 50000 条级别下约 350 毫秒。若资源规模超过此数量级，建议启用 Git 分片存储或迁移至 PostgreSQL 后端，相关配置已在 `storage/` 模块中预留扩展接口。

Q: 元数据抓取失败或超时如何处理？是否会影响其他资源的管理？

A: 元数据抓取采用独立异步任务执行，单条资源的超时或失败不会阻塞主流程。系统在首次抓取失败时会记录错误类型，并在后续健康检查轮次中重试最多 3 次。用户也可以手动触发单条资源的元数据重新提取。所有失败记录会汇总在 `data/logs/fetch_errors.log` 中，便于排查。

Q: 如何将现有浏览器书签或 Pocket 收藏批量迁移到 WebRead？

A: 项目提供 `scripts/batch_import.py` 脚本，支持从 CSV 文件、Markdown 列表和 JSON 数组三种格式导入。浏览器书签可先导出为 HTML 格式，再使用社区提供的转换工具转为 CSV 后导入。Pocket 用户可通过其官方导出功能获取 HTML 或 JSON 格式数据，同样可经转换后批量导入。详细转换步骤参见 `docs/user-guide/batch-import.md`。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
