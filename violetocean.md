# WebLink Archive Registry

WebLink Archive Registry 是一个面向技术文档、开源资料与互联网历史资源的高密度外链归档与结构化检索系统。项目定位于为开发者、研究人员及内容策展人提供稳定、可追溯、可编程访问的 URL 元数据集合。本仓库不对具体文章内容进行复刻或重分发，而是围绕一组经过人工筛选的原始链接构建索引层、校验层与示例应用层，帮助用户在信息碎片化环境中快速定位高价值外链，并降低链接失效带来的研究成本。

目标用户包括：需要批量处理外部链接的数据工程师、搭建个人知识库的技术作者、对特定域名进行长期引用跟踪的信息分析人员，以及希望基于既有链接集合构建推荐系统或可视化图谱的开源开发者。项目核心交付物为一套结构化的链接清单、若干辅助工具脚本以及完整的中英文文档框架，可作为更大规模外链治理项目的基础设施组件。

## 功能概览

**批量链接导入与去重** 提供基于文本文件或 CSV 的批量 URL 注入接口，自动执行协议归一化与去重逻辑，保留原始输入顺序的同时生成唯一索引标识。

**域名归属与状态探测** 内置异步 HTTP 探针，支持对每条链接返回状态码、响应时间与内容类型摘要，帮助用户快速识别失效链接或重定向链路。

**标签化分类与全文检索** 允许用户为每条链接附加多个自定义标签，并基于 SQLite 全文搜索实现标题级与 URL 级别的模糊匹配，适用于快速筛选特定主题或来源。

**结构化数据导出** 支持将当前索引库导出为 JSON、CSV 或 Markdown 表格格式，便于下游系统集成或离线备份。导出过程可指定字段子集与排序规则。

**变更日志与快照对比** 每次运行探针后自动生成变更报告，标注新增、失效、状态码变化的链接，并支持与历史快照进行差异对比，便于长期监控。

**RESTful API 查询接口** 基于 Flask 提供轻量级只读 API，支持按 ID、标签、域名前缀或状态码范围进行查询，返回 JSON 格式结果，适合嵌入仪表板或自动化脚本。

**定时任务调度示例** 包含针对 Linux cron 与 Windows Task Scheduler 的配置文件模板，可实现每日或每周自动刷新链接状态，确保索引库与实际资源保持同步。

## 应用场景

**技术博客外链整理** 技术作者在撰写年度回顾或专题综述时，可将散落在各草稿中的参考链接统一录入本系统，借助标签体系按主题分类，并在发布前批量检查所有外部引用是否可访问，避免读者遇到死链。

**开源项目依赖文档追溯** 开源项目的 README 或 Wiki 中常引用大量第三方教程、规范文档与工具站点。维护者可利用本仓库的导入功能快速建立依赖链接清单，并结合状态探测定期收到失效通知，及时更新文档中的引用地址。

**学术研究数据溯源** 社会科学或计算机科学领域的研究人员在进行文献计量分析或网络内容演变研究时，需要保存大量被引用的网页地址。本项目的快照对比功能可帮助记录链接在时间维度上的可用性变化，为论文附录提供可验证的数据支撑。

**企业知识库外链治理** 企业内部 Wiki 或知识管理平台往往积累了大量外部链接。通过本系统的批量导出与标签管理，知识管理员可以按部门或项目维度整理外链资产，生成可分享的链接目录，并在定期的健康检查中识别风险链接。

## 快速开始

以下指令适用于 Linux / macOS 环境，Windows 用户可使用 WSL 或 Git Bash 执行。

```bash
# 克隆仓库
git clone https://github.com/weblink-archive/registry.git
cd registry

# 创建并激活 Python 虚拟环境
python3 -m venv venv
source venv/bin/activate

# 安装核心依赖
pip install -r requirements.txt

# 初始化 SQLite 数据库并导入示例链接
python scripts/init_db.py
python scripts/import_links.py --input data/sample_urls.txt

# 运行状态探测（默认并发数 10）
python scripts/probe_links.py --concurrency 10

# 启动本地 API 服务（默认端口 5000）
python app.py
```

