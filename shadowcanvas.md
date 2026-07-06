# LinkMaster

LinkMaster 是一个轻量级的技术资源外链聚合与导航系统，专为开发者、技术内容创作者以及研究团队设计，用于集中管理、分类展示和快速检索分散于互联网各处的优质技术文章、教程、文档与工具站点。该项目不存储任何实体内容，仅作为结构化索引层，通过可配置的抓取与解析规则，将用户提供的海量链接转化为具备分类、标签、快照摘要与有效性检测的本地知识库导航。

LinkMaster 面向需要频繁查阅外部技术资料但厌倦了零散书签管理的用户。它解决了传统浏览器书签无法批量校验死链、无法进行全文检索、缺乏上下文摘要以及难以团队共享的问题。通过本项目，运维人员可快速搭建一套只读的、对搜索引擎友好的导航门户，开发者可基于其提供的 JSON API 将外链资源集成到 CI/CD 文档站点或内部知识管理系统中。

## 功能概览

- 批量外链导入与自动去重：支持从纯文本列表、CSV 及浏览器书签导出文件批量导入 URL，自动识别并剔除重复条目，保留最新添加时间戳。
- 智能链接可用性巡检：内置异步任务队列，定期对已收录链接发起 HEAD 请求，检测 HTTP 状态码变化，标记失效链接并记录重定向后的最终地址。
- 自定义元数据增强提取：针对特定域名配置 CSS 选择器或 XPath 规则，自动抓取目标页面的标题、发布时间、作者及正文前 200 字符作为本地索引摘要。
- 多级分类与标签体系管理：提供无限层级的分类目录与扁平化标签系统，支持一个资源关联多个分类和标签，便于构建多维导航视图。
- 全文检索引擎：基于倒排索引实现对已收录链接标题、摘要、自定义备注的快速中文分词搜索，支持布尔运算符与短语精确匹配。
- 只读 RESTful API 输出：所有导航数据均可通过 JSON 格式接口对外输出，方便集成至静态站点生成器、文档工具或自定义前端界面。
- 数据快照导入导出：支持将整个索引数据库导出为单一 JSON 或 SQLite 文件，便于迁移、备份或离线分析。

## 应用场景

企业内部技术文档中心导航
企业技术文档团队可利用 LinkMaster 汇总分散在各个团队 Wiki、外部技术博客、官方 SDK 文档页面的链接，通过统一的分类与标签体系构建内部导航门户，新入职员工可借此快速熟悉公司技术栈涉及的关键外部资源。

个人开发者知识库构建
独立开发者或技术爱好者可使用 LinkMaster 整理长期积累的技术书签，通过定时巡检功能清理失效链接，并利用全文检索功能在数百上千个资源中快速定位特定关键词的相关文章，避免重复搜索。

技术内容运营与编辑后台
技术媒体编辑或开源社区运营人员可将 LinkMaster 作为内容素材库的后台，通过标签关联热点技术趋势，快速检索过往报道过的主题，辅助选题策划与内容引用溯源。

离线文档站点镜像辅助
在受网络限制的开发环境中，运维人员可先在外网使用 LinkMaster 整理所需外链清单，导出为结构化数据后，配合离线下载工具批量获取页面存档，实现受限网络下的知识迁移。

## 快速开始

以下命令演示了如何在 Linux 或 macOS 环境下从源码启动 LinkMaster 服务。

