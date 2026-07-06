# LinkArchive Core

LinkArchive Core 是一个面向技术文档维护者、知识库运营者和互联网档案馆志愿者的结构化外链归档与校验工具集。该项目不提供可视化界面，而是以命令行管道、结构化日志和可插拔校验规则为核心，帮助用户在批量收录外部文章链接时，自动检测链接可用性、提取元数据、生成归档报告，并维持一套可版本化的链接清单。

LinkArchive Core 定位为“链接基础设施”，适用于需要长期维护大量外链引用的项目，例如技术周报、开源文档站、学术资源导航、合规存档系统等。它不绑定任何特定数据库，默认以 JSON Lines 和 SQLite 作为存储后端，可被集成到 GitHub Actions、Airflow 或简单的 cron 任务中。

## 功能概览

批量链接存活检测：支持 HTTP/HTTPS 状态码检查、重定向追踪、超时与 TLS 握手异常捕获，并记录每次检测的时间戳与响应耗时。

元数据智能抽取：从目标页面自动提取标题、字符编码、内容摘要哈希、最后修改时间头，并识别站点使用的 CMS 类型（如 WordPress、DokuWiki、XenForo）。

链接变更追踪：通过对比历史记录，标记链接的“新增”“失效”“恢复”“重定向目标变更”四种状态，便于生成变更摘要。

结构化输入输出：输入支持纯文本列表、CSV、JSON Lines 以及 SQLite 查询结果；输出支持 Markdown 报告、JSON 摘要、SQLite 归档表、Grafana 兼容的指标端点。

过滤与去重规则引擎：支持基于域名、路径前缀、正则表达式、MIME 类型、状态码范围的包含/排除规则，并可自动去重（按 URL 规范化后的键值）。

断点续跑与并发控制：支持中断恢复，检测队列可持久化到磁盘；同时支持用户配置并发工作线程数（1-32），避免对目标站点造成过大压力。

容器化与无状态设计：官方提供 Docker 镜像，所有配置通过环境变量或 YAML 配置文件传入，运行日志以 structured logging 输出到 stdout/stderr。

扩展脚本钩子：允许用户在“检测前”“检测后”“状态变更时”三个时机调用外部 shell 脚本或 Python 函数，便于对接自定义通知系统（如邮件、Telegram）。

## 应用场景

技术文档站的每日外链巡检：维护者设定每日凌晨 2 点运行全量检测，若发现 404 或 5xx 链接，自动生成 Markdown 报告并提交至文档仓库的 issue 列表，帮助文档团队在用户反馈之前修复断链。

开源项目 README 中的引用链接审计：在项目发布新版前，通过 CI 流水线执行 LinkArchive Core 对 README 中所有外链进行一次快速检测，确保所有“快速开始”“参考文档”“致谢”部分的链接均有效。

互联网档案馆志愿者的批量链接预处理：志愿者在抓取网页前，先用 LinkArchive Core 对目标链接列表进行存活初筛，排除明显失效或超时的链接，减少抓取队列中的无用任务，提升存档效率。

合规部门的定期外链披露清单维护：金融机构或医疗机构需要定期公开其对外引用的全部链接。LinkArchive Core 可以按照月度周期生成一份完整的外链清单，并附带每次检测的状态记录，作为合规备案材料。

知识库迁移过程中的链接清洗：当企业将旧 wiki 迁移到新知识库平台时，使用 LinkArchive Core 扫描旧系统中的所有外链，找出哪些引用已经失效，哪些域名需要加入白名单，哪些资源应被内联化处理。

## 快速开始

以下命令演示了如何在 Linux/macOS 环境中从源码启动 LinkArchive Core。