访问 http://127.0.0.1:5000/api/links 可获取当前索引库中的全部链接元数据。如需修改端口或调试级别，请编辑 config.py 文件。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，低于 3.9 将无法使用异步语法特性 |
| SQLite | 3.31 及以上 | 内置数据库，支持全文搜索 FTS5 扩展 |
| aiohttp | 3.8.4 及以上 | 异步 HTTP 客户端，用于并发链接探测 |
| Flask | 2.2.0 及以上 | API 服务框架，提供 RESTful 接口 |
| pandas | 1.5.0 及以上 | 用于数据导出与表格格式转换 |
| 网络连接 | 稳定出站访问 | 执行探针时需要访问外部域名，需确保防火墙允许出站 80/443 端口 |
| 磁盘空间 | 至少 200 MB | 用于存放 SQLite 数据库文件与日志，实际需求随链接数量线性增长 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/quickstart.md | 如何在 10 分钟内完成首次导入并看到探测结果；如何理解控制台输出的状态码含义 |
| 数据模型 | docs/schema.md | 链接表、标签表、快照表之间的关联关系；各字段的存储类型与索引策略 |
| API 参考 | docs/api_reference.md | 每个端点的路径、参数、返回样例及错误码说明；如何通过 curl 调用查询接口 |
| 运维手册 | docs/operations.md | 如何调整并发数避免被目标网站封禁；如何手动清理无效历史快照以节省存储空间 |

## 资源列表

