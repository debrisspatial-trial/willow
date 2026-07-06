# WebLink Navigator

WebLink Navigator 是一个面向技术研究者、内容聚合者与信息分析人员的结构化外链资源导航系统。该项目定位于对大规模分散式 URL 资源进行统一收录、分类标注与快速检索，解决从海量原始链接中高效定位有效信息的问题。通过提供轻量级的本地运行环境与清晰的资源视图，帮助用户在信息过载场景下建立有序的知识入口。

本项目适用于个人知识库构建、技术文章引用归档、舆情材料整理以及自动化爬虫数据预览等多种工作流。WebLink Navigator 不依赖外部数据库或云服务，所有资源数据以静态文本形式存储，便于版本控制与协作共享。

## 功能概览

- 批量链接导入与解析：支持从纯文本文件或标准输入流中批量导入原始 URL，自动解析协议、域名与路径参数。

- 多维度资源分类：根据 URL 来源域名、文件类型或路径关键字对链接进行自动归类，支持用户自定义标签体系。

- 快速全文检索：基于倒排索引机制，在资源标题、摘要及自定义备注字段中执行毫秒级关键词匹配。

- 资源状态快照：记录每次链接收录的时间戳与批次编号，提供第 25/80 批共 250 个资源链接的完整追溯视图。

- 静态站点生成：将资源列表与元数据渲染为离线可用的 HTML 文档，便于在浏览器中直接浏览或部署至任意静态托管服务。

- 导入导出兼容性：支持 CSV、JSON 与 Markdown 表格格式的导入导出，方便与电子表格软件或数据分析工具对接。

- 命令行交互界面：提供轻量级 CLI 工具，支持资源添加、删除、列表筛选与统计信息输出，无需图形界面即可完成日常维护。

## 应用场景

技术博客的参考文献整理：技术作者在撰写文章时，需要引用外部资料作为论据支撑。WebLink Navigator 可将分散在各个浏览器书签或临时笔记中的链接统一收录，并为每条链接添加主题标签与阅读状态，最终生成规范化的引用列表。

舆情监控数据预处理：舆情分析师每日需处理大量新闻报道与社交媒体链接。本系统可作为数据清洗的前置环节，将原始采集的 URL 去重、分类并标记来源可信度，为后续的情感分析或趋势研判提供结构化输入。

开源项目文档外链管理：开源项目的 README 或 Wiki 中经常包含大量外部参考链接。使用 WebLink Navigator 可以维护一个独立于代码仓库的外链索引文件，便于版本更新时同步校验链接可用性，避免文档中出现失效引用。

个人知识库资源聚合：使用本地笔记工具（如 Obsidian、Logseq 或 Emacs Org-mode）的用户，可将 WebLink Navigator 作为外部资源管理插件，定期将笔记中散落的链接导出至统一索引，实现知识的网状关联。

自动化爬虫任务结果预览：爬虫工程师在完成一次数据采集后，可将提取到的 URL 列表输入 WebLink Navigator 生成可视化的汇总报告，快速检查采集范围是否覆盖预期目标，以及是否存在异常重复条目。

## 快速开始

以下命令将指导您在三分钟内完成 WebLink Navigator 的本地部署与首次运行。

```bash
# 克隆项目仓库至本地
git clone https://github.com/weblink-navigator/weblink-navigator.git

# 进入项目根目录
cd weblink-navigator

# 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 系统请使用 venv\Scripts\activate
pip install -r requirements.txt

# 执行初始资源导入（示例数据包含第 25/80 批次 URL）
python cli.py import --batch 25 --source ./data/raw_urls_25_80.txt

# 启动本地静态预览服务
python cli.py serve --port 8000
```

