# LinkPlex 资源导航系统

LinkPlex 是一个面向技术社区的内容聚合与导航系统，旨在解决技术文档分散、优质外链难以追溯、知识碎片化的问题。本项目通过结构化的资源索引机制，将分散在互联网各处的技术文章、教程、案例和参考文档进行统一收录与分类管理，帮助开发者、研究人员和技术写作人员快速定位高价值外部资源。系统内置了批次化资源导入、分类标签自动推断和基础全文检索能力，适用于个人知识库构建、团队技术栈文档化以及开源项目外链资产管理等场景。LinkPlex 定位于轻量级、可扩展的资源网关层，不依赖重型数据库，采用文件系统加元数据索引的方式运行，可作为静态站点生成器的数据源，也可集成到现有文档平台中作为外链治理工具。

## 功能概览

批量资源导入 支持按批次（每批最多 250 个条目）从外部数据源导入 URL 列表，自动生成唯一标识符并记录导入时间戳。

元数据自动补全 根据 URL 路径特征和域名信息，自动推断资源类型（如教程、API 参考、案例研究等）并附加初步分类标签。

链接可达性巡检 内置轻量级链接状态检查器，可定时探测资源是否可访问，并标记失效链接以供人工复核。

全文检索接口 基于资源标题、摘要和标签构建简单的倒排索引，提供命令行和 HTTP 两种查询方式。

标签体系与筛选 支持自定义标签的增删改，可按单个标签或多个标签组合筛选资源列表，便于按主题浏览。

静态快照导出 可将当前索引数据导出为 JSON 或 YAML 格式，供静态站点生成器（如 Hugo、VuePress）直接消费。

冲突检测与去重 在导入新批次时自动检测与现有资源的 URL 重复，并提供覆盖或跳过的策略选项。

操作日志审计 记录所有资源变更操作（新增、更新、删除、标记失效），支持按时间范围和操作者追溯历史。

## 应用场景

个人技术博客外链治理 技术博主在撰写文章时，常需引用大量外部资料。LinkPlex 可作为本地外链仓库，统一管理所有引用链接，并在文章发布前自动检查链接有效性，避免读者遇到 404 页面。

团队内部技术文档中心 研发团队可将常用的官方文档、社区最佳实践、内部培训资料等链接集中录入 LinkPlex，按技术栈（如 Go、Rust、Kubernetes）打标签，新成员入职时可通过标签筛选快速了解团队所依赖的知识体系。

开源项目 README 与官网资源页管理 开源项目维护者可使用 LinkPlex 管理项目官网或 README 中陈列的社区资源列表。每次发布新版本时，通过批次导入功能更新资源清单，并导出为 Markdown 格式，自动同步到项目仓库。

技术培训课程资料包组织 培训机构或教育工作者可将课程涉及的延伸阅读链接按周次或模块导入系统，学员可通过标签筛选获取当周推荐阅读材料，同时系统可统计各链接的访问频次，辅助优化课程内容编排。

## 快速开始

以下命令演示了从克隆代码到启动服务的完整流程。