- http://www.read.rswzr.com/Article/2369891.shtml
- http://www.read.rswzr.com/Article/9521.shtml
- http://www.read.rswzr.com/Article/2670585.shtml
- http://www.read.rswzr.com/Article/7455.shtml
- http://www.read.rswzr.com/Article/4004.shtml
- http://www.read.rswzr.com/Article/9124032.shtml
- http://www.read.rswzr.com/Article/0078.shtml
- http://www.read.rswzr.com/Article/186901.shtml
- http://www.read.rswzr.com/Article/678844.shtml
- http://www.read.rswzr.com/Article/972028.shtml
- http://www.read.rswzr.com/Article/536810.shtml
- http://www.read.rswzr.com/Article/979805.shtml
- http://www.read.rswzr.com/Article/26291.shtml
- http://www.read.rswzr.com/Article/16653.shtml
- http://www.read.rswzr.com/Article/18014.shtml
- http://www.read.rswzr.com/Article/2903.shtml
- http://www.read.rswzr.com/Article/34968.shtml
- http://www.read.rswzr.com/Article/0495.shtml
- http://www.read.rswzr.com/Article/998944.shtml
- http://www.read.rswzr.com/Article/7317.shtml
- http://www.read.rswzr.com/Article/736070.shtml
- http://www.read.rswzr.com/Article/56394.shtml
- http://www.read.rswzr.com/Article/1069772.shtml
- http://www.read.rswzr.com/Article/058386.shtml
- http://www.read.rswzr.com/Article/4816270.shtml
- http://www.read.rswzr.com/Article/0982344.shtml
- http://www.read.rswzr.com/Article/042363.shtml
- http://www.read.rswzr.com/Article/255422.shtml
- http://www.read.rswzr.com/Article/9220.shtml
- http://www.read.rswzr.com/Article/0317.shtml
- http://www.read.rswzr.com/Article/0030192.shtml
- http://www.read.rswzr.com/Article/9783.shtml
- http://www.read.rswzr.com/Article/151915.shtml
- http://www.read.rswzr.com/Article/90449.shtml
- http://www.read.rswzr.com/Article/7506389.shtml
- http://www.read.rswzr.com/Article/54697.shtml
- http://www.read.rswzr.com/Article/194046.shtml
- http://www.read.rswzr.com/Article/48085.shtml
- http://www.read.rswzr.com/Article/232223.shtml
- http://www.read.rswzr.com/Article/648347.shtml
- http://www.read.rswzr.com/Article/6657.shtml
- http://www.read.rswzr.com/Article/4599374.shtml
- http://www.read.rswzr.com/Article/179927.shtml
- http://www.read.rswzr.com/Article/0639.shtml
- http://www.read.rswzr.com/Article/374543.shtml
- http://www.read.rswzr.com/Article/04460.shtml
- http://www.read.rswzr.com/Article/34856.shtml
- http://www.read.rswzr.com/Article/67334.shtml
- http://www.read.rswzr.com/Article/0493764.shtml
- http://www.read.rswzr.com/Article/3887.shtml
- http://www.read.rswzr.com/Article/595656.shtml
- http://www.read.rswzr.com/Article/4224578.shtml
- http://www.read.rswzr.com/Article/962120.shtml
- http://www.read.rswzr.com/Article/2079774.shtml
- http://www.read.rswzr.com/Article/6102907.shtml
- http://www.read.rswzr.com/Article/95732.shtml
- http://www.read.rswzr.com/Article/220246.shtml
- http://www.read.rswzr.com/Article/7234.shtml
- http://www.read.rswzr.com/Article/2630.shtml
- http://www.read.rswzr.com/Article/84307.shtml
- http://www.read.rswzr.com/Article/7854.shtml
- http://www.read.rswzr.com/Article/173163.shtml
- http://www.read.rswzr.com/Article/40230.shtml
- http://www.read.rswzr.com/Article/48554.shtml
- http://www.read.rswzr.com/Article/7790247.shtml
- http://www.read.rswzr.com/Article/3710.shtml
- http://www.read.rswzr.com/Article/840581.shtml
- http://www.read.rswzr.com/Article/0958028.shtml
- http://www.read.rswzr.com/Article/3904589.shtml
- http://www.read.rswzr.com/Article/6833633.shtml
- http://www.read.rswzr.com/Article/3986.shtml
- http://www.read.rswzr.com/Article/664513.shtml
- http://www.read.rswzr.com/Article/48754.shtml
- http://www.read.rswzr.com/Article/0164.shtml
- http://www.read.rswzr.com/Article/48247.shtml
- http://www.read.rswzr.com/Article/3621.shtml
- http://www.read.rswzr.com/Article/94967.shtml
- http://www.read.rswzr.com/Article/96019.shtml
- http://www.read.rswzr.com/Article/190652.shtml
- http://www.read.rswzr.com/Article/682956.shtml
- http://www.read.rswzr.com/Article/4773.shtml
- http://www.read.rswzr.com/Article/2100973.shtml
- http://www.read.rswzr.com/Article/37003.shtml
- http://www.read.rswzr.com/Article/42506.shtml
- http://www.read.rswzr.com/Article/39004.shtml
- http://www.read.rswzr.com/Article/832196.shtml
- http://www.read.rswzr.com/Article/0127.shtml
- http://www.read.rswzr.com/Article/214442.shtml
- http://www.read.rswzr.com/Article/4904.shtml
- http://www.read.rswzr.com/Article/4610872.shtml
- http://www.read.rswzr.com/Article/0139386.shtml
- http://www.read.rswzr.com/Article/99154.shtml
- http://www.read.rswzr.com/Article/1421.shtml
- http://www.read.rswzr.com/Article/2494.shtml
- http://www.read.rswzr.com/Article/70751.shtml
- http://www.read.rswzr.com/Article/7168451.shtml
- http://www.read.rswzr.com/Article/772986.shtml
- http://www.read.rswzr.com/Article/8036.shtml
- http://www.read.rswzr.com/Article/4440.shtml
- http://www.read.rswzr.com/Article/3809.shtml
- http://www.read.rswzr.com/Article/085875.shtml
- http://www.read.rswzr.com/Article/4194576.shtml
- http://www.read.rswzr.com/Article/442509.shtml
- http://www.read.rswzr.com/Article/7566.shtml
- http://www.read.rswzr.com/Article/44796.shtml
- http://www.read.rswzr.com/Article/8535018.shtml
- http://www.read.rswzr.com/Article/77594.shtml
- http://www.read.rswzr.com/Article/996218.shtml
- http://www.read.rswzr.com/Article/13055.shtml
- http://www.read.rswzr.com/Article/422003.shtml
- http://www.read.rswzr.com/Article/7914710.shtml
- http://www.read.rswzr.com/Article/34278.shtml
- http://www.read.rswzr.com/Article/3919400.shtml
- http://www.read.rswzr.com/Article/725411.shtml
- http://www.read.rswzr.com/Article/0802.shtml
- http://www.read.rswzr.com/Article/2620386.shtml
- http://www.read.rswzr.com/Article/94219.shtml
- http://www.read.rswzr.com/Article/896434.shtml
- http://www.read.rswzr.com/Article/1198970.shtml
- http://www.read.rswzr.com/Article/071272.shtml
- http://www.read.rswzr.com/Article/122808.shtml
- http://www.read.rswzr.com/Article/9383.shtml
- http://www.read.rswzr.com/Article/761768.shtml
- http://www.read.rswzr.com/Article/0058.shtml
- http://www.read.rswzr.com/Article/1022.shtml
- http://www.read.rswzr.com/Article/5726875.shtml
- http://www.read.rswzr.com/Article/7016265.shtml
- http://www.read.rswzr.com/Article/8666.shtml
- http://www.read.rswzr.com/Article/4252089.shtml
- http://www.read.rswzr.com/Article/46896.shtml
- http://www.read.rswzr.com/Article/300974.shtml
- http://www.read.rswzr.com/Article/914606.shtml
- http://www.read.rswzr.com/Article/7061.shtml
- http://www.read.rswzr.com/Article/4276269.shtml
- http://www.read.rswzr.com/Article/75379.shtml
- http://www.read.rswzr.com/Article/85932.shtml
- http://www.read.rswzr.com/Article/094236.shtml
- http://www.read.rswzr.com/Article/17970.shtml
- http://www.read.rswzr.com/Article/838467.shtml
- http://www.read.rswzr.com/Article/87988.shtml
- http://www.read.rswzr.com/Article/796638.shtml
- http://www.read.rswzr.com/Article/0875.shtml
- http://www.read.rswzr.com/Article/5154.shtml
- http://www.read.rswzr.com/Article/69989.shtml
- http://www.read.rswzr.com/Article/590381.shtml
- http://www.read.rswzr.com/Article/51104.shtml
- http://www.read.rswzr.com/Article/32898.shtml
- http://www.read.rswzr.com/Article/6118.shtml
- http://www.read.rswzr.com/Article/12154.shtml
- http://www.read.rswzr.com/Article/439510.shtml
- http://www.read.rswzr.com/Article/4474357.shtml
- http://www.read.rswzr.com/Article/274828.shtml
- http://www.read.rswzr.com/Article/280934.shtml
- http://www.read.rswzr.com/Article/60077.shtml
- http://www.read.rswzr.com/Article/89261.shtml
- http://www.read.rswzr.com/Article/256373.shtml
- http://www.read.rswzr.com/Article/1497073.shtml
- http://www.read.rswzr.com/Article/99434.shtml
- http://www.read.rswzr.com/Article/19044.shtml
- http://www.read.rswzr.com/Article/486313.shtml
- http://www.read.rswzr.com/Article/756341.shtml
- http://www.read.rswzr.com/Article/508880.shtml
- http://www.read.rswzr.com/Article/5239514.shtml
- http://www.read.rswzr.com/Article/122690.shtml
- http://www.read.rswzr.com/Article/016618.shtml
- http://www.read.rswzr.com/Article/487065.shtml
- http://www.read.rswzr.com/Article/34975.shtml
- http://www.read.rswzr.com/Article/2049546.shtml
- http://www.read.rswzr.com/Article/7596810.shtml
- http://www.read.rswzr.com/Article/5423.shtml
- http://www.read.rswzr.com/Article/1258266.shtml
- http://www.read.rswzr.com/Article/1627408.shtml
- http://www.read.rswzr.com/Article/807462.shtml
- http://www.read.rswzr.com/Article/2027.shtml
- http://www.read.rswzr.com/Article/2560393.shtml
- http://www.read.rswzr.com/Article/0217820.shtml
- http://www.read.rswzr.com/Article/9329.shtml
- http://www.read.rswzr.com/Article/92947.shtml
- http://www.read.rswzr.com/Article/5859509.shtml
- http://www.read.rswzr.com/Article/2062.shtml
- http://www.read.rswzr.com/Article/6545.shtml
- http://www.read.rswzr.com/Article/050970.shtml
- http://www.read.rswzr.com/Article/6538.shtml
- http://www.read.rswzr.com/Article/9669.shtml
- http://www.read.rswzr.com/Article/2786895.shtml
- http://www.read.rswzr.com/Article/2534.shtml
- http://www.read.rswzr.com/Article/4985060.shtml
- http://www.read.rswzr.com/Article/223549.shtml
- http://www.read.rswzr.com/Article/236970.shtml
- http://www.read.rswzr.com/Article/8746.shtml
- http://www.read.rswzr.com/Article/1180.shtml
- http://www.read.rswzr.com/Article/383130.shtml
- http://www.read.rswzr.com/Article/46148.shtml
- http://www.read.rswzr.com/Article/707993.shtml
- http://www.read.rswzr.com/Article/440517.shtml
- http://www.read.rswzr.com/Article/7335433.shtml
- http://www.read.rswzr.com/Article/9061.shtml
- http://www.read.rswzr.com/Article/5164.shtml
- http://www.read.rswzr.com/Article/37300.shtml
- http://www.read.rswzr.com/Article/8778.shtml
- http://www.read.rswzr.com/Article/547537.shtml
- http://www.read.rswzr.com/Article/3769086.shtml
- http://www.read.rswzr.com/Article/683247.shtml
- http://www.read.rswzr.com/Article/9229.shtml
- http://www.read.rswzr.com/Article/0808.shtml
- http://www.read.rswzr.com/Article/6869993.shtml
- http://www.read.rswzr.com/Article/3791.shtml
- http://www.read.rswzr.com/Article/30304.shtml
- http://www.read.rswzr.com/Article/34729.shtml
- http://www.read.rswzr.com/Article/46749.shtml
- http://www.read.rswzr.com/Article/00817.shtml
- http://www.read.rswzr.com/Article/2220.shtml
- http://www.read.rswzr.com/Article/089342.shtml
- http://www.read.rswzr.com/Article/6411309.shtml
- http://www.read.rswzr.com/Article/44174.shtml
- http://www.read.rswzr.com/Article/45759.shtml
- http://www.read.rswzr.com/Article/197925.shtml
- http://www.read.rswzr.com/Article/64714.shtml
- http://www.read.rswzr.com/Article/58189.shtml
- http://www.read.rswzr.com/Article/6115.shtml
- http://www.read.rswzr.com/Article/9585626.shtml
- http://www.read.rswzr.com/Article/9293300.shtml
- http://www.read.rswzr.com/Article/763312.shtml
- http://www.read.rswzr.com/Article/6557.shtml
- http://www.read.rswzr.com/Article/192142.shtml
- http://www.read.rswzr.com/Article/5317.shtml
- http://www.read.rswzr.com/Article/3879642.shtml
- http://www.read.rswzr.com/Article/6383.shtml
- http://www.read.rswzr.com/Article/7274.shtml
- http://www.read.rswzr.com/Article/2630700.shtml
- http://www.read.rswzr.com/Article/878993.shtml
- http://www.read.rswzr.com/Article/7816.shtml
- http://www.read.rswzr.com/Article/6500.shtml
- http://www.read.rswzr.com/Article/79096.shtml
- http://www.read.rswzr.com/Article/253063.shtml
- http://www.read.rswzr.com/Article/29894.shtml
- http://www.read.rswzr.com/Article/89514.shtml
- http://www.read.rswzr.com/Article/5569.shtml
- http://www.read.rswzr.com/Article/9444049.shtml
- http://www.read.rswzr.com/Article/7744.shtml
- http://www.read.rswzr.com/Article/92445.shtml
- http://www.read.rswzr.com/Article/27407.shtml
- http://www.read.rswzr.com/Article/2646.shtml
- http://www.read.rswzr.com/Article/151590.shtml
- http://www.read.rswzr.com/Article/1152684.shtml
- http://www.read.rswzr.com/Article/672225.shtml
- http://www.read.rswzr.com/Article/602978.shtml
- http://www.read.rswzr.com/Article/0362286.shtml
- http://www.read.rswzr.com/Article/905457.shtml
- http://www.read.rswzr.com/Article/14007.shtml