运行上述命令后，在浏览器中访问 http://127.0.0.1:8000 即可查看资源导航页面。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 或更高 | 核心运行环境，用于执行 CLI 工具与静态生成逻辑 |
| pip | 22.0 或更高 | Python 包管理工具，用于安装依赖库 |
| virtualenv | 20.0 或更高（推荐） | 创建隔离的 Python 环境，避免全局包冲突 |
| Git | 2.25 或更高 | 用于克隆仓库及版本管理 |
| Markdown 解析库 | Python-Markdown 3.4.1 | 将资源备注中的 Markdown 格式渲染为 HTML |
| Jinja2 | 3.1.2 | 模板引擎，用于生成静态站点页面 |
| pytest | 7.2.0（可选） | 运行单元测试，验证导入解析逻辑的正确性 |
| 操作系统 | Linux/macOS/Windows | 跨平台支持，推荐在 Unix-like 系统下获得最佳性能 |
| 磁盘空间 | 至少 50 MB | 用于存放源代码、静态资源及生成的 HTML 文件 |
| 网络访问 | 建议具备 | 初始克隆与依赖安装阶段需要访问 PyPI 及 GitHub |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user_guide.md | 如何导入新批次资源？如何自定义分类标签？如何导出为 CSV？ |
| 开发者指南 | docs/developer_guide.md | 项目代码结构是怎样的？如何扩展新的解析器？如何提交补丁？ |
| 部署运维 | docs/deployment.md | 如何将静态站点部署到 VPS 或对象存储？如何配置自动化构建？ |
| 设计说明 | docs/design.md | 为什么要选择静态生成方案？数据索引的数据结构是什么？性能瓶颈在哪里？ |
| 变更日志 | CHANGELOG.md | 每个版本更新了哪些功能？修复了哪些缺陷？是否有破坏性变更？ |

## 资源列表