```bash
# 克隆项目仓库至本地
git clone https://github.com/linkmaster/linkmaster-core.git

# 进入项目工作目录
cd linkmaster-core

# 安装项目依赖（基于 Python 3.10+ 与 Poetry 管理）
poetry install

# 复制环境变量模板并进行必要配置（如数据库连接、巡检间隔）
cp .env.example .env

# 执行数据库迁移初始化
poetry run python manage.py migrate

# 启动开发调试服务器，默认监听 127.0.0.1:8000
poetry run python manage.py runserver
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 至 3.12 | 项目核心运行环境，低于 3.10 会导致类型注解语法错误 |
| Poetry | 1.4.0 及以上 | 用于依赖包管理与虚拟环境隔离，非必需但强烈推荐 |
| SQLite | 3.35.0 及以上 | 默认嵌入式数据库，支持 JSON 字段存储与全文搜索扩展 |
| Redis | 7.0 及以上 | 用于缓存调度任务状态与分布式锁，单机模式也可运行 |
| Node.js | 18.0 及以上 | 仅当启用前端仪表盘构建时所需，后端可独立运行 |
| Nginx | 1.20 及以上 | 生产环境反向代理与静态资源服务推荐使用，非强制 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user/quick-start.md | 如何快速运行实例、配置第一个数据源并浏览导航页面 |
| 管理员指南 | /docs/admin/scheduler-config.md | 如何调整巡检频率、配置通知回调以及管理任务队列 |
| 开发者文档 | /docs/developer/api-reference.md | 各 RESTful 端点的请求参数、响应结构及鉴权方式说明 |
| 部署运维 | /docs/ops/deployment-checklist.md | 生产环境部署前的安全检查、性能调优与日志采集配置 |

## 资源列表

- http://www.read.xwpxi.com/Article/138326.shtml
- http://www.read.xwpxi.com/Article/298246.shtml
- http://www.read.xwpxi.com/Article/190041.shtml
- http://www.read.xwpxi.com/Article/24265.shtml
- http://www.read.xwpxi.com/Article/6751806.shtml
- http://www.read.xwpxi.com/Article/1121259.shtml
- http://www.read.xwpxi.com/Article/357274.shtml
- http://www.read.xwpxi.com/Article/83796.shtml
- http://www.read.xwpxi.com/Article/533942.shtml
- http://www.read.xwpxi.com/Article/2058444.shtml
- http://www.read.xwpxi.com/Article/1279.shtml
- http://www.read.xwpxi.com/Article/4830289.shtml
- http://www.read.xwpxi.com/Article/93153.shtml
- http://www.read.xwpxi.com/Article/2221288.shtml
- http://www.read.xwpxi.com/Article/3815000.shtml
- http://www.read.xwpxi.com/Article/572684.shtml
- http://www.read.xwpxi.com/Article/9759717.shtml
- http://www.read.xwpxi.com/Article/7433.shtml
- http://www.read.xwpxi.com/Article/47889.shtml
- http://www.read.xwpxi.com/Article/974698.shtml
- http://www.read.xwpxi.com/Article/2810.shtml
- http://www.read.xwpxi.com/Article/2732217.shtml
- http://www.read.xwpxi.com/Article/1716768.shtml
- http://www.read.xwpxi.com/Article/5885.shtml
- http://www.read.xwpxi.com/Article/087433.shtml
- http://www.read.xwpxi.com/Article/9379724.shtml
- http://www.read.xwpxi.com/Article/71136.shtml
- http://www.read.xwpxi.com/Article/9008.shtml
- http://www.read.xwpxi.com/Article/5715.shtml
- http://www.read.xwpxi.com/Article/32740.shtml
- http://www.read.xwpxi.com/Article/5811542.shtml
- http://www.read.xwpxi.com/Article/59402.shtml
- http://www.read.xwpxi.com/Article/7366692.shtml
- http://www.read.xwpxi.com/Article/3437007.shtml
- http://www.read.xwpxi.com/Article/3970.shtml
- http://www.read.xwpxi.com/Article/67027.shtml
- http://www.read.xwpxi.com/Article/6222790.shtml
- http://www.read.xwpxi.com/Article/3132.shtml
- http://www.read.xwpxi.com/Article/328988.shtml
- http://www.read.xwpxi.com/Article/4908.shtml
- http://www.read.xwpxi.com/Article/340757.shtml
- http://www.read.xwpxi.com/Article/850727.shtml
- http://www.read.xwpxi.com/Article/9229831.shtml
- http://www.read.xwpxi.com/Article/1269172.shtml
- http://www.read.xwpxi.com/Article/69213.shtml
- http://www.read.xwpxi.com/Article/7902.shtml
- http://www.read.xwpxi.com/Article/843382.shtml
- http://www.read.xwpxi.com/Article/77463.shtml
- http://www.read.xwpxi.com/Article/2826383.shtml
- http://www.read.xwpxi.com/Article/33240.shtml
- http://www.read.xwpxi.com/Article/149542.shtml
- http://www.read.xwpxi.com/Article/978510.shtml
- http://www.read.xwpxi.com/Article/4283587.shtml
- http://www.read.xwpxi.com/Article/032976.shtml
- http://www.read.xwpxi.com/Article/142499.shtml
- http://www.read.xwpxi.com/Article/4358.shtml
- http://www.read.xwpxi.com/Article/050127.shtml
- http://www.read.xwpxi.com/Article/0700483.shtml
- http://www.read.xwpxi.com/Article/6492.shtml
- http://www.read.xwpxi.com/Article/4692.shtml
- http://www.read.xwpxi.com/Article/36369.shtml
- http://www.read.xwpxi.com/Article/2010.shtml
- http://www.read.xwpxi.com/Article/1362019.shtml
- http://www.read.xwpxi.com/Article/416218.shtml
- http://www.read.xwpxi.com/Article/7934.shtml
- http://www.read.xwpxi.com/Article/55134.shtml
- http://www.read.xwpxi.com/Article/66529.shtml
- http://www.read.xwpxi.com/Article/5236449.shtml
- http://www.read.xwpxi.com/Article/285941.shtml
- http://www.read.xwpxi.com/Article/104626.shtml
- http://www.read.xwpxi.com/Article/513584.shtml
- http://www.read.xwpxi.com/Article/69280.shtml
- http://www.read.xwpxi.com/Article/9433.shtml
- http://www.read.xwpxi.com/Article/37618.shtml
- http://www.read.xwpxi.com/Article/4042952.shtml
- http://www.read.xwpxi.com/Article/3286.shtml
- http://www.read.xwpxi.com/Article/831693.shtml
- http://www.read.xwpxi.com/Article/21090.shtml
- http://www.read.xwpxi.com/Article/80190.shtml
- http://www.read.xwpxi.com/Article/4730476.shtml
- http://www.read.xwpxi.com/Article/36707.shtml
- http://www.read.xwpxi.com/Article/709026.shtml
- http://www.read.xwpxi.com/Article/9775.shtml
- http://www.read.xwpxi.com/Article/79642.shtml
- http://www.read.xwpxi.com/Article/845007.shtml
- http://www.read.xwpxi.com/Article/7379.shtml
- http://www.read.xwpxi.com/Article/431591.shtml
- http://www.read.xwpxi.com/Article/023838.shtml
- http://www.read.xwpxi.com/Article/2308876.shtml
- http://www.read.xwpxi.com/Article/688947.shtml
- http://www.read.xwpxi.com/Article/8181.shtml
- http://www.read.xwpxi.com/Article/481958.shtml
- http://www.read.xwpxi.com/Article/62475.shtml
- http://www.read.xwpxi.com/Article/8907823.shtml
- http://www.read.xwpxi.com/Article/309455.shtml
- http://www.read.xwpxi.com/Article/985743.shtml
- http://www.read.xwpxi.com/Article/640343.shtml
- http://www.read.xwpxi.com/Article/79904.shtml
- http://www.read.xwpxi.com/Article/81517.shtml
- http://www.read.xwpxi.com/Article/272791.shtml
- http://www.read.xwpxi.com/Article/8429.shtml
- http://www.read.xwpxi.com/Article/69173.shtml
- http://www.read.xwpxi.com/Article/3900.shtml
- http://www.read.xwpxi.com/Article/6520666.shtml
- http://www.read.xwpxi.com/Article/5348143.shtml
- http://www.read.xwpxi.com/Article/7224698.shtml
- http://www.read.xwpxi.com/Article/70748.shtml
- http://www.read.xwpxi.com/Article/891986.shtml
- http://www.read.xwpxi.com/Article/4118.shtml
- http://www.read.xwpxi.com/Article/9849.shtml
- http://www.read.xwpxi.com/Article/0565.shtml
- http://www.read.xwpxi.com/Article/54466.shtml
- http://www.read.xwpxi.com/Article/012333.shtml
- http://www.read.xwpxi.com/Article/748251.shtml
- http://www.read.xwpxi.com/Article/69351.shtml
- http://www.read.xwpxi.com/Article/2759151.shtml
- http://www.read.xwpxi.com/Article/422704.shtml
- http://www.read.xwpxi.com/Article/08247.shtml
- http://www.read.xwpxi.com/Article/0112843.shtml
- http://www.read.xwpxi.com/Article/8932.shtml
- http://www.read.xwpxi.com/Article/762524.shtml
- http://www.read.xwpxi.com/Article/562935.shtml
- http://www.read.xwpxi.com/Article/579507.shtml
- http://www.read.xwpxi.com/Article/2618355.shtml
- http://www.read.xwpxi.com/Article/835851.shtml
- http://www.read.xwpxi.com/Article/8532406.shtml
- http://www.read.xwpxi.com/Article/989029.shtml
- http://www.read.xwpxi.com/Article/0628375.shtml
- http://www.read.xwpxi.com/Article/6708910.shtml
- http://www.read.xwpxi.com/Article/9147644.shtml
- http://www.read.xwpxi.com/Article/04085.shtml
- http://www.read.xwpxi.com/Article/6673.shtml
- http://www.read.xwpxi.com/Article/9159.shtml
- http://www.read.xwpxi.com/Article/328369.shtml
- http://www.read.xwpxi.com/Article/638463.shtml
- http://www.read.xwpxi.com/Article/4782847.shtml
- http://www.read.xwpxi.com/Article/762430.shtml
- http://www.read.xwpxi.com/Article/8815.shtml
- http://www.read.xwpxi.com/Article/1759717.shtml
- http://www.read.xwpxi.com/Article/78085.shtml
- http://www.read.xwpxi.com/Article/357188.shtml
- http://www.read.xwpxi.com/Article/7194.shtml
- http://www.read.xwpxi.com/Article/52601.shtml
- http://www.read.xwpxi.com/Article/13942.shtml
- http://www.read.xwpxi.com/Article/075061.shtml
- http://www.read.xwpxi.com/Article/15955.shtml
- http://www.read.xwpxi.com/Article/9297.shtml
- http://www.read.xwpxi.com/Article/878228.shtml
- http://www.read.xwpxi.com/Article/5391.shtml
- http://www.read.xwpxi.com/Article/8247281.shtml
- http://www.read.xwpxi.com/Article/7558.shtml
- http://www.read.xwpxi.com/Article/67878.shtml
- http://www.read.xwpxi.com/Article/042858.shtml
- http://www.read.xwpxi.com/Article/798552.shtml
- http://www.read.xwpxi.com/Article/96079.shtml
- http://www.read.xwpxi.com/Article/5626915.shtml
- http://www.read.xwpxi.com/Article/55377.shtml
- http://www.read.xwpxi.com/Article/7633.shtml
- http://www.read.xwpxi.com/Article/08473.shtml
- http://www.read.xwpxi.com/Article/4382.shtml
- http://www.read.xwpxi.com/Article/7176914.shtml
- http://www.read.xwpxi.com/Article/003803.shtml
- http://www.read.xwpxi.com/Article/34182.shtml
- http://www.read.xwpxi.com/Article/7769.shtml
- http://www.read.xwpxi.com/Article/2026160.shtml
- http://www.read.xwpxi.com/Article/0573065.shtml
- http://www.read.xwpxi.com/Article/337273.shtml
- http://www.read.xwpxi.com/Article/596484.shtml
- http://www.read.xwpxi.com/Article/08867.shtml
- http://www.read.xwpxi.com/Article/31525.shtml
- http://www.read.xwpxi.com/Article/834697.shtml
- http://www.read.xwpxi.com/Article/897039.shtml
- http://www.read.xwpxi.com/Article/56393.shtml
- http://www.read.xwpxi.com/Article/9520247.shtml
- http://www.read.xwpxi.com/Article/9601.shtml
- http://www.read.xwpxi.com/Article/966730.shtml
- http://www.read.xwpxi.com/Article/4205269.shtml
- http://www.read.xwpxi.com/Article/2459.shtml
- http://www.read.xwpxi.com/Article/23897.shtml
- http://www.read.xwpxi.com/Article/224189.shtml
- http://www.read.xwpxi.com/Article/7781141.shtml
- http://www.read.xwpxi.com/Article/0888251.shtml
- http://www.read.xwpxi.com/Article/5478852.shtml
- http://www.read.xwpxi.com/Article/2729773.shtml
- http://www.read.xwpxi.com/Article/70728.shtml
- http://www.read.xwpxi.com/Article/6787551.shtml
- http://www.read.xwpxi.com/Article/28671.shtml
- http://www.read.xwpxi.com/Article/319671.shtml
- http://www.read.xwpxi.com/Article/73759.shtml
- http://www.read.xwpxi.com/Article/846302.shtml
- http://www.read.xwpxi.com/Article/3208.shtml
- http://www.read.xwpxi.com/Article/1707.shtml
- http://www.read.xwpxi.com/Article/1714.shtml
- http://www.read.xwpxi.com/Article/79481.shtml
- http://www.read.xwpxi.com/Article/616468.shtml
- http://www.read.xwpxi.com/Article/52103.shtml
- http://www.read.xwpxi.com/Article/1180.shtml
- http://www.read.xwpxi.com/Article/5913582.shtml
- http://www.read.xwpxi.com/Article/637551.shtml
- http://www.read.xwpxi.com/Article/2852309.shtml
- http://www.read.xwpxi.com/Article/9989.shtml
- http://www.read.xwpxi.com/Article/1897883.shtml
- http://www.read.xwpxi.com/Article/07982.shtml
- http://www.read.xwpxi.com/Article/42578.shtml
- http://www.read.xwpxi.com/Article/3258.shtml
- http://www.read.xwpxi.com/Article/6621.shtml
- http://www.read.xwpxi.com/Article/4861017.shtml
- http://www.read.xwpxi.com/Article/8644.shtml
- http://www.read.xwpxi.com/Article/5015.shtml
- http://www.read.xwpxi.com/Article/542071.shtml
- http://www.read.xwpxi.com/Article/3963.shtml
- http://www.read.xwpxi.com/Article/63819.shtml
- http://www.read.xwpxi.com/Article/206914.shtml
- http://www.read.xwpxi.com/Article/8167.shtml
- http://www.read.xwpxi.com/Article/57085.shtml
- http://www.read.xwpxi.com/Article/05943.shtml
- http://www.read.xwpxi.com/Article/248489.shtml
- http://www.read.xwpxi.com/Article/291590.shtml
- http://www.read.xwpxi.com/Article/979972.shtml
- http://www.read.xwpxi.com/Article/2612.shtml
- http://www.read.xwpxi.com/Article/4238.shtml
- http://www.read.xwpxi.com/Article/0088.shtml
- http://www.read.xwpxi.com/Article/73944.shtml
- http://www.read.xwpxi.com/Article/2646.shtml
- http://www.read.xwpxi.com/Article/916992.shtml
- http://www.read.xwpxi.com/Article/5741.shtml
- http://www.read.xwpxi.com/Article/59907.shtml
- http://www.read.xwpxi.com/Article/05132.shtml
- http://www.read.xwpxi.com/Article/2631221.shtml
- http://www.read.xwpxi.com/Article/535823.shtml
- http://www.read.xwpxi.com/Article/2632410.shtml
- http://www.read.xwpxi.com/Article/165912.shtml
- http://www.read.xwpxi.com/Article/4991805.shtml
- http://www.read.xwpxi.com/Article/6856.shtml
- http://www.read.xwpxi.com/Article/605233.shtml
- http://www.read.xwpxi.com/Article/19442.shtml
- http://www.read.xwpxi.com/Article/8732.shtml
- http://www.read.xwpxi.com/Article/8057857.shtml
- http://www.read.xwpxi.com/Article/07139.shtml
- http://www.read.xwpxi.com/Article/1862389.shtml
- http://www.read.xwpxi.com/Article/9059165.shtml
- http://www.read.xwpxi.com/Article/733430.shtml
- http://www.read.xwpxi.com/Article/79009.shtml
- http://www.read.xwpxi.com/Article/45829.shtml
- http://www.read.xwpxi.com/Article/7623.shtml
- http://www.read.xwpxi.com/Article/4709424.shtml
- http://www.read.xwpxi.com/Article/2155137.shtml
- http://www.read.xwpxi.com/Article/509922.shtml
- http://www.read.xwpxi.com/Article/862447.shtml
- http://www.read.xwpxi.com/Article/470042.shtml

## 项目结构

```
linkmaster-core/
├── cmd/                                 # 命令行入口与子命令定义
│   ├── server/                          # 启动 HTTP 服务的主程序
│   │   └── main.go                      # 初始化路由、中间件与数据库连接
│   └── worker/                          # 独立运行的异步任务执行器
│       └── main.go                      # 启动巡检与元数据抓取协程池
├── internal/                            # 内部私有包，不对外暴露
│   ├── core/                            # 核心业务逻辑实现
│   │   ├── link.go                      # 链接实体的增删改查与去重算法
│   │   ├── checker.go                   # HTTP 状态码检测与重定向跟踪逻辑
│   │   └── extractor.go                 # 基于选择器的元数据抓取引擎
│   ├── storage/                         # 数据库适配器与迁移脚本
│   │   ├── sqlite.go                    # SQLite 驱动与连接池管理
│   │   └── migrations/                  # 版本化的表结构变更 SQL 文件
│   ├── queue/                           # 任务队列封装（基于 Redis 的延迟队列）
│   │   ├── producer.go                  # 任务入队与优先级设定
│   │   └── consumer.go                  # 任务消费与重试策略
│   └── api/                             # RESTful API 路由与处理器
│       ├── handler_v1.go                # 版本 1 的端点函数实现
│       └── middleware.go                # 认证、日志与限流中间件
├── pkg/                                 # 可被外部项目引用的公共库
│   ├── httpx/                           # 增强型 HTTP 客户端（带超时与重试）
│   └── textproc/                        # 中文分词与摘要截断工具函数
├── configs/                             # 环境配置模板与默认参数
│   ├── config.yaml                      # 主配置文件（含数据库、队列、巡检间隔）
│   └── rules/                           # 各域名专用的元数据提取规则文件
├── web/                                 # 前端仪表盘源码（可选构建）
│   ├── static/                          # 编译后的 CSS 与 JavaScript 资源
│   └── templates/                       # 服务端渲染的导航页面模板
├── scripts/                             # 运维辅助脚本
│   ├── import_batch.sh                  # 批量导入 URL 列表的 Shell 工具
│   └── export_snapshot.sh               # 导出全量数据快照的 Shell 工具
├── test/                                # 单元测试与集成测试用例
│   ├── integration/                     # 依赖外部 Redis 与数据库的测试
│   └── unit/                            # 纯内存模拟的快速单元测试
├── go.mod                               # Go 模块依赖定义文件
├── go.sum                               # 依赖包的哈希校验文件
├── .env.example                         # 环境变量配置参考模板
├── Dockerfile                           # 基于 Alpine 的容器镜像构建定义
└── README.md                            # 项目说明文档（即本文档）
```

## 贡献指南

欢迎各类形式的贡献，包括但不限于新增功能、修复缺陷、完善文档或提出改进建议。请遵循以下流程以保证协作效率。

1. 查阅问题追踪列表
访问 GitHub Issues 页面，查找未被认领且标记为 `help-wanted` 或 `good-first-issue` 的任务。若准备处理现有任务，请在对应 Issue 下回复说明以避免重复工作。

2. 派生仓库并创建功能分支
将主仓库派生至个人账户下，然后克隆至本地。创建分支时请使用 `feature/` 或 `fix/` 前缀，并附上简洁的英文描述，例如 `feature/add-json-export`。

3. 编写代码与添加测试
所有新增逻辑必须包含对应的单元测试，确保测试覆盖率达到当前标准。代码风格应遵循项目配置的 golangci-lint 规则，提交前需在本地通过全部测试套件。

4. 提交变更并签署开发者原产地证书
提交信息须采用语义化格式，首行为简短摘要，空行后附详细说明。每次提交需包含 Signed-off-by 尾注，以表示您同意开发者原产地证书 1.1 版本。

5. 发起拉取请求并等待审查
推送分支至派生仓库后，向主仓库的 `main` 分支发起拉取请求。请求描述中需关联相关 Issue 编号，并根据审查意见进行修改，直至获得至少一名维护者的批准。

## 常见问题

问题：启动服务后，浏览器访问导航页面显示空白，但 API 接口可正常返回 JSON 数据。
回答：此情况通常是由于前端静态资源未正确构建或未放置于预期路径所致。请确认在启动服务前已执行 `npm run build` 或使用 `--disable-web` 参数仅以 API 模式运行。若使用 Docker 镜像，请检查挂载卷是否覆盖了 `/web/static` 目录。

问题：执行链接巡检任务后，大量链接被标记为失效，但手动访问浏览器可正常打开。
回答：LinkMaster 的巡检模块默认遵循 HTTP 严格标准，对返回 4xx 或 5xx 状态码即判定为失效。部分站点会针对非浏览器 User-Agent 返回不同状态码。您可在配置文件 `config.yaml` 的 `checker` 段下修改 `user_agent` 字段为常用浏览器标识，并启用 `follow_redirects` 选项。此外，若站点存在防火墙策略，可适当增加 `timeout` 与 `retry` 次数。

问题：如何迁移已有的浏览器书签数据至 LinkMaster？
回答：本项目未直接集成浏览器书签解析器，但您可使用通用转换路径。主流浏览器均支持将书签导出为 HTML 文件。您可使用第三方工具如 `bookmarks-to-json` 将该 HTML 转换为包含 `url` 和 `title` 字段的 JSON 数组，随后通过 LinkMaster 提供的 `POST /api/v1/links/batch` 接口批量导入。若需要保留书签的文件夹层级结构，可先手动在 LinkMaster 中创建对应分类，再逐类导入。

## 许可证

MIT License

Copyright (c) 2025 LinkMaster Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