## 项目结构

```
registry/
├── app.py                     # Flask API 服务入口，注册路由与错误处理器
├── config.py                  # 环境变量读取与默认配置（端口、并发数、超时阈值）
├── requirements.txt           # Python 依赖清单，锁定版本范围
├── data/                      # 数据目录
│   ├── sample_urls.txt        # 示例链接集合，用于快速测试导入流程
│   └── archive/               # 历史快照归档，按 yyyy-mm-dd 命名存放 JSON 结果
├── scripts/                   # 可执行工具脚本目录
│   ├── init_db.py             # 初始化数据库表结构，创建 FTS5 虚拟表
│   ├── import_links.py        # 从文本文件逐行读取 URL 并写入数据库
│   ├── probe_links.py         # 异步状态探测主逻辑，支持断点续探
│   └── export_data.py         # 将数据库内容导出为多种格式（JSON/CSV/Markdown）
├── docs/                      # 项目文档目录
│   ├── quickstart.md          # 快速入门指南，含常见操作示例
│   ├── schema.md              # 完整数据模型定义与字段约束说明
│   ├── api_reference.md       # API 端点详细文档，包含请求/响应 JSON 结构
│   └── operations.md          # 运维指南，含日志轮转、性能调优建议
├── tests/                     # 单元测试与集成测试目录
│   ├── test_import.py         # 测试导入逻辑对异常 URL 的处理
│   └── test_probe.py          # 测试探针的超时重试与状态码解析
├── logs/                      # 运行时日志存储目录，按日切割
│   └── app.log                # 当前活跃日志文件，记录 API 请求与探针事件
└── .github/                   # GitHub 社区模板与 CI 配置
    └── ISSUE_TEMPLATE/        # 问题报告与功能请求模板
```