- http://www.read.xwpxi.com/Article/7551829.shtml
- http://www.read.xwpxi.com/Article/834768.shtml
- http://www.read.xwpxi.com/Article/7806.shtml
- http://www.read.xwpxi.com/Article/8844.shtml
- http://www.read.xwpxi.com/Article/70127.shtml
- http://www.read.xwpxi.com/Article/434347.shtml
- http://www.read.xwpxi.com/Article/065137.shtml
- http://www.read.xwpxi.com/Article/696212.shtml
- http://www.read.xwpxi.com/Article/19400.shtml
- http://www.read.xwpxi.com/Article/40497.shtml
- http://www.read.xwpxi.com/Article/6788.shtml
- http://www.read.xwpxi.com/Article/1561522.shtml
- http://www.read.xwpxi.com/Article/13867.shtml
- http://www.read.xwpxi.com/Article/1877766.shtml
- http://www.read.xwpxi.com/Article/986757.shtml
- http://www.read.xwpxi.com/Article/7211.shtml
- http://www.read.xwpxi.com/Article/4311.shtml
- http://www.read.xwpxi.com/Article/69321.shtml
- http://www.read.xwpxi.com/Article/7558051.shtml
- http://www.read.xwpxi.com/Article/8617.shtml
- http://www.read.xwpxi.com/Article/7880868.shtml
- http://www.read.xwpxi.com/Article/69036.shtml
- http://www.read.xwpxi.com/Article/654062.shtml
- http://www.read.xwpxi.com/Article/2140105.shtml
- http://www.read.xwpxi.com/Article/1094.shtml
- http://www.read.xwpxi.com/Article/4716210.shtml
- http://www.read.xwpxi.com/Article/9464205.shtml
- http://www.read.xwpxi.com/Article/8040.shtml
- http://www.read.xwpxi.com/Article/22748.shtml
- http://www.read.xwpxi.com/Article/4540093.shtml
- http://www.read.xwpxi.com/Article/3977.shtml
- http://www.read.xwpxi.com/Article/2917316.shtml
- http://www.read.xwpxi.com/Article/6704.shtml
- http://www.read.xwpxi.com/Article/4135664.shtml
- http://www.read.xwpxi.com/Article/4047800.shtml
- http://www.read.xwpxi.com/Article/9944648.shtml
- http://www.read.xwpxi.com/Article/7281.shtml
- http://www.read.xwpxi.com/Article/4711.shtml
- http://www.read.xwpxi.com/Article/5787.shtml
- http://www.read.xwpxi.com/Article/8503.shtml
- http://www.read.xwpxi.com/Article/3227.shtml
- http://www.read.xwpxi.com/Article/83559.shtml
- http://www.read.xwpxi.com/Article/1992719.shtml
- http://www.read.xwpxi.com/Article/6064225.shtml
- http://www.read.xwpxi.com/Article/09088.shtml
- http://www.read.xwpxi.com/Article/061424.shtml
- http://www.read.xwpxi.com/Article/006028.shtml
- http://www.read.xwpxi.com/Article/94889.shtml
- http://www.read.xwpxi.com/Article/105905.shtml
- http://www.read.xwpxi.com/Article/26798.shtml
- http://www.read.xwpxi.com/Article/85107.shtml
- http://www.read.xwpxi.com/Article/05071.shtml
- http://www.read.xwpxi.com/Article/3130.shtml
- http://www.read.xwpxi.com/Article/5414.shtml
- http://www.read.xwpxi.com/Article/18348.shtml
- http://www.read.xwpxi.com/Article/38599.shtml
- http://www.read.xwpxi.com/Article/849525.shtml
- http://www.read.xwpxi.com/Article/364450.shtml
- http://www.read.xwpxi.com/Article/0917545.shtml
- http://www.read.xwpxi.com/Article/486774.shtml
- http://www.read.xwpxi.com/Article/62272.shtml
- http://www.read.xwpxi.com/Article/97372.shtml
- http://www.read.xwpxi.com/Article/57680.shtml
- http://www.read.xwpxi.com/Article/80126.shtml
- http://www.read.xwpxi.com/Article/515869.shtml
- http://www.read.xwpxi.com/Article/7994855.shtml
- http://www.read.xwpxi.com/Article/8892.shtml
- http://www.read.xwpxi.com/Article/6634.shtml
- http://www.read.xwpxi.com/Article/0953.shtml
- http://www.read.xwpxi.com/Article/1248593.shtml
- http://www.read.xwpxi.com/Article/3110.shtml
- http://www.read.xwpxi.com/Article/8344569.shtml
- http://www.read.xwpxi.com/Article/5918.shtml
- http://www.read.xwpxi.com/Article/8266.shtml
- http://www.read.xwpxi.com/Article/5970035.shtml
- http://www.read.xwpxi.com/Article/2132.shtml
- http://www.read.xwpxi.com/Article/5042875.shtml
- http://www.read.xwpxi.com/Article/2940681.shtml
- http://www.read.xwpxi.com/Article/4670.shtml
- http://www.read.xwpxi.com/Article/05936.shtml
- http://www.read.xwpxi.com/Article/17041.shtml
- http://www.read.xwpxi.com/Article/37243.shtml
- http://www.read.xwpxi.com/Article/06266.shtml
- http://www.read.xwpxi.com/Article/933528.shtml
- http://www.read.xwpxi.com/Article/0836161.shtml
- http://www.read.xwpxi.com/Article/2403.shtml
- http://www.read.xwpxi.com/Article/58572.shtml
- http://www.read.xwpxi.com/Article/850929.shtml
- http://www.read.xwpxi.com/Article/5594755.shtml
- http://www.read.xwpxi.com/Article/0976.shtml
- http://www.read.xwpxi.com/Article/460329.shtml
- http://www.read.xwpxi.com/Article/8901480.shtml
- http://www.read.xwpxi.com/Article/00456.shtml
- http://www.read.xwpxi.com/Article/269875.shtml
- http://www.read.xwpxi.com/Article/14664.shtml
- http://www.read.xwpxi.com/Article/257757.shtml
- http://www.read.xwpxi.com/Article/509026.shtml
- http://www.read.xwpxi.com/Article/161721.shtml
- http://www.read.xwpxi.com/Article/92002.shtml
- http://www.read.xwpxi.com/Article/65947.shtml
- http://www.read.xwpxi.com/Article/8077.shtml
- http://www.read.xwpxi.com/Article/2347654.shtml
- http://www.read.xwpxi.com/Article/4380258.shtml
- http://www.read.xwpxi.com/Article/3472634.shtml
- http://www.read.xwpxi.com/Article/1113603.shtml
- http://www.read.xwpxi.com/Article/2589.shtml
- http://www.read.xwpxi.com/Article/0643165.shtml
- http://www.read.xwpxi.com/Article/59582.shtml
- http://www.read.xwpxi.com/Article/164931.shtml
- http://www.read.xwpxi.com/Article/6889129.shtml
- http://www.read.xwpxi.com/Article/0636191.shtml
- http://www.read.xwpxi.com/Article/1464034.shtml
- http://www.read.xwpxi.com/Article/7399.shtml
- http://www.read.xwpxi.com/Article/8151.shtml
- http://www.read.xwpxi.com/Article/2202874.shtml
- http://www.read.xwpxi.com/Article/9002.shtml
- http://www.read.xwpxi.com/Article/98220.shtml
- http://www.read.xwpxi.com/Article/0069567.shtml
- http://www.read.xwpxi.com/Article/6377.shtml
- http://www.read.xwpxi.com/Article/458214.shtml
- http://www.read.xwpxi.com/Article/373150.shtml
- http://www.read.xwpxi.com/Article/0022446.shtml
- http://www.read.xwpxi.com/Article/304185.shtml
- http://www.read.xwpxi.com/Article/1322675.shtml
- http://www.read.xwpxi.com/Article/067666.shtml
- http://www.read.xwpxi.com/Article/245811.shtml
- http://www.read.xwpxi.com/Article/3203761.shtml
- http://www.read.xwpxi.com/Article/15195.shtml
- http://www.read.xwpxi.com/Article/137639.shtml
- http://www.read.xwpxi.com/Article/3793584.shtml
- http://www.read.xwpxi.com/Article/626304.shtml
- http://www.read.xwpxi.com/Article/2099.shtml
- http://www.read.xwpxi.com/Article/9536489.shtml
- http://www.read.xwpxi.com/Article/7712476.shtml
- http://www.read.xwpxi.com/Article/086189.shtml
- http://www.read.xwpxi.com/Article/970067.shtml
- http://www.read.xwpxi.com/Article/236989.shtml
- http://www.read.xwpxi.com/Article/098634.shtml
- http://www.read.xwpxi.com/Article/792743.shtml
- http://www.read.xwpxi.com/Article/6329.shtml
- http://www.read.xwpxi.com/Article/6314351.shtml
- http://www.read.xwpxi.com/Article/112901.shtml
- http://www.read.xwpxi.com/Article/464382.shtml
- http://www.read.xwpxi.com/Article/860882.shtml
- http://www.read.xwpxi.com/Article/6364829.shtml
- http://www.read.xwpxi.com/Article/844670.shtml
- http://www.read.xwpxi.com/Article/9444.shtml
- http://www.read.xwpxi.com/Article/9453244.shtml
- http://www.read.xwpxi.com/Article/6497.shtml
- http://www.read.xwpxi.com/Article/301856.shtml
- http://www.read.xwpxi.com/Article/5596450.shtml
- http://www.read.xwpxi.com/Article/7765.shtml
- http://www.read.xwpxi.com/Article/47636.shtml
- http://www.read.xwpxi.com/Article/7534.shtml
- http://www.read.xwpxi.com/Article/7688.shtml
- http://www.read.xwpxi.com/Article/434257.shtml
- http://www.read.xwpxi.com/Article/887715.shtml
- http://www.read.xwpxi.com/Article/89169.shtml
- http://www.read.xwpxi.com/Article/1789.shtml
- http://www.read.xwpxi.com/Article/57808.shtml
- http://www.read.xwpxi.com/Article/2764.shtml
- http://www.read.xwpxi.com/Article/3068338.shtml
- http://www.read.xwpxi.com/Article/321010.shtml
- http://www.read.xwpxi.com/Article/0762855.shtml
- http://www.read.xwpxi.com/Article/3221.shtml
- http://www.read.xwpxi.com/Article/251269.shtml
- http://www.read.xwpxi.com/Article/4285.shtml
- http://www.read.xwpxi.com/Article/266859.shtml
- http://www.read.xwpxi.com/Article/2922.shtml
- http://www.read.xwpxi.com/Article/5066.shtml
- http://www.read.xwpxi.com/Article/721217.shtml
- http://www.read.xwpxi.com/Article/1248396.shtml
- http://www.read.xwpxi.com/Article/172718.shtml
- http://www.read.xwpxi.com/Article/98290.shtml
- http://www.read.xwpxi.com/Article/3301044.shtml
- http://www.read.xwpxi.com/Article/75436.shtml
- http://www.read.xwpxi.com/Article/0067532.shtml
- http://www.read.xwpxi.com/Article/9643674.shtml
- http://www.read.xwpxi.com/Article/3959.shtml
- http://www.read.xwpxi.com/Article/1173.shtml
- http://www.read.xwpxi.com/Article/70436.shtml
- http://www.read.xwpxi.com/Article/5166980.shtml
- http://www.read.xwpxi.com/Article/3627.shtml
- http://www.read.xwpxi.com/Article/2789.shtml
- http://www.read.xwpxi.com/Article/765821.shtml
- http://www.read.xwpxi.com/Article/1852351.shtml
- http://www.read.xwpxi.com/Article/2919.shtml
- http://www.read.xwpxi.com/Article/6989276.shtml
- http://www.read.xwpxi.com/Article/0095840.shtml
- http://www.read.xwpxi.com/Article/2958307.shtml
- http://www.read.xwpxi.com/Article/56272.shtml
- http://www.read.xwpxi.com/Article/0239228.shtml
- http://www.read.xwpxi.com/Article/18695.shtml
- http://www.read.xwpxi.com/Article/86883.shtml
- http://www.read.xwpxi.com/Article/6749.shtml
- http://www.read.xwpxi.com/Article/152598.shtml
- http://www.read.xwpxi.com/Article/193418.shtml
- http://www.read.xwpxi.com/Article/42353.shtml
- http://www.read.xwpxi.com/Article/493823.shtml
- http://www.read.xwpxi.com/Article/2950516.shtml
- http://www.read.xwpxi.com/Article/82605.shtml
- http://www.read.xwpxi.com/Article/451382.shtml
- http://www.read.xwpxi.com/Article/4143.shtml
- http://www.read.xwpxi.com/Article/8401609.shtml
- http://www.read.xwpxi.com/Article/4755.shtml
- http://www.read.xwpxi.com/Article/95496.shtml
- http://www.read.xwpxi.com/Article/4233940.shtml
- http://www.read.xwpxi.com/Article/7650643.shtml
- http://www.read.xwpxi.com/Article/944758.shtml
- http://www.read.xwpxi.com/Article/3171.shtml
- http://www.read.xwpxi.com/Article/8881.shtml
- http://www.read.xwpxi.com/Article/260656.shtml
- http://www.read.xwpxi.com/Article/0971101.shtml
- http://www.read.xwpxi.com/Article/694083.shtml
- http://www.read.xwpxi.com/Article/0669.shtml
- http://www.read.xwpxi.com/Article/345668.shtml
- http://www.read.xwpxi.com/Article/8433006.shtml
- http://www.read.xwpxi.com/Article/08801.shtml
- http://www.read.xwpxi.com/Article/4574.shtml
- http://www.read.xwpxi.com/Article/85488.shtml
- http://www.read.xwpxi.com/Article/6695781.shtml
- http://www.read.xwpxi.com/Article/310172.shtml
- http://www.read.xwpxi.com/Article/58217.shtml
- http://www.read.xwpxi.com/Article/8311.shtml
- http://www.read.xwpxi.com/Article/1606006.shtml
- http://www.read.xwpxi.com/Article/935554.shtml
- http://www.read.xwpxi.com/Article/5885411.shtml
- http://www.read.xwpxi.com/Article/1338.shtml
- http://www.read.xwpxi.com/Article/27877.shtml
- http://www.read.xwpxi.com/Article/6855.shtml
- http://www.read.xwpxi.com/Article/2824575.shtml
- http://www.read.xwpxi.com/Article/5587831.shtml
- http://www.read.xwpxi.com/Article/2598513.shtml
- http://www.read.xwpxi.com/Article/952085.shtml
- http://www.read.xwpxi.com/Article/4894266.shtml
- http://www.read.xwpxi.com/Article/3502753.shtml
- http://www.read.xwpxi.com/Article/5779352.shtml
- http://www.read.xwpxi.com/Article/672381.shtml
- http://www.read.xwpxi.com/Article/6951152.shtml
- http://www.read.xwpxi.com/Article/16176.shtml
- http://www.read.xwpxi.com/Article/804647.shtml
- http://www.read.xwpxi.com/Article/36228.shtml
- http://www.read.xwpxi.com/Article/1998.shtml
- http://www.read.xwpxi.com/Article/411056.shtml
- http://www.read.xwpxi.com/Article/13014.shtml
- http://www.read.xwpxi.com/Article/3417.shtml
- http://www.read.xwpxi.com/Article/44139.shtml
- http://www.read.xwpxi.com/Article/0429.shtml
- http://www.read.xwpxi.com/Article/9036.shtml
- http://www.read.xwpxi.com/Article/057374.shtml

