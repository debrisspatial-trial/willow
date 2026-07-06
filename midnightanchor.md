# WebLink Collective Archive

WebLink Collective Archive 是一个面向技术研究者、内容运营者和信息分析人员的外链资源归集与元数据管理工具。该项目并不试图成为另一个搜索引擎或内容聚合平台，而是专注于解决分散在大量路径型 URL 中的资源定位、状态监测、分类标注与批量引用问题。目标用户包括开源文档维护者、技术博客编辑、数据采集工程师以及需要进行大规模外链审计的合规团队。

本项目以静态资源索引为核心，内置元数据提取与链接健康度检查框架，能够对用户导入的批量 URL 进行结构化存储，并生成可视化的资源清单。第 6/80 批次收录了来自 read.xwpxi.com 域下的 250 个文章型 URL，项目提供完整的导入、解析、筛选与导出工作流，支持命令行交互与 API 调用两种使用方式。

## 功能概览

批量 URL 导入解析：支持从文本文件、CSV 或直接粘贴的 URL 列表中批量解析资源地址，自动识别 URL 结构中的目录层级、文件后缀及参数模式。

链接状态实时检测：内置异步 HTTP 客户端，支持配置超时时间与重试策略，可对每个 URL 执行可达性检测，返回状态码、响应时长与重定向链信息。

元数据自动提取：从目标页面中提取标题、摘要、关键词以及基础 HTML 结构信息，支持通过正则表达式或 CSS 选择器自定义抓取规则。

资源分类与标签管理：提供扁平标签体系与树形分类两种组织方式，用户可为每个 URL 分配多个标签，并基于标签组合进行快速筛选。

索引快照与版本记录：每次导入或更新操作均生成索引快照，支持历史版本回溯与变更差异对比，便于审计追踪。

数据导出与集成：支持将资源列表导出为 JSON、CSV 或 Markdown 表格格式，并提供 RESTful API 供外部系统集成。

命令行交互界面：提供完整的 CLI 工具，支持交互式筛选、批量操作与脚本化调用，适配服务器端自动化运维场景。

## 应用场景

技术文档团队进行外部引用链接的定期审计。当项目文档中引用大量外部文章或 API 文档时，维护人员可使用 WebLink Collective Archive 批量检测所有引用链接的有效性，及时发现失效链接并生成替换建议报告。

内容运营人员构建行业资源导航页。运营人员可将分散在多个来源的优质文章 URL 统一导入系统，通过标签和分类进行组织，快速生成按主题或时间排序的资源导航页面，供读者查阅。

数据采集工程师验证数据源可用性。在构建数据采集管道前，工程师可使用本工具对候选数据源 URL 进行批量预检，过滤掉响应超时或返回异常状态的地址，确保采集任务的稳定性。

合规审计团队执行外链合规检查。法务或合规团队可定期导入需要审查的外部链接列表，利用元数据提取功能获取页面快照信息，辅助判断链接内容是否符合合规要求，并生成审计日志。

## 快速开始

以下命令演示了从克隆代码到运行基础检测的完整流程。