## 贡献指南

1. 复刻本仓库至个人账户，并在本地创建功能分支。分支命名建议采用 `feature/简述改动` 或 `fix/简述修复` 格式，避免直接在主分支上修改。

2. 安装开发依赖组，包括 pytest、black 与 flake8。执行 `pip install -r requirements-dev.txt` 完成安装，并运行 `pre-commit install` 启用提交前代码格式检查。

3. 若新增链接来源或修改探针逻辑，请同步更新 `data/sample_urls.txt` 中的示例数据，并在 `tests/` 下补充对应的单元测试用例，确保测试覆盖率达到 80% 以上。

4. 提交变更前，执行 `make test` 与 `make lint` 验证所有测试通过且无风格警告。提交信息采用英文，遵循 Conventional Commits 规范，例如 `feat: add retry mechanism for probe timeout`。

5. 发起 Pull Request 至主仓库的 `main` 分支，在描述中关联相关 Issue 编号，并简要说明改动动机与影响范围。核心维护者将在 3 个工作日内进行审核。

## 常见问题

**问：导入链接时提示 URL 格式无效，但链接在浏览器中可以正常打开。**
答：导入脚本默认要求每条 URL 包含协议头（http:// 或 https://）。请检查原始文本是否缺少协议前缀。若确认为有效链接，可使用 `--strict` 参数关闭格式校验，但需自行承担格式异常导致后续探针报错的风险。

**问：状态探测返回大量 403 或 429 状态码，如何降低被目标网站限制的频率？**
答：可在 config.py 中调低 `PROBE_CONCURRENCY` 参数（例如设置为 3）并增大 `PROBE_DELAY` 参数（单位秒），使请求间隔更加稀疏。对于特定域名，也可通过 `--exclude-domains` 参数暂时跳过探测。

**问：SQLite 数据库文件体积增长过快，如何压缩或清理历史快照？**
答：可运行 `scripts/export_data.py --prune --keep-days 30` 清理 30 天前的快照记录。若需彻底回收磁盘空间，请在停止 API 服务后执行 `vacuum` 命令，该操作会重建数据库文件并释放未使用的页面。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