```bash
# 克隆项目仓库
git clone https://github.com/linkarchiv/linkarchive-core.git
cd linkarchive-core

# 创建并激活 Python 虚拟环境（Python 3.9 及以上）
python3 -m venv venv
source venv/bin/activate

# 安装核心依赖与 CLI 入口
pip install --upgrade pip
pip install -e .

# 运行一次基础检测（示例：检测 example.txt 中的所有链接，输出 JSON 摘要到 report.json）
linkarchive check --input lists/example.txt --output report.json --format json --workers 4
```

若使用 Docker，可跳过上述安装步骤，直接执行：

```bash
docker pull linkarchive/core:latest
docker run --rm -v $(pwd)/data:/data linkarchive/core check --input /data/links.txt --output /data/result.json
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行时，低于 3.9 将无法使用类型注解与异步特性 |
| SQLite | 3.35 及以上 | 内置归档存储后端，支持 JSON 函数和窗口函数 |
| aiohttp | 3.8.0 及以上 | 异步 HTTP 客户端，负责所有网络请求 |
| orjson | 3.9.0 及以上 | 高性能 JSON 序列化与反序列化，用于报告生成 |
| click | 8.1.0 及以上 | CLI 命令行参数解析框架 |
| pydantic | 2.0.0 及以上 | 配置模型与输入数据校验 |
| python-dotenv | 1.0.0 及以上 | 用于从 .env 文件加载配置变量 |
| pytest | 7.0.0 及以上 | 仅在开发/测试环境中需要，用于运行单元测试 |
| docker | 20.10 及以上 | 仅在构建或运行容器镜像时需要 |
| make | 3.82 及以上 | 仅在通过 Makefile 执行构建任务时需要 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user/ | 如何安装、配置、运行检测任务；如何解读报告；如何设置定时任务 |
| 配置参考 | docs/config/ | YAML 配置文件中所有字段的含义、默认值、合法取值范围；环境变量映射表 |
| 规则编写 | docs/rules/ | 过滤规则和去重规则的语法；常见域名策略示例；正则表达式库 |
| 开发指南 | docs/dev/ | 如何扩展新的校验器；如何增加输出格式；如何提交 Pull Request；测试规范 |
| API 参考 | docs/api/ | 内部模块的类图、函数签名、事件钩子接口定义（供脚本调用） |
| 故障排查 | docs/troubleshoot/ | 常见错误码含义；网络超时调整方法；SQLite 锁冲突解决；日志级别调优 |
| 版本发布 | docs/releases/ | 每个版本的变更日志、废弃特性、迁移指南和已知问题列表 |

## 资源列表

- http://www.read.rswzr.com/Article/1787064.shtml
- http://www.read.rswzr.com/Article/8448959.shtml
- http://www.read.rswzr.com/Article/073305.shtml
- http://www.read.rswzr.com/Article/973808.shtml
- http://www.read.rswzr.com/Article/037791.shtml
- http://www.read.rswzr.com/Article/7591768.shtml
- http://www.read.rswzr.com/Article/8117.shtml
- http://www.read.rswzr.com/Article/2265.shtml
- http://www.read.rswzr.com/Article/78906.shtml
- http://www.read.rswzr.com/Article/526980.shtml
- http://www.read.rswzr.com/Article/23128.shtml
- http://www.read.rswzr.com/Article/53442.shtml
- http://www.read.rswzr.com/Article/724547.shtml
- http://www.read.rswzr.com/Article/28903.shtml
- http://www.read.rswzr.com/Article/9141962.shtml
- http://www.read.rswzr.com/Article/3734233.shtml
- http://www.read.rswzr.com/Article/88676.shtml
- http://www.read.rswzr.com/Article/060727.shtml
- http://www.read.rswzr.com/Article/8249.shtml
- http://www.read.rswzr.com/Article/1842456.shtml
- http://www.read.rswzr.com/Article/4634.shtml
- http://www.read.rswzr.com/Article/31175.shtml
- http://www.read.rswzr.com/Article/4052.shtml
- http://www.read.rswzr.com/Article/75066.shtml
- http://www.read.rswzr.com/Article/2512727.shtml
- http://www.read.rswzr.com/Article/8058578.shtml
- http://www.read.rswzr.com/Article/223485.shtml
- http://www.read.rswzr.com/Article/316237.shtml
- http://www.read.rswzr.com/Article/02565.shtml
- http://www.read.rswzr.com/Article/594103.shtml
- http://www.read.rswzr.com/Article/02716.shtml
- http://www.read.rswzr.com/Article/8199199.shtml
- http://www.read.rswzr.com/Article/3375717.shtml
- http://www.read.rswzr.com/Article/1649.shtml
- http://www.read.rswzr.com/Article/4846879.shtml
- http://www.read.rswzr.com/Article/70912.shtml
- http://www.read.rswzr.com/Article/1908159.shtml
- http://www.read.rswzr.com/Article/799943.shtml
- http://www.read.rswzr.com/Article/0178787.shtml
- http://www.read.rswzr.com/Article/30666.shtml
- http://www.read.rswzr.com/Article/337455.shtml
- http://www.read.rswzr.com/Article/050938.shtml
- http://www.read.rswzr.com/Article/9900404.shtml
- http://www.read.rswzr.com/Article/80493.shtml
- http://www.read.rswzr.com/Article/5241.shtml
- http://www.read.rswzr.com/Article/134554.shtml
- http://www.read.rswzr.com/Article/907567.shtml
- http://www.read.rswzr.com/Article/37081.shtml
- http://www.read.rswzr.com/Article/9911.shtml
- http://www.read.rswzr.com/Article/141209.shtml
- http://www.read.rswzr.com/Article/6680964.shtml
- http://www.read.rswzr.com/Article/89436.shtml
- http://www.read.rswzr.com/Article/0175023.shtml
- http://www.read.rswzr.com/Article/398817.shtml
- http://www.read.rswzr.com/Article/2861.shtml
- http://www.read.rswzr.com/Article/8765.shtml
- http://www.read.rswzr.com/Article/3413337.shtml
- http://www.read.rswzr.com/Article/6976.shtml
- http://www.read.rswzr.com/Article/38123.shtml
- http://www.read.rswzr.com/Article/85973.shtml
- http://www.read.rswzr.com/Article/17855.shtml
- http://www.read.rswzr.com/Article/13320.shtml
- http://www.read.rswzr.com/Article/4876425.shtml
- http://www.read.rswzr.com/Article/0832615.shtml
- http://www.read.rswzr.com/Article/2283029.shtml
- http://www.read.rswzr.com/Article/2269213.shtml
- http://www.read.rswzr.com/Article/436694.shtml
- http://www.read.rswzr.com/Article/1690018.shtml
- http://www.read.rswzr.com/Article/31641.shtml
- http://www.read.rswzr.com/Article/670670.shtml
- http://www.read.rswzr.com/Article/1292339.shtml
- http://www.read.rswzr.com/Article/058659.shtml
- http://www.read.rswzr.com/Article/6142841.shtml
- http://www.read.rswzr.com/Article/92365.shtml
- http://www.read.rswzr.com/Article/13666.shtml
- http://www.read.rswzr.com/Article/1178.shtml
- http://www.read.rswzr.com/Article/14724.shtml
- http://www.read.rswzr.com/Article/1713.shtml
- http://www.read.rswzr.com/Article/50204.shtml
- http://www.read.rswzr.com/Article/41052.shtml
- http://www.read.rswzr.com/Article/45365.shtml
- http://www.read.rswzr.com/Article/7980.shtml
- http://www.read.rswzr.com/Article/152305.shtml
- http://www.read.rswzr.com/Article/5566798.shtml
- http://www.read.rswzr.com/Article/4727417.shtml
- http://www.read.rswzr.com/Article/4339836.shtml
- http://www.read.rswzr.com/Article/6813193.shtml
- http://www.read.rswzr.com/Article/2120966.shtml
- http://www.read.rswzr.com/Article/127357.shtml
- http://www.read.rswzr.com/Article/2778.shtml
- http://www.read.rswzr.com/Article/1973291.shtml
- http://www.read.rswzr.com/Article/934040.shtml
- http://www.read.rswzr.com/Article/22671.shtml
- http://www.read.rswzr.com/Article/66984.shtml
- http://www.read.rswzr.com/Article/5871826.shtml
- http://www.read.rswzr.com/Article/35365.shtml
- http://www.read.rswzr.com/Article/0409186.shtml
- http://www.read.rswzr.com/Article/083061.shtml
- http://www.read.rswzr.com/Article/6714170.shtml
- http://www.read.rswzr.com/Article/9981197.shtml
- http://www.read.rswzr.com/Article/8377.shtml
- http://www.read.rswzr.com/Article/8826847.shtml
- http://www.read.rswzr.com/Article/87229.shtml
- http://www.read.rswzr.com/Article/3934918.shtml
- http://www.read.rswzr.com/Article/157006.shtml
- http://www.read.rswzr.com/Article/99266.shtml
- http://www.read.rswzr.com/Article/7131142.shtml
- http://www.read.rswzr.com/Article/313325.shtml
- http://www.read.rswzr.com/Article/7496395.shtml
- http://www.read.rswzr.com/Article/04995.shtml
- http://www.read.rswzr.com/Article/4234790.shtml
- http://www.read.rswzr.com/Article/8436739.shtml
- http://www.read.rswzr.com/Article/9813.shtml
- http://www.read.rswzr.com/Article/6412.shtml
- http://www.read.rswzr.com/Article/6895699.shtml
- http://www.read.rswzr.com/Article/49728.shtml
- http://www.read.rswzr.com/Article/362271.shtml
- http://www.read.rswzr.com/Article/8866.shtml
- http://www.read.rswzr.com/Article/64535.shtml
- http://www.read.rswzr.com/Article/5918.shtml
- http://www.read.rswzr.com/Article/351175.shtml
- http://www.read.rswzr.com/Article/6088.shtml
- http://www.read.rswzr.com/Article/8197292.shtml
- http://www.read.rswzr.com/Article/8742104.shtml
- http://www.read.rswzr.com/Article/40340.shtml
- http://www.read.rswzr.com/Article/7993.shtml
- http://www.read.rswzr.com/Article/605354.shtml
- http://www.read.rswzr.com/Article/3352661.shtml
- http://www.read.rswzr.com/Article/4031093.shtml
- http://www.read.rswzr.com/Article/0325015.shtml
- http://www.read.rswzr.com/Article/4661827.shtml
- http://www.read.rswzr.com/Article/8729524.shtml
- http://www.read.rswzr.com/Article/02359.shtml
- http://www.read.rswzr.com/Article/9408.shtml
- http://www.read.rswzr.com/Article/633159.shtml
- http://www.read.rswzr.com/Article/121489.shtml
- http://www.read.rswzr.com/Article/8393619.shtml
- http://www.read.rswzr.com/Article/730972.shtml
- http://www.read.rswzr.com/Article/764861.shtml
- http://www.read.rswzr.com/Article/0356363.shtml
- http://www.read.rswzr.com/Article/6446.shtml
- http://www.read.rswzr.com/Article/0822677.shtml
- http://www.read.rswzr.com/Article/81749.shtml
- http://www.read.rswzr.com/Article/8843495.shtml
- http://www.read.rswzr.com/Article/9244.shtml
- http://www.read.rswzr.com/Article/9423062.shtml
- http://www.read.rswzr.com/Article/2044352.shtml
- http://www.read.rswzr.com/Article/870829.shtml
- http://www.read.rswzr.com/Article/225867.shtml
- http://www.read.rswzr.com/Article/1848.shtml
- http://www.read.rswzr.com/Article/134182.shtml
- http://www.read.rswzr.com/Article/4373.shtml
- http://www.read.rswzr.com/Article/731511.shtml
- http://www.read.rswzr.com/Article/7776354.shtml
- http://www.read.rswzr.com/Article/94632.shtml
- http://www.read.rswzr.com/Article/5677989.shtml
- http://www.read.rswzr.com/Article/349722.shtml
- http://www.read.rswzr.com/Article/669297.shtml
- http://www.read.rswzr.com/Article/908085.shtml
- http://www.read.rswzr.com/Article/07369.shtml
- http://www.read.rswzr.com/Article/8239273.shtml
- http://www.read.rswzr.com/Article/32922.shtml
- http://www.read.rswzr.com/Article/492009.shtml
- http://www.read.rswzr.com/Article/4495680.shtml
- http://www.read.rswzr.com/Article/321628.shtml
- http://www.read.rswzr.com/Article/92651.shtml
- http://www.read.rswzr.com/Article/16250.shtml
- http://www.read.rswzr.com/Article/3557.shtml
- http://www.read.rswzr.com/Article/7564792.shtml
- http://www.read.rswzr.com/Article/1799729.shtml
- http://www.read.rswzr.com/Article/802144.shtml
- http://www.read.rswzr.com/Article/888344.shtml
- http://www.read.rswzr.com/Article/13638.shtml
- http://www.read.rswzr.com/Article/059624.shtml
- http://www.read.rswzr.com/Article/7951.shtml
- http://www.read.rswzr.com/Article/669264.shtml
- http://www.read.rswzr.com/Article/55775.shtml
- http://www.read.rswzr.com/Article/2173.shtml
- http://www.read.rswzr.com/Article/41959.shtml
- http://www.read.rswzr.com/Article/770908.shtml
- http://www.read.rswzr.com/Article/23603.shtml
- http://www.read.rswzr.com/Article/4358.shtml
- http://www.read.rswzr.com/Article/7574408.shtml
- http://www.read.rswzr.com/Article/53922.shtml
- http://www.read.rswzr.com/Article/8780010.shtml
- http://www.read.rswzr.com/Article/1729.shtml
- http://www.read.rswzr.com/Article/3414.shtml
- http://www.read.rswzr.com/Article/440473.shtml
- http://www.read.rswzr.com/Article/03274.shtml
- http://www.read.rswzr.com/Article/0152464.shtml
- http://www.read.rswzr.com/Article/5580676.shtml
- http://www.read.rswzr.com/Article/9709.shtml
- http://www.read.rswzr.com/Article/984391.shtml
- http://www.read.rswzr.com/Article/8525.shtml
- http://www.read.rswzr.com/Article/12896.shtml
- http://www.read.rswzr.com/Article/0560.shtml
- http://www.read.rswzr.com/Article/2960397.shtml
- http://www.read.rswzr.com/Article/71226.shtml
- http://www.read.rswzr.com/Article/9531.shtml
- http://www.read.rswzr.com/Article/0766655.shtml
- http://www.read.rswzr.com/Article/70454.shtml
- http://www.read.rswzr.com/Article/49541.shtml
- http://www.read.rswzr.com/Article/0155.shtml
- http://www.read.rswzr.com/Article/9438.shtml
- http://www.read.rswzr.com/Article/7917159.shtml
- http://www.read.rswzr.com/Article/1219540.shtml
- http://www.read.rswzr.com/Article/8130912.shtml
- http://www.read.rswzr.com/Article/94705.shtml
- http://www.read.rswzr.com/Article/7809676.shtml
- http://www.read.rswzr.com/Article/00148.shtml
- http://www.read.rswzr.com/Article/37337.shtml
- http://www.read.rswzr.com/Article/818429.shtml
- http://www.read.rswzr.com/Article/9603.shtml
- http://www.read.rswzr.com/Article/23422.shtml
- http://www.read.rswzr.com/Article/6439.shtml
- http://www.read.rswzr.com/Article/38292.shtml
- http://www.read.rswzr.com/Article/0343365.shtml
- http://www.read.rswzr.com/Article/5363108.shtml
- http://www.read.rswzr.com/Article/3467269.shtml
- http://www.read.rswzr.com/Article/9981281.shtml
- http://www.read.rswzr.com/Article/157885.shtml
- http://www.read.rswzr.com/Article/3045238.shtml
- http://www.read.rswzr.com/Article/5803.shtml
- http://www.read.rswzr.com/Article/3798.shtml
- http://www.read.rswzr.com/Article/73911.shtml
- http://www.read.rswzr.com/Article/0700.shtml
- http://www.read.rswzr.com/Article/1923.shtml
- http://www.read.rswzr.com/Article/85191.shtml
- http://www.read.rswzr.com/Article/20121.shtml
- http://www.read.rswzr.com/Article/9800.shtml
- http://www.read.rswzr.com/Article/490679.shtml
- http://www.read.rswzr.com/Article/105818.shtml
- http://www.read.rswzr.com/Article/9197.shtml
- http://www.read.rswzr.com/Article/030281.shtml
- http://www.read.rswzr.com/Article/8327.shtml
- http://www.read.rswzr.com/Article/1516814.shtml
- http://www.read.rswzr.com/Article/2593984.shtml
- http://www.read.rswzr.com/Article/42038.shtml
- http://www.read.rswzr.com/Article/1449.shtml
- http://www.read.rswzr.com/Article/852303.shtml
- http://www.read.rswzr.com/Article/581125.shtml
- http://www.read.rswzr.com/Article/3790.shtml
- http://www.read.rswzr.com/Article/867097.shtml
- http://www.read.rswzr.com/Article/814125.shtml
- http://www.read.rswzr.com/Article/65252.shtml
- http://www.read.rswzr.com/Article/29805.shtml
- http://www.read.rswzr.com/Article/5621030.shtml
- http://www.read.rswzr.com/Article/1956853.shtml
- http://www.read.rswzr.com/Article/229469.shtml
- http://www.read.rswzr.com/Article/83363.shtml

## 项目结构

```
linkarchive-core/
├── cmd/
│   ├── linkarchive/                # CLI 主入口，封装 click 命令组
│   │   ├── main.py                 # 命令解析与全局上下文初始化
│   │   ├── check.py                # check 子命令实现
│   │   ├── report.py               # report 子命令实现
│   │   └── archive.py              # archive 子命令实现（写入 SQLite）
├── internal/
│   ├── checker/                    # 核心校验引擎
│   │   ├── http_checker.py         # aiohttp 异步请求封装，含重试与超时策略
│   │   ├── rules_engine.py         # 包含/排除规则匹配器
│   │   └── status_tracker.py       # 状态变更判定逻辑（新增/失效/恢复/重定向）
│   ├── metadata/                   # 元数据抽取模块
│   │   ├── html_parser.py          # 基于 lxml 的标题与编码提取
│   │   ├── cms_detector.py         # 通过 meta 标签和特定路径识别 CMS
│   │   └── content_hasher.py       # 计算响应体的内容哈希（用于内容变更检测）
│   ├── storage/                    # 存储适配器
│   │   ├── sqlite_repo.py          # SQLite 表创建、插入、查询、增量更新
│   │   ├── jsonl_repo.py           # JSON Lines 读写，用于轻量级批量导入导出
│   │   └── schema.sql              # SQLite 初始化脚本（含索引与触发器）
│   ├── queue/                      # 任务队列持久化
│   │   ├── disk_queue.py           # 基于磁盘的 FIFO 队列（支持中断恢复）
│   │   └── worker_pool.py          # 异步工作线程池管理
│   └── config/                     # 配置加载
│       ├── loader.py               # YAML + .env + 默认值三层合并
│       └── validators.py           # pydantic 模型，校验 workers、timeout、重试次数
├── pkg/
│   ├── logger/                     # 结构化日志封装
│   │   └── logger.py               # 基于 logging + json 格式输出
│   └── metrics/                    # 内部指标暴露（Prometheus 兼容）
│       └── exporter.py             # 暴露运行计数、成功率、平均耗时
├── scripts/
│   ├── pre_check.sh                # 检测前钩子示例（如拉取最新链接列表）
│   ├── post_report.py              # 检测后钩子示例（发送企业微信通知）
│   └── on_change.py                # 状态变更钩子示例（记录变更到单独文件）
├── docker/
│   ├── Dockerfile                  # 多阶段构建，基于 alpine
│   └── docker-compose.yml          # 本地测试环境，挂载数据卷并带 cron 示例
├── tests/
│   ├── unit/                       # 单元测试（pytest，覆盖规则引擎与存储层）
│   ├── integration/                # 集成测试（需启动本地 mock 服务器）
│   └── fixtures/                   # 测试用样例输入、预期输出
├── docs/                           # 完整文档（见上节文档导航）
├── lists/                          # 存放示例输入链接列表文件
│   └── example.txt                 # 每行一个 URL 的示例文件
├── .env.example                    # 环境变量模板（包含所有可覆盖配置项）
├── Makefile                        # 构建、测试、格式化的快捷指令
├── pyproject.toml                  # 项目元信息、依赖声明、工具配置
└── README.md                       # 本文件
```

## 贡献指南

贡献者需要先阅读项目行为准则（CODE_OF_CONDUCT.md）和开发者证书（DCO）。具体贡献流程如下：

提交问题报告或功能请求前，请先查阅现有 issue 列表，避免重复。若确认是新问题，请使用提供的 issue 模板，详细描述复现步骤、环境信息、预期行为和实际行为。

本地开发环境准备：克隆仓库后，运行 `make setup-dev` 创建虚拟环境并安装所有开发依赖（包括 pytest、black、mypy、pre-commit）。所有代码提交前必须通过 `make lint` 和 `make test` 检查。

为新增功能编写单元测试：所有校验逻辑、规则匹配、存储操作必须有对应的单元测试，覆盖率不低于 85%。集成测试需放置在 `tests/integration` 下，并注明是否需要外部网络。

提交 Pull Request 时，请确保分支名称以 `feature/`、`fix/` 或 `docs/` 为前缀，PR 描述中必须引用相关 issue 编号，并附上变更摘要和测试结果截图或日志片段。

文档更新与代码变更同步：若新增配置项、命令参数或钩子接口，必须在 `docs/` 对应目录下同步更新文档，并在 PR 中标注“文档已更新”。

## 常见问题

检测过程中出现大量超时错误，如何调整？

超时错误通常由目标服务器响应慢或网络抖动引起。可以通过配置文件中的 `checker.timeout` 字段调整单次请求超时时间（默认 10 秒），同时增大 `checker.retry` 重试次数（默认 3 次）。若仍无效，可降低 `workers` 并发数以减少目标服务器压力，并检查是否被目标站点防火墙拦截。

SQLite 数据库文件在并发写入时出现锁错误，如何解决？

SQLite 在默认配置下不支持高并发写入。LinkArchive Core 内部已使用 WAL 模式并设置 `busy_timeout` 为 5000 毫秒。若仍频繁出现锁错误，建议将存储后端切换为 JSON Lines 模式（`--format jsonl`）进行单次检测，或使用外部 PostgreSQL/MySQL 作为存储（通过扩展模块实现，参见文档开发指南）。

如何只检测链接状态而不抽取元数据，以提升速度？

可以通过 `--skip-metadata` 命令行标志或在配置文件中设置 `metadata.enabled: false`。此模式下，请求将使用 HEAD 方法而非 GET 方法（需目标服务器支持），并跳过 HTML 解析和内容哈希计算，可显著减少网络流量和 CPU 占用，适用于仅关注存活性的大批量检测任务。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