```bash
git clone https://github.com/weblink-archive/weblink-collective.git
cd weblink-collective
pip install -r requirements.txt
cp config.example.yaml config.yaml
python cli.py import --source urls.txt --batch 6
python cli.py check --batch 6 --timeout 10 --retry 3
python cli.py export --batch 6 --format markdown --output report_6.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 - 3.11 | 核心运行环境，推荐使用 3.10 长期支持版本 |
| pip | 21.0 及以上 | Python 包管理器，用于安装项目依赖项 |
| aiohttp | 3.8.0 及以上 | 异步 HTTP 客户端库，用于并发链接检测请求 |
| beautifulsoup4 | 4.11.0 及以上 | HTML 解析库，用于提取页面标题与元数据 |
| pyyaml | 6.0 及以上 | YAML 格式配置文件解析与写入支持 |
| click | 8.1.0 及以上 | 命令行交互界面框架，用于实现 CLI 子命令 |
| pytest | 7.0.0 及以上 | 单元测试与集成测试框架（仅开发环境需要） |
| redis | 5.0.0 及以上 | 可选缓存后端，用于加速重复 URL 的检测结果查询 |
| postgresql | 13.0 及以上 | 可选持久化存储后端，用于大规模索引管理 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide/ | 如何安装、导入 URL、执行检测与导出结果 |
| 配置参考 | docs/configuration.md | 配置文件中的各项参数含义与推荐取值 |
| API 接口 | docs/api-reference.md | RESTful API 的端点列表、请求格式与响应结构 |
| 开发指南 | docs/developer-guide/ | 项目架构、模块划分与二次开发扩展方法 |
| 运维手册 | docs/operations.md | 部署方案、日志管理、性能调优与故障排查 |
| 常见问题 | docs/faq.md | 社区收集的典型问题与解决方案汇总 |

## 资源列表

- http://www.read.xwpxi.com/Article/52909.shtml
- http://www.read.xwpxi.com/Article/5112386.shtml
- http://www.read.xwpxi.com/Article/121443.shtml
- http://www.read.xwpxi.com/Article/71031.shtml
- http://www.read.xwpxi.com/Article/803110.shtml
- http://www.read.xwpxi.com/Article/9375.shtml
- http://www.read.xwpxi.com/Article/6705.shtml
- http://www.read.xwpxi.com/Article/2699.shtml
- http://www.read.xwpxi.com/Article/42131.shtml
- http://www.read.xwpxi.com/Article/3625731.shtml
- http://www.read.xwpxi.com/Article/23678.shtml
- http://www.read.xwpxi.com/Article/873708.shtml
- http://www.read.xwpxi.com/Article/9930468.shtml
- http://www.read.xwpxi.com/Article/742409.shtml
- http://www.read.xwpxi.com/Article/2873.shtml
- http://www.read.xwpxi.com/Article/690527.shtml
- http://www.read.xwpxi.com/Article/28723.shtml
- http://www.read.xwpxi.com/Article/2546.shtml
- http://www.read.xwpxi.com/Article/887462.shtml
- http://www.read.xwpxi.com/Article/856672.shtml
- http://www.read.xwpxi.com/Article/3514101.shtml
- http://www.read.xwpxi.com/Article/6125.shtml
- http://www.read.xwpxi.com/Article/5239714.shtml
- http://www.read.xwpxi.com/Article/7890.shtml
- http://www.read.xwpxi.com/Article/5764491.shtml
- http://www.read.xwpxi.com/Article/054873.shtml
- http://www.read.xwpxi.com/Article/26164.shtml
- http://www.read.xwpxi.com/Article/049438.shtml
- http://www.read.xwpxi.com/Article/248798.shtml
- http://www.read.xwpxi.com/Article/8471.shtml
- http://www.read.xwpxi.com/Article/6203986.shtml
- http://www.read.xwpxi.com/Article/435459.shtml
- http://www.read.xwpxi.com/Article/6739.shtml
- http://www.read.xwpxi.com/Article/8078.shtml
- http://www.read.xwpxi.com/Article/7709973.shtml
- http://www.read.xwpxi.com/Article/5122.shtml
- http://www.read.xwpxi.com/Article/3980621.shtml
- http://www.read.xwpxi.com/Article/142005.shtml
- http://www.read.xwpxi.com/Article/145201.shtml
- http://www.read.xwpxi.com/Article/3551218.shtml
- http://www.read.xwpxi.com/Article/2585410.shtml
- http://www.read.xwpxi.com/Article/181956.shtml
- http://www.read.xwpxi.com/Article/6338.shtml
- http://www.read.xwpxi.com/Article/331116.shtml
- http://www.read.xwpxi.com/Article/7409.shtml
- http://www.read.xwpxi.com/Article/03525.shtml
- http://www.read.xwpxi.com/Article/6919.shtml
- http://www.read.xwpxi.com/Article/0858569.shtml
- http://www.read.xwpxi.com/Article/678567.shtml
- http://www.read.xwpxi.com/Article/9315.shtml
- http://www.read.xwpxi.com/Article/867067.shtml
- http://www.read.xwpxi.com/Article/25060.shtml
- http://www.read.xwpxi.com/Article/785541.shtml
- http://www.read.xwpxi.com/Article/174605.shtml
- http://www.read.xwpxi.com/Article/7316481.shtml
- http://www.read.xwpxi.com/Article/2208.shtml
- http://www.read.xwpxi.com/Article/4342577.shtml
- http://www.read.xwpxi.com/Article/046713.shtml
- http://www.read.xwpxi.com/Article/3840719.shtml
- http://www.read.xwpxi.com/Article/71390.shtml
- http://www.read.xwpxi.com/Article/739093.shtml
- http://www.read.xwpxi.com/Article/78492.shtml
- http://www.read.xwpxi.com/Article/485825.shtml
- http://www.read.xwpxi.com/Article/3067688.shtml
- http://www.read.xwpxi.com/Article/8532.shtml
- http://www.read.xwpxi.com/Article/42132.shtml
- http://www.read.xwpxi.com/Article/0048.shtml
- http://www.read.xwpxi.com/Article/9221999.shtml
- http://www.read.xwpxi.com/Article/421259.shtml
- http://www.read.xwpxi.com/Article/33531.shtml
- http://www.read.xwpxi.com/Article/15609.shtml
- http://www.read.xwpxi.com/Article/262003.shtml
- http://www.read.xwpxi.com/Article/99997.shtml
- http://www.read.xwpxi.com/Article/709032.shtml
- http://www.read.xwpxi.com/Article/5097.shtml
- http://www.read.xwpxi.com/Article/137655.shtml
- http://www.read.xwpxi.com/Article/1977.shtml
- http://www.read.xwpxi.com/Article/2370445.shtml
- http://www.read.xwpxi.com/Article/98112.shtml
- http://www.read.xwpxi.com/Article/42368.shtml
- http://www.read.xwpxi.com/Article/39597.shtml
- http://www.read.xwpxi.com/Article/970513.shtml
- http://www.read.xwpxi.com/Article/03706.shtml
- http://www.read.xwpxi.com/Article/1255.shtml
- http://www.read.xwpxi.com/Article/2642770.shtml
- http://www.read.xwpxi.com/Article/869908.shtml
- http://www.read.xwpxi.com/Article/01545.shtml
- http://www.read.xwpxi.com/Article/9884866.shtml
- http://www.read.xwpxi.com/Article/53058.shtml
- http://www.read.xwpxi.com/Article/7241.shtml
- http://www.read.xwpxi.com/Article/91232.shtml
- http://www.read.xwpxi.com/Article/8248432.shtml
- http://www.read.xwpxi.com/Article/3472026.shtml
- http://www.read.xwpxi.com/Article/0489285.shtml
- http://www.read.xwpxi.com/Article/1238424.shtml
- http://www.read.xwpxi.com/Article/8287122.shtml
- http://www.read.xwpxi.com/Article/0745.shtml
- http://www.read.xwpxi.com/Article/26744.shtml
- http://www.read.xwpxi.com/Article/4202.shtml
- http://www.read.xwpxi.com/Article/73375.shtml
- http://www.read.xwpxi.com/Article/83846.shtml
- http://www.read.xwpxi.com/Article/1290134.shtml
- http://www.read.xwpxi.com/Article/6859240.shtml
- http://www.read.xwpxi.com/Article/4497316.shtml
- http://www.read.xwpxi.com/Article/108568.shtml
- http://www.read.xwpxi.com/Article/9123.shtml
- http://www.read.xwpxi.com/Article/40625.shtml
- http://www.read.xwpxi.com/Article/4869918.shtml
- http://www.read.xwpxi.com/Article/9476.shtml
- http://www.read.xwpxi.com/Article/8621.shtml
- http://www.read.xwpxi.com/Article/915148.shtml
- http://www.read.xwpxi.com/Article/68989.shtml
- http://www.read.xwpxi.com/Article/2554225.shtml
- http://www.read.xwpxi.com/Article/6488882.shtml
- http://www.read.xwpxi.com/Article/5039.shtml
- http://www.read.xwpxi.com/Article/8416443.shtml
- http://www.read.xwpxi.com/Article/18606.shtml
- http://www.read.xwpxi.com/Article/6574.shtml
- http://www.read.xwpxi.com/Article/6528786.shtml
- http://www.read.xwpxi.com/Article/8321.shtml
- http://www.read.xwpxi.com/Article/390800.shtml
- http://www.read.xwpxi.com/Article/38415.shtml
- http://www.read.xwpxi.com/Article/3396184.shtml
- http://www.read.xwpxi.com/Article/38943.shtml
- http://www.read.xwpxi.com/Article/7302292.shtml
- http://www.read.xwpxi.com/Article/4771.shtml
- http://www.read.xwpxi.com/Article/85557.shtml
- http://www.read.xwpxi.com/Article/7040.shtml
- http://www.read.xwpxi.com/Article/8696.shtml
- http://www.read.xwpxi.com/Article/95941.shtml
- http://www.read.xwpxi.com/Article/8674.shtml
- http://www.read.xwpxi.com/Article/201673.shtml
- http://www.read.xwpxi.com/Article/70731.shtml
- http://www.read.xwpxi.com/Article/7334736.shtml
- http://www.read.xwpxi.com/Article/4354687.shtml
- http://www.read.xwpxi.com/Article/795603.shtml
- http://www.read.xwpxi.com/Article/7399005.shtml
- http://www.read.xwpxi.com/Article/869509.shtml
- http://www.read.xwpxi.com/Article/030141.shtml
- http://www.read.xwpxi.com/Article/082355.shtml
- http://www.read.xwpxi.com/Article/588603.shtml
- http://www.read.xwpxi.com/Article/3979882.shtml
- http://www.read.xwpxi.com/Article/455295.shtml
- http://www.read.xwpxi.com/Article/0071.shtml
- http://www.read.xwpxi.com/Article/2438.shtml
- http://www.read.xwpxi.com/Article/3993664.shtml
- http://www.read.xwpxi.com/Article/414372.shtml
- http://www.read.xwpxi.com/Article/84153.shtml
- http://www.read.xwpxi.com/Article/3309.shtml
- http://www.read.xwpxi.com/Article/5447.shtml
- http://www.read.xwpxi.com/Article/092339.shtml
- http://www.read.xwpxi.com/Article/2029.shtml
- http://www.read.xwpxi.com/Article/44388.shtml
- http://www.read.xwpxi.com/Article/59356.shtml
- http://www.read.xwpxi.com/Article/45338.shtml
- http://www.read.xwpxi.com/Article/3311380.shtml
- http://www.read.xwpxi.com/Article/8228171.shtml
- http://www.read.xwpxi.com/Article/402265.shtml
- http://www.read.xwpxi.com/Article/4156.shtml
- http://www.read.xwpxi.com/Article/81040.shtml
- http://www.read.xwpxi.com/Article/04850.shtml
- http://www.read.xwpxi.com/Article/4430.shtml
- http://www.read.xwpxi.com/Article/8352.shtml
- http://www.read.xwpxi.com/Article/9508581.shtml
- http://www.read.xwpxi.com/Article/94996.shtml
- http://www.read.xwpxi.com/Article/0740330.shtml
- http://www.read.xwpxi.com/Article/539308.shtml
- http://www.read.xwpxi.com/Article/3544595.shtml
- http://www.read.xwpxi.com/Article/8323794.shtml
- http://www.read.xwpxi.com/Article/13108.shtml
- http://www.read.xwpxi.com/Article/93768.shtml
- http://www.read.xwpxi.com/Article/65868.shtml
- http://www.read.xwpxi.com/Article/53147.shtml
- http://www.read.xwpxi.com/Article/336239.shtml
- http://www.read.xwpxi.com/Article/6394.shtml
- http://www.read.xwpxi.com/Article/3549112.shtml
- http://www.read.xwpxi.com/Article/2249709.shtml
- http://www.read.xwpxi.com/Article/65553.shtml
- http://www.read.xwpxi.com/Article/45509.shtml
- http://www.read.xwpxi.com/Article/914337.shtml
- http://www.read.xwpxi.com/Article/6546.shtml
- http://www.read.xwpxi.com/Article/580179.shtml
- http://www.read.xwpxi.com/Article/9768919.shtml
- http://www.read.xwpxi.com/Article/7514.shtml
- http://www.read.xwpxi.com/Article/797138.shtml
- http://www.read.xwpxi.com/Article/299711.shtml
- http://www.read.xwpxi.com/Article/0274.shtml
- http://www.read.xwpxi.com/Article/39015.shtml
- http://www.read.xwpxi.com/Article/2382.shtml
- http://www.read.xwpxi.com/Article/3296267.shtml
- http://www.read.xwpxi.com/Article/536120.shtml
- http://www.read.xwpxi.com/Article/0612129.shtml
- http://www.read.xwpxi.com/Article/379226.shtml
- http://www.read.xwpxi.com/Article/504855.shtml
- http://www.read.xwpxi.com/Article/11882.shtml
- http://www.read.xwpxi.com/Article/8239284.shtml
- http://www.read.xwpxi.com/Article/996304.shtml
- http://www.read.xwpxi.com/Article/7519.shtml
- http://www.read.xwpxi.com/Article/2951.shtml
- http://www.read.xwpxi.com/Article/2471693.shtml
- http://www.read.xwpxi.com/Article/96912.shtml
- http://www.read.xwpxi.com/Article/8633716.shtml
- http://www.read.xwpxi.com/Article/6586.shtml
- http://www.read.xwpxi.com/Article/2685976.shtml
- http://www.read.xwpxi.com/Article/8009.shtml
- http://www.read.xwpxi.com/Article/456758.shtml
- http://www.read.xwpxi.com/Article/0659726.shtml
- http://www.read.xwpxi.com/Article/98514.shtml
- http://www.read.xwpxi.com/Article/43226.shtml
- http://www.read.xwpxi.com/Article/4867567.shtml
- http://www.read.xwpxi.com/Article/4059850.shtml
- http://www.read.xwpxi.com/Article/7124.shtml
- http://www.read.xwpxi.com/Article/711650.shtml
- http://www.read.xwpxi.com/Article/5007.shtml
- http://www.read.xwpxi.com/Article/9758392.shtml
- http://www.read.xwpxi.com/Article/86588.shtml
- http://www.read.xwpxi.com/Article/062584.shtml
- http://www.read.xwpxi.com/Article/9742.shtml
- http://www.read.xwpxi.com/Article/953992.shtml
- http://www.read.xwpxi.com/Article/239783.shtml
- http://www.read.xwpxi.com/Article/820292.shtml
- http://www.read.xwpxi.com/Article/36493.shtml
- http://www.read.xwpxi.com/Article/5113084.shtml
- http://www.read.xwpxi.com/Article/86513.shtml
- http://www.read.xwpxi.com/Article/2265684.shtml
- http://www.read.xwpxi.com/Article/8447088.shtml
- http://www.read.xwpxi.com/Article/47871.shtml
- http://www.read.xwpxi.com/Article/9967.shtml
- http://www.read.xwpxi.com/Article/9463778.shtml
- http://www.read.xwpxi.com/Article/79770.shtml
- http://www.read.xwpxi.com/Article/52960.shtml
- http://www.read.xwpxi.com/Article/4718.shtml
- http://www.read.xwpxi.com/Article/20127.shtml
- http://www.read.xwpxi.com/Article/967540.shtml
- http://www.read.xwpxi.com/Article/8116695.shtml
- http://www.read.xwpxi.com/Article/8320.shtml
- http://www.read.xwpxi.com/Article/121974.shtml
- http://www.read.xwpxi.com/Article/49867.shtml
- http://www.read.xwpxi.com/Article/6383664.shtml
- http://www.read.xwpxi.com/Article/6588.shtml
- http://www.read.xwpxi.com/Article/1642.shtml
- http://www.read.xwpxi.com/Article/43794.shtml
- http://www.read.xwpxi.com/Article/3092.shtml
- http://www.read.xwpxi.com/Article/7270565.shtml
- http://www.read.xwpxi.com/Article/1831904.shtml
- http://www.read.xwpxi.com/Article/1163604.shtml
- http://www.read.xwpxi.com/Article/5002497.shtml
- http://www.read.xwpxi.com/Article/9863.shtml
- http://www.read.xwpxi.com/Article/0070.shtml
- http://www.read.xwpxi.com/Article/87962.shtml

## 项目结构

```
weblink-collective/
├── cli.py                      # 命令行入口，注册所有子命令
├── config.example.yaml         # 配置文件模板，包含检测参数与存储后端设置
├── requirements.txt            # Python 依赖清单
├── setup.py                    # 项目安装与打包配置
├── src/                        # 核心源代码目录
│   ├── core/                   # 核心业务逻辑层
│   │   ├── importer.py         # URL 导入与解析引擎
│   │   ├── checker.py          # 异步链接状态检测器
│   │   ├── extractor.py        # 页面元数据提取器
│   │   └── exporter.py         # 数据导出格式化器
│   ├── models/                 # 数据模型与数据结构定义
│   │   ├── url_entry.py        # URL 条目模型，包含地址、状态、标签等字段
│   │   ├── batch.py            # 批次模型，管理批次元数据与统计信息
│   │   └── snapshot.py         # 索引快照模型，用于版本追踪
│   ├── storage/                # 存储适配器层
│   │   ├── local.py            # 本地文件系统存储实现
│   │   ├── redis.py            # Redis 缓存存储实现
│   │   └── postgres.py         # PostgreSQL 持久化存储实现
│   ├── api/                    # RESTful API 服务模块
│   │   ├── app.py              # FastAPI 应用实例与路由注册
│   │   ├── endpoints/          # 各资源端点实现
│   │   │   ├── batches.py      # 批次管理接口
│   │   │   └── entries.py      # 条目查询与筛选接口
│   │   └── schemas.py          # Pydantic 请求与响应模型
│   └── utils/                  # 通用工具函数集合
│       ├── http.py             # 异步 HTTP 客户端封装
│       ├── parser.py           # URL 解析与规范化工具
│       └── logger.py           # 统一日志配置与输出格式
├── tests/                      # 单元测试与集成测试目录
│   ├── test_importer.py        # 导入引擎测试用例
│   ├── test_checker.py         # 检测器测试用例，含模拟响应
│   └── test_api.py             # API 接口测试用例
├── docs/                       # 完整项目文档目录
│   ├── user-guide/             # 用户手册分章节
│   ├── api-reference.md        # API 详细参考文档
│   └── developer-guide/        # 开发者扩展指南
└── scripts/                    # 运维与辅助脚本
    ├── migrate_db.py           # 数据库迁移脚本
    └── batch_import.sh         # 批量导入自动化 shell 脚本