## 项目结构

```
weblink-navigator/
├── cli.py                      # 命令行入口，解析子命令并调用对应模块
├── requirements.txt            # Python 依赖清单，包含 Jinja2、Markdown 等
├── CHANGELOG.md                # 版本变更记录，按语义化版本号组织
├── LICENSE                     # MIT 许可证全文
├── README.md                   # 项目说明文档（即本文档）
├── config/
│   ├── default.yaml            # 默认配置项，包含端口、缓存目录、分页大小
│   └── schema.json             # 资源数据结构的 JSON Schema 校验文件
├── data/
│   ├── raw_urls_25_80.txt      # 第 25/80 批次原始链接列表（共 250 条）
│   ├── resources.db.json       # 主数据存储文件，包含所有已导入资源条目
│   └── tags.index.json         # 标签索引，记录标签与资源 ID 的映射关系
├── src/
│   ├── __init__.py             # 包初始化文件，声明版本号与公开 API
│   ├── importer.py             # 链接导入解析器，支持纯文本与 CSV 格式
│   ├── search.py               # 倒排索引构建与检索执行引擎
│   ├── renderer.py             # 静态站点渲染器，调用 Jinja2 模板生成 HTML
│   ├── exporter.py             # 数据导出模块，支持 JSON/CSV/Markdown 格式
│   └── utils.py                # 通用工具函数，如日期格式化、URL 规范化
├── templates/
│   ├── base.html               # 基础 HTML 模板，定义导航栏与页脚结构
│   ├── index.html              # 资源列表页模板，展示分页后的链接表格
│   └── detail.html             # 单条资源详情页模板，显示完整元数据
├── tests/
│   ├── test_importer.py        # 导入解析器的单元测试用例
│   ├── test_search.py          # 搜索引擎的单元测试用例
│   └── fixtures/               # 测试固定数据集，包含示例 URL 与预期结果
├── docs/
│   ├── user_guide.md           # 用户手册，涵盖日常操作流程
│   ├── developer_guide.md      # 开发者指南，包含贡献规范与调试方法
│   ├── deployment.md           # 部署运维文档，含 Nginx 配置示例
│   └── design.md               # 设计文档，阐述架构决策与数据流
└── build/
    └── output/                 # 静态站点生成目标目录，包含 HTML/CSS/JS
```