```bash
# 克隆代码仓库
git clone https://github.com/example/linkplex.git
cd linkplex

# 安装依赖（使用 pip 和虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化本地索引数据库（使用 SQLite）
python manage.py init --db-path ./data/linkplex.db

# 导入示例资源批次（包含 250 条测试链接）
python manage.py import --batch ./samples/batch_028.json

# 启动本地检索服务（默认监听 127.0.0.1:8000）
python manage.py serve --host 127.0.0.1 --port 8000
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，建议使用 3.11 长期支持版本 |
| SQLite | 3.35 及以上 | 嵌入式数据库，用于存储索引元数据，无需额外安装 |
| requests | 2.28.0 及以上 | 用于链接可达性检查和外部资源元数据抓取 |
| click | 8.1.0 及以上 | 命令行交互界面框架，用于子命令解析 |
| PyYAML | 6.0 及以上 | 用于导出快照为 YAML 格式，便于静态站点集成 |
| markdownify | 0.11.6 及以上 | 可选组件，用于将 HTML 摘要转换为 Markdown 纯文本 |
| pytest | 7.2.0 及以上 | 开发测试依赖，仅运行单元测试时需安装 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user/quickstart.md | 如何安装、配置、启动系统以及执行基本导入导出操作 |
| 用户手册 | docs/user/batch-management.md | 如何管理资源批次、查看批次状态、删除或回滚批次 |
| 开发指南 | docs/dev/architecture.md | 系统整体模块划分、数据流向、扩展点设计说明 |
| 开发指南 | docs/dev/api-reference.md | HTTP 接口的请求与响应格式、状态码含义、鉴权方式 |
| 运维手册 | docs/ops/deployment.md | 生产环境部署建议（反向代理、进程守护、定期巡检配置） |
| 运维手册 | docs/ops/troubleshooting.md | 常见错误码排查、日志分析、性能调优参数 |

## 资源列表

- http://www.read.xwpxi.com/Article/1028388.shtml
- http://www.read.xwpxi.com/Article/0295184.shtml
- http://www.read.xwpxi.com/Article/9972.shtml
- http://www.read.xwpxi.com/Article/3675550.shtml
- http://www.read.xwpxi.com/Article/92822.shtml
- http://www.read.xwpxi.com/Article/6426.shtml
- http://www.read.xwpxi.com/Article/04009.shtml
- http://www.read.xwpxi.com/Article/2162496.shtml
- http://www.read.xwpxi.com/Article/13111.shtml
- http://www.read.xwpxi.com/Article/4357130.shtml
- http://www.read.xwpxi.com/Article/2997.shtml
- http://www.read.xwpxi.com/Article/7165340.shtml
- http://www.read.xwpxi.com/Article/200487.shtml
- http://www.read.xwpxi.com/Article/26786.shtml
- http://www.read.xwpxi.com/Article/6413556.shtml
- http://www.read.xwpxi.com/Article/65160.shtml
- http://www.read.xwpxi.com/Article/74007.shtml
- http://www.read.xwpxi.com/Article/4003.shtml
- http://www.read.xwpxi.com/Article/4125.shtml
- http://www.read.xwpxi.com/Article/5984.shtml
- http://www.read.xwpxi.com/Article/99353.shtml
- http://www.read.xwpxi.com/Article/493951.shtml
- http://www.read.xwpxi.com/Article/38606.shtml
- http://www.read.xwpxi.com/Article/6079374.shtml
- http://www.read.xwpxi.com/Article/99771.shtml
- http://www.read.xwpxi.com/Article/043736.shtml
- http://www.read.xwpxi.com/Article/05756.shtml
- http://www.read.xwpxi.com/Article/54361.shtml
- http://www.read.xwpxi.com/Article/08081.shtml
- http://www.read.xwpxi.com/Article/214589.shtml
- http://www.read.xwpxi.com/Article/237963.shtml
- http://www.read.xwpxi.com/Article/4643684.shtml
- http://www.read.xwpxi.com/Article/620832.shtml
- http://www.read.xwpxi.com/Article/747022.shtml
- http://www.read.xwpxi.com/Article/561028.shtml
- http://www.read.xwpxi.com/Article/738964.shtml
- http://www.read.xwpxi.com/Article/09018.shtml
- http://www.read.xwpxi.com/Article/32112.shtml
- http://www.read.xwpxi.com/Article/982860.shtml
- http://www.read.xwpxi.com/Article/27763.shtml
- http://www.read.xwpxi.com/Article/238397.shtml
- http://www.read.xwpxi.com/Article/8931.shtml
- http://www.read.xwpxi.com/Article/8095.shtml
- http://www.read.xwpxi.com/Article/6400025.shtml
- http://www.read.xwpxi.com/Article/824423.shtml
- http://www.read.xwpxi.com/Article/24151.shtml
- http://www.read.xwpxi.com/Article/194251.shtml
- http://www.read.xwpxi.com/Article/989901.shtml
- http://www.read.xwpxi.com/Article/785960.shtml
- http://www.read.xwpxi.com/Article/576061.shtml
- http://www.read.xwpxi.com/Article/288413.shtml
- http://www.read.xwpxi.com/Article/185037.shtml
- http://www.read.xwpxi.com/Article/5859331.shtml
- http://www.read.xwpxi.com/Article/7970.shtml
- http://www.read.xwpxi.com/Article/9361.shtml
- http://www.read.xwpxi.com/Article/52869.shtml
- http://www.read.xwpxi.com/Article/7980704.shtml
- http://www.read.xwpxi.com/Article/5565499.shtml
- http://www.read.xwpxi.com/Article/17813.shtml
- http://www.read.xwpxi.com/Article/0230772.shtml
- http://www.read.xwpxi.com/Article/67139.shtml
- http://www.read.xwpxi.com/Article/98073.shtml
- http://www.read.xwpxi.com/Article/569512.shtml
- http://www.read.xwpxi.com/Article/23839.shtml
- http://www.read.xwpxi.com/Article/2816952.shtml
- http://www.read.xwpxi.com/Article/624665.shtml
- http://www.read.xwpxi.com/Article/1619.shtml
- http://www.read.xwpxi.com/Article/359006.shtml
- http://www.read.xwpxi.com/Article/482494.shtml
- http://www.read.xwpxi.com/Article/080878.shtml
- http://www.read.xwpxi.com/Article/7522.shtml
- http://www.read.xwpxi.com/Article/33578.shtml
- http://www.read.xwpxi.com/Article/52863.shtml
- http://www.read.xwpxi.com/Article/8842.shtml
- http://www.read.xwpxi.com/Article/275858.shtml
- http://www.read.xwpxi.com/Article/1920.shtml
- http://www.read.xwpxi.com/Article/9430.shtml
- http://www.read.xwpxi.com/Article/92031.shtml
- http://www.read.xwpxi.com/Article/0234653.shtml
- http://www.read.xwpxi.com/Article/12239.shtml
- http://www.read.xwpxi.com/Article/2969.shtml
- http://www.read.xwpxi.com/Article/8415082.shtml
- http://www.read.xwpxi.com/Article/420039.shtml
- http://www.read.xwpxi.com/Article/40694.shtml
- http://www.read.xwpxi.com/Article/8933.shtml
- http://www.read.xwpxi.com/Article/102961.shtml
- http://www.read.xwpxi.com/Article/7551.shtml
- http://www.read.xwpxi.com/Article/55869.shtml
- http://www.read.xwpxi.com/Article/3476.shtml
- http://www.read.xwpxi.com/Article/0965.shtml
- http://www.read.xwpxi.com/Article/355194.shtml
- http://www.read.xwpxi.com/Article/06843.shtml
- http://www.read.xwpxi.com/Article/6780236.shtml
- http://www.read.xwpxi.com/Article/6503.shtml
- http://www.read.xwpxi.com/Article/694139.shtml
- http://www.read.xwpxi.com/Article/289010.shtml
- http://www.read.xwpxi.com/Article/77616.shtml
- http://www.read.xwpxi.com/Article/351283.shtml
- http://www.read.xwpxi.com/Article/2885.shtml
- http://www.read.xwpxi.com/Article/24340.shtml
- http://www.read.xwpxi.com/Article/66542.shtml
- http://www.read.xwpxi.com/Article/08808.shtml
- http://www.read.xwpxi.com/Article/053567.shtml
- http://www.read.xwpxi.com/Article/865017.shtml
- http://www.read.xwpxi.com/Article/0340.shtml
- http://www.read.xwpxi.com/Article/4455170.shtml
- http://www.read.xwpxi.com/Article/8906.shtml
- http://www.read.xwpxi.com/Article/8788.shtml
- http://www.read.xwpxi.com/Article/1623.shtml
- http://www.read.xwpxi.com/Article/4385.shtml
- http://www.read.xwpxi.com/Article/69727.shtml
- http://www.read.xwpxi.com/Article/18512.shtml
- http://www.read.xwpxi.com/Article/66379.shtml
- http://www.read.xwpxi.com/Article/77056.shtml
- http://www.read.xwpxi.com/Article/078901.shtml
- http://www.read.xwpxi.com/Article/20364.shtml
- http://www.read.xwpxi.com/Article/6885501.shtml
- http://www.read.xwpxi.com/Article/24923.shtml
- http://www.read.xwpxi.com/Article/2572.shtml
- http://www.read.xwpxi.com/Article/7573.shtml
- http://www.read.xwpxi.com/Article/593817.shtml
- http://www.read.xwpxi.com/Article/857178.shtml
- http://www.read.xwpxi.com/Article/853917.shtml
- http://www.read.xwpxi.com/Article/6307941.shtml
- http://www.read.xwpxi.com/Article/70367.shtml
- http://www.read.xwpxi.com/Article/4422064.shtml
- http://www.read.xwpxi.com/Article/1462000.shtml
- http://www.read.xwpxi.com/Article/1609.shtml
- http://www.read.xwpxi.com/Article/904464.shtml
- http://www.read.xwpxi.com/Article/17904.shtml
- http://www.read.xwpxi.com/Article/3760.shtml
- http://www.read.xwpxi.com/Article/86035.shtml
- http://www.read.xwpxi.com/Article/8791289.shtml
- http://www.read.xwpxi.com/Article/1912834.shtml
- http://www.read.xwpxi.com/Article/6591948.shtml
- http://www.read.xwpxi.com/Article/1384466.shtml
- http://www.read.xwpxi.com/Article/214542.shtml
- http://www.read.xwpxi.com/Article/39421.shtml
- http://www.read.xwpxi.com/Article/1936866.shtml
- http://www.read.xwpxi.com/Article/939513.shtml
- http://www.read.xwpxi.com/Article/02422.shtml
- http://www.read.xwpxi.com/Article/204572.shtml
- http://www.read.xwpxi.com/Article/733074.shtml
- http://www.read.xwpxi.com/Article/782226.shtml
- http://www.read.xwpxi.com/Article/664521.shtml
- http://www.read.xwpxi.com/Article/9580456.shtml
- http://www.read.xwpxi.com/Article/4550175.shtml
- http://www.read.xwpxi.com/Article/002970.shtml
- http://www.read.xwpxi.com/Article/9212561.shtml
- http://www.read.xwpxi.com/Article/5785.shtml
- http://www.read.xwpxi.com/Article/464732.shtml
- http://www.read.xwpxi.com/Article/68964.shtml
- http://www.read.xwpxi.com/Article/48210.shtml
- http://www.read.xwpxi.com/Article/6851869.shtml
- http://www.read.xwpxi.com/Article/0794.shtml
- http://www.read.xwpxi.com/Article/05421.shtml
- http://www.read.xwpxi.com/Article/821376.shtml
- http://www.read.xwpxi.com/Article/0373.shtml
- http://www.read.xwpxi.com/Article/6598997.shtml
- http://www.read.xwpxi.com/Article/029278.shtml
- http://www.read.xwpxi.com/Article/17753.shtml
- http://www.read.xwpxi.com/Article/96051.shtml
- http://www.read.xwpxi.com/Article/87720.shtml
- http://www.read.xwpxi.com/Article/84943.shtml
- http://www.read.xwpxi.com/Article/3686780.shtml
- http://www.read.xwpxi.com/Article/6734.shtml
- http://www.read.xwpxi.com/Article/1050.shtml
- http://www.read.xwpxi.com/Article/5157940.shtml
- http://www.read.xwpxi.com/Article/0180.shtml
- http://www.read.xwpxi.com/Article/4682.shtml
- http://www.read.xwpxi.com/Article/1731565.shtml
- http://www.read.xwpxi.com/Article/4120.shtml
- http://www.read.xwpxi.com/Article/052611.shtml
- http://www.read.xwpxi.com/Article/69657.shtml
- http://www.read.xwpxi.com/Article/328817.shtml
- http://www.read.xwpxi.com/Article/8124546.shtml
- http://www.read.xwpxi.com/Article/886024.shtml
- http://www.read.xwpxi.com/Article/7184327.shtml
- http://www.read.xwpxi.com/Article/8455.shtml
- http://www.read.xwpxi.com/Article/1347.shtml
- http://www.read.xwpxi.com/Article/9940669.shtml
- http://www.read.xwpxi.com/Article/80807.shtml
- http://www.read.xwpxi.com/Article/816124.shtml
- http://www.read.xwpxi.com/Article/1163.shtml
- http://www.read.xwpxi.com/Article/0101630.shtml
- http://www.read.xwpxi.com/Article/7142268.shtml
- http://www.read.xwpxi.com/Article/25551.shtml
- http://www.read.xwpxi.com/Article/67705.shtml
- http://www.read.xwpxi.com/Article/6720.shtml
- http://www.read.xwpxi.com/Article/427059.shtml
- http://www.read.xwpxi.com/Article/4880.shtml
- http://www.read.xwpxi.com/Article/01048.shtml
- http://www.read.xwpxi.com/Article/99559.shtml
- http://www.read.xwpxi.com/Article/45249.shtml
- http://www.read.xwpxi.com/Article/2150062.shtml
- http://www.read.xwpxi.com/Article/022767.shtml
- http://www.read.xwpxi.com/Article/5626730.shtml
- http://www.read.xwpxi.com/Article/203860.shtml
- http://www.read.xwpxi.com/Article/893520.shtml
- http://www.read.xwpxi.com/Article/860637.shtml
- http://www.read.xwpxi.com/Article/52410.shtml
- http://www.read.xwpxi.com/Article/54349.shtml
- http://www.read.xwpxi.com/Article/337141.shtml
- http://www.read.xwpxi.com/Article/7570247.shtml
- http://www.read.xwpxi.com/Article/089504.shtml
- http://www.read.xwpxi.com/Article/3491.shtml
- http://www.read.xwpxi.com/Article/5927.shtml
- http://www.read.xwpxi.com/Article/3087680.shtml
- http://www.read.xwpxi.com/Article/130438.shtml
- http://www.read.xwpxi.com/Article/1835.shtml
- http://www.read.xwpxi.com/Article/94269.shtml
- http://www.read.xwpxi.com/Article/61651.shtml
- http://www.read.xwpxi.com/Article/09882.shtml
- http://www.read.xwpxi.com/Article/6629077.shtml
- http://www.read.xwpxi.com/Article/9918.shtml
- http://www.read.xwpxi.com/Article/988392.shtml
- http://www.read.xwpxi.com/Article/0838.shtml
- http://www.read.xwpxi.com/Article/350482.shtml
- http://www.read.xwpxi.com/Article/5915258.shtml
- http://www.read.xwpxi.com/Article/8596.shtml
- http://www.read.xwpxi.com/Article/302309.shtml
- http://www.read.xwpxi.com/Article/395564.shtml
- http://www.read.xwpxi.com/Article/1259767.shtml
- http://www.read.xwpxi.com/Article/3012687.shtml
- http://www.read.xwpxi.com/Article/03212.shtml
- http://www.read.xwpxi.com/Article/82834.shtml
- http://www.read.xwpxi.com/Article/4068.shtml
- http://www.read.xwpxi.com/Article/172652.shtml
- http://www.read.xwpxi.com/Article/4320752.shtml
- http://www.read.xwpxi.com/Article/7835.shtml
- http://www.read.xwpxi.com/Article/2719.shtml
- http://www.read.xwpxi.com/Article/0136.shtml
- http://www.read.xwpxi.com/Article/006891.shtml
- http://www.read.xwpxi.com/Article/9307.shtml
- http://www.read.xwpxi.com/Article/42669.shtml
- http://www.read.xwpxi.com/Article/1556437.shtml
- http://www.read.xwpxi.com/Article/89250.shtml
- http://www.read.xwpxi.com/Article/673052.shtml
- http://www.read.xwpxi.com/Article/413652.shtml
- http://www.read.xwpxi.com/Article/8263.shtml
- http://www.read.xwpxi.com/Article/045667.shtml
- http://www.read.xwpxi.com/Article/074465.shtml
- http://www.read.xwpxi.com/Article/9445812.shtml
- http://www.read.xwpxi.com/Article/2536481.shtml
- http://www.read.xwpxi.com/Article/70689.shtml
- http://www.read.xwpxi.com/Article/74587.shtml
- http://www.read.xwpxi.com/Article/302490.shtml
- http://www.read.xwpxi.com/Article/5585479.shtml
- http://www.read.xwpxi.com/Article/592073.shtml
- http://www.read.xwpxi.com/Article/4409.shtml

## 项目结构

```
linkplex/
├── cmd/                                 # 命令行入口层
│   ├── main.go                          # 主程序入口，解析全局参数并调用子命令
│   └── commands/                        # 各子命令实现
│       ├── import.go                    # import 子命令：解析批次文件并写入索引
│       ├── serve.go                     # serve 子命令：启动 HTTP 服务
│       ├── init.go                      # init 子命令：初始化数据库与配置目录
│       └── check.go                     # check 子命令：触发链接可达性巡检
├── internal/                            # 内部核心包，不对外暴露
│   ├── indexer/                         # 索引引擎模块
│   │   ├── sqlite.go                    # SQLite 存储层实现，含表结构迁移
│   │   └── batch.go                     # 批次解析与去重逻辑
│   ├── checker/                         # 链接巡检模块
│   │   ├── http.go                      # HTTP 客户端封装，含超时与重试策略
│   │   └── scheduler.go                 # 定时任务调度器
│   ├── api/                             # HTTP API 处理模块
│   │   ├── handlers.go                  # 路由处理器：查询、导入、状态
│   │   └── middleware.go                # 日志、跨域、限流中间件
│   ├── tags/                            # 标签管理模块
│   │   ├── classifier.go                # 基于正则和域名的自动标签推断
│   │   └── store.go                     # 标签与资源的关联关系操作
│   └── exporter/                        # 快照导出模块
│       ├── json.go                      # JSON 格式序列化器
│       └── yaml.go                      # YAML 格式序列化器
├── pkg/                                 # 可复用公共库
│   ├── logger/                          # 统一日志接口，支持 JSON 和文本格式
│   └── config/                          # 配置文件解析（支持 .env 和 .yaml）
├── data/                                # 运行时数据目录（默认）
│   ├── linkplex.db                      # SQLite 主数据库文件
│   └── logs/                            # 应用日志存储目录
├── samples/                             # 示例数据与批次模板
│   ├── batch_028.json                   # 第 28 批资源示例（含 250 条 URL）
│   └── schema.json                      # 批次导入的 JSON Schema 校验文件
├── docs/                                # 文档目录
│   ├── user/                            # 用户文档（快速开始、批量管理）
│   ├── dev/                             # 开发者文档（架构、API 参考）
│   └── ops/                             # 运维文档（部署、排障）
├── scripts/                             # 辅助脚本
│   ├── migrate_db.sh                    # 数据库版本升级脚本
│   └── gen_sample_batch.py              # 用于生成示例批次数据的 Python 脚本
├── go.mod                               # Go 模块定义文件
├── go.sum                               # 依赖校验文件
├── Makefile                             # 构建与测试任务快捷命令
└── README.md                            # 项目入口文档（即本文档）
```

## 贡献指南

1. 查阅问题追踪器 访问 GitHub Issues 页面，查找未被认领的 bug 或功能请求。建议优先选择标记为 "good first issue" 的条目作为初次贡献切入点。

2. 派生仓库并创建功能分支 将主仓库派生至个人账户下，然后克隆派生仓库至本地。新建分支时请遵循命名规范，例如 feat/improve-batch-parser 或 fix/sqlite-connection-leak。

3. 遵循代码风格与测试规范 所有 Go 代码必须通过 gofmt 和 go vet 检查。新增功能或修复缺陷时，需在对应的 test 文件下补充单元测试或集成测试用例，确保测试覆盖率达到 80% 以上。

4. 提交变更并编写清晰 commit 信息 提交消息应采用前缀加主题的格式，例如 "indexer: add retry logic for batch insert" 或 "api: fix response status code for duplicate URL"。正文中应简述变更原因和影响范围。

5. 发起拉取请求 推送分支至派生仓库后，在主仓库的 Pull Request 页面创建新请求。请求描述中请关联相关 issue 编号，并勾选自检清单（如是否已运行全部测试、是否更新了对应文档）。

## 常见问题

Q: 导入批次时提示 URL 重复，我应该选择覆盖还是跳过？
A: 系统检测到重复 URL 时会给出交互选项。如果您希望更新已有资源的元数据（如标签或备注），可选择覆盖；若您保留首次导入的版本，请选择跳过。对于维护历史记录的场景，建议优先跳过并人工核对重复条目，避免意外覆盖有效信息。

Q: 如何自定义链接可达性巡检的时间间隔和超时阈值？
A: 您可以在 data/config.yaml 文件中修改 checker 章节的参数。interval_minutes 控制巡检周期（默认 1440 分钟，即每日一次），timeout_seconds 控制单次请求超时时间（默认 10 秒）。修改后需重启 serve 进程使配置生效。

Q: 能否将 LinkPlex 与现有的静态站点生成器（如 Docusaurus）集成？
A: 可以。系统提供了 export 子命令，可将当前索引数据导出为 JSON 或 YAML 格式的静态文件。您可以在站点构建流程中添加一个前置步骤，调用 export 命令生成数据文件，然后在站点模板中读取该文件并渲染资源列表。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