```

## 贡献指南

贡献者应首先阅读项目行为准则并在提交前签署贡献者许可协议。所有代码贡献需通过拉取请求流程提交，并确保通过全部单元测试。

开发环境准备：克隆代码仓库后，使用 Python 3.10 创建虚拟环境，执行 pip install -e .[dev] 安装开发依赖，并复制 config.example.yaml 为 config.yaml 进行本地配置。

测试用例编写：新增功能或修复缺陷时，应在 tests/ 目录下对应的测试文件中补充测试用例，确保代码覆盖率达到 80% 以上。测试执行使用 pytest -v --cov=src 命令。

拉取请求提交：分支命名遵循 feature/xxx 或 fix/xxx 格式，提交信息使用约定式提交规范。拉取请求描述中应清晰说明变更内容、测试结果与相关文档更新。

文档同步更新：涉及用户可见变更时，需同步更新 docs/ 目录下的相关文档，并在拉取请求中标注文档变更情况。API 变更需同步修改 api-reference.md 中的接口说明。

## 常见问题

问：导入包含大量 URL 的文件时，如何处理网络波动导致的部分检测失败？

答：检测器内置了指数退避重试机制，默认重试 3 次，每次重试间隔递增。用户可通过 --retry 参数调整重试次数，或通过 --timeout 调整单次请求超时时间。对于持续失败的链接，系统会将其标记为 UNREACHABLE 状态并记录失败原因，不会中断整体检测流程。

问：如何迁移已存储的索引数据到新的存储后端？

答：项目提供了 storage/ 目录下的多后端适配器，数据迁移可通过导出为 JSON 快照再导入到新后端的方式完成。具体操作为：使用 export --format json --batch all 导出全部数据为 JSON 文件，然后修改 config.yaml 中的 storage 配置为新后端参数，最后使用 import --source snapshot.json --rebuild 重建索引。此过程不会丢失标签分类与检测历史记录。

问：CLI 命令执行时提示模块找不到，如何解决？

答：该问题通常是由于未以开发模式安装项目导致。请确保在项目根目录下执行 pip install -e . 完成安装。如果使用虚拟环境，确认虚拟环境已激活。对于自定义模块路径问题，可设置 PYTHONPATH=. 环境变量后重试。仍无法解决时，请检查 requirements.txt 中所有依赖是否已正确安装。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