## 贡献指南

1. 在 GitHub Issues 中查找标记为「good first issue」或「help wanted」的任务，或新建 Issue 描述您希望实现的功能或修复的缺陷，等待维护者确认需求范围。

2. Fork 本仓库至个人账户，在本地创建功能分支（如 feature/add-json-export 或 fix/search-case-sensitivity），确保分支命名能够体现变更意图。

3. 编写或修改代码时，请遵循项目已有的代码风格（使用 PEP 8 标准，函数添加 docstring，提交前运行 pytest 确保所有测试用例通过）。

4. 提交 Pull Request 时，请在描述中关联对应的 Issue 编号，并列出变更摘要、测试覆盖情况以及是否包含破坏性改动。维护者将在 3 个工作日内进行审查。

5. 若需要更新资源列表数据，请将新批次 URL 按照已有格式追加至 data/ 目录下的对应文件，并同步更新本文档的资源列表章节。

## 常见问题

Q: 项目启动后浏览器无法访问 8000 端口，应该怎么办？

A: 首先确认终端是否显示了「Serving at http://127.0.0.1:8000」字样。若未显示，请检查是否存在端口占用（可使用 lsof -i:8000 命令）。若端口被占用，可通过 python cli.py serve --port 8001 更换端口。若提示缺少依赖，请重新执行 pip install -r requirements.txt 安装所有依赖包。

Q: 如何批量导入我自己的链接列表，而非使用示例数据？

A: 您可以将自己的 URL 列表保存为纯文本文件（每行一个 URL），然后执行 python cli.py import --batch 自定义批次号 --source 您的文件路径。导入后，系统会自动去重并生成新的资源条目。若需要覆盖已有批次，可添加 --force 参数。

Q: 静态站点生成后，资源备注中的 Markdown 格式没有被渲染为 HTML，如何解决？

A: 请确认在导入数据时，备注字段使用了标准的 Markdown 语法（如 [text](url) 或 **粗体**）。渲染器默认启用 Markdown 扩展，若仍不生效，请检查 config/default.yaml 中的 markdown_extensions 配置项是否包含 extra 和 toc。您也可以手动编辑 resources.db.json 中的 remark 字段，然后重新运行 python cli.py render 生成静态页面。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
