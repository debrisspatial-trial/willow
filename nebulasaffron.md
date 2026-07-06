# WebReads 技术文章索引与导航系统

WebReads 是一个面向开发者和技术研究人员的结构化外链资源汇总与导航系统。该项目并不生产原创内容，而是通过人工筛选与自动化采集相结合的方式，对散布于互联网各处的优质技术文章、教程、案例分析与工程实践文档进行系统化整理、分类索引与永久归档。WebReads 适用于需要快速查阅特定技术主题、追溯技术演进脉络或寻找参考实现的开发者，同时也适用于技术团队内部建立知识库外链池的场景。

本项目的核心价值在于降低技术信息的发现成本。互联网上的技术内容高度碎片化，优质文章往往淹没在重复或低质内容之中。WebReads 通过对资源链接进行主题标注、质量评级与失效检测，使开发者能够在数秒内定位到所需的高价值外部资源，而非在搜索引擎的多个页面间反复跳转。项目采用静态站点生成机制，所有资源数据以 Markdown 与 YAML 格式存储于仓库中，支持本地检索、自定义标签过滤与按日期排序。

## 功能概览

多层级分类索引：支持按编程语言、框架、数据库、操作系统、算法与数据结构、工程实践等一级分类进行浏览，每个一级分类下包含若干二级子分类，便于精确定位。

全文检索与元数据过滤：基于 Lunr.js 或同类静态索引方案实现前端全文搜索，同时支持按发布时间、作者、来源域名、内容类型（教程、参考手册、案例研究、性能调优报告）进行多维度筛选过滤。

资源健康度监控：每日定时执行链接可达性检查，自动标记失效链接、重定向链接与响应缓慢链接，并在管理后台提供批量更新或移除操作界面。

用户自定义收藏夹与标签系统：注册用户可创建个人收藏夹，对资源链接添加自定义标签与备注，支持私有与公开两种可见性模式。

批量导入与导出接口：支持通过 CSV 或 JSON 格式批量导入外部资源链接，同时提供标准化的 JSON API 与 RSS 订阅源供第三方工具调用或二次开发。

资源版本追踪与历史快照：对每个资源链接记录其首次收录时间、最后验证时间与内容摘要哈希值，当目标页面内容发生显著变化时系统发出通知，便于维护者更新描述信息。

社区协作编辑机制：具备贡献者权限的用户可提交资源链接的新增、编辑或废弃申请，经审核后合并入主索引库，所有变更记录完整保留于 Git 提交日志中。

## 应用场景

技术团队内部知识库外链管理。技术团队在日常开发中会积累大量参考链接，散落于文档、Wiki 或聊天记录中，难以维护与复用。WebReads 提供统一的外链入库、分类与检索界面，团队可将经过验证的优质资源集中托管，新成员入职或遇到技术难题时可快速查阅前人整理的材料。

个人开发者的技术阅读与学习路线规划。开发者可使用 WebReads 订阅特定分类的新增资源，每日获取经过筛选的高质量文章推送，避免在海量信息中迷失方向。结合标签与收藏功能，可构建个人专属的技术文献库，用于面试准备、新技术预研或深度专题学习。

开源项目文档站的外部参考资料附录。开源项目在撰写文档时往往需要引用外部标准规范、协议说明或相关实现参考。WebReads 可作为子模块嵌入项目文档站点，以结构化列表形式呈现所有外部引用链接，并自动生成引用编号与双向链接，提升文档的权威性与可追溯性。

技术内容聚合站或导航站的后端数据源。对于运营技术博客聚合站或垂直领域导航站的站长，WebReads 可作为后端数据管理工具，提供标准化的数据导入导出流程与 API 接口，简化链接数据的采集、清洗与更新工作。

## 快速开始

以下命令可在本地环境完成 WebReads 项目的克隆、依赖安装与开发服务器启动。

```bash
git clone https://github.com/webreads/webreads.git
cd webreads
npm install
npm run build
npm start
```

执行完成后，访问 http://localhost:3000 即可浏览本地实例。默认管理员账户为 admin，初始密码在首次启动时自动生成并输出至控制台日志。生产环境部署请参考 `docs/deployment.md` 中的说明，配置环境变量 `DATABASE_URL` 与 `JWT_SECRET`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.x LTS 或 20.x LTS | 运行时环境，推荐使用 NVM 管理版本 |
| npm | 9.x 或以上 | 包管理器，用于安装项目依赖 |
| PostgreSQL | 14.x 或以上 | 主数据库，存储用户数据、标签与资源元信息 |
| Redis | 6.x 或以上 | 缓存与任务队列后端，用于链接健康度检查任务的调度 |
| Elasticsearch | 7.x 或 8.x | 可选依赖，用于提升全文检索性能，若不安装则回退至 Lunr.js 本地索引 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | docs/user-guide/ | 如何注册账号、创建收藏夹、使用搜索与筛选功能、导入导出数据 |
| 管理员指南 | docs/admin-guide/ | 如何配置链接健康度检查策略、管理用户权限、处理协作编辑申请 |
| 开发者文档 | docs/developer-guide/ | 如何二次开发插件、扩展分类体系、对接外部 API 或编写自定义数据导入脚本 |
| 部署运维手册 | docs/ops-guide/ | 生产环境部署架构、性能调优参数、备份恢复策略与监控告警配置 |

## 资源列表

- http://www.read.xwpxi.com/Article/2173.shtml
- http://www.read.xwpxi.com/Article/18708.shtml
- http://www.read.xwpxi.com/Article/055223.shtml
- http://www.read.xwpxi.com/Article/5496090.shtml
- http://www.read.xwpxi.com/Article/8328.shtml
- http://www.read.xwpxi.com/Article/9184.shtml
- http://www.read.xwpxi.com/Article/11626.shtml
- http://www.read.xwpxi.com/Article/4298610.shtml
- http://www.read.xwpxi.com/Article/4607.shtml
- http://www.read.xwpxi.com/Article/1941.shtml
- http://www.read.xwpxi.com/Article/3895.shtml
- http://www.read.xwpxi.com/Article/70008.shtml
- http://www.read.xwpxi.com/Article/4562999.shtml
- http://www.read.xwpxi.com/Article/6315949.shtml
- http://www.read.xwpxi.com/Article/798385.shtml
- http://www.read.xwpxi.com/Article/19542.shtml
- http://www.read.xwpxi.com/Article/5265296.shtml
- http://www.read.xwpxi.com/Article/211857.shtml
- http://www.read.xwpxi.com/Article/9045.shtml
- http://www.read.xwpxi.com/Article/229371.shtml
- http://www.read.xwpxi.com/Article/76737.shtml
- http://www.read.xwpxi.com/Article/692208.shtml
- http://www.read.xwpxi.com/Article/2823.shtml
- http://www.read.xwpxi.com/Article/335687.shtml
- http://www.read.xwpxi.com/Article/1533349.shtml
- http://www.read.xwpxi.com/Article/0160.shtml
- http://www.read.xwpxi.com/Article/54990.shtml
- http://www.read.xwpxi.com/Article/91941.shtml
- http://www.read.xwpxi.com/Article/6797.shtml
- http://www.read.xwpxi.com/Article/3562164.shtml
- http://www.read.xwpxi.com/Article/1061480.shtml
- http://www.read.xwpxi.com/Article/35921.shtml
- http://www.read.xwpxi.com/Article/79889.shtml
- http://www.read.xwpxi.com/Article/2206133.shtml
- http://www.read.xwpxi.com/Article/92252.shtml
- http://www.read.xwpxi.com/Article/5932.shtml
- http://www.read.xwpxi.com/Article/3371.shtml
- http://www.read.xwpxi.com/Article/092588.shtml
- http://www.read.xwpxi.com/Article/415905.shtml
- http://www.read.xwpxi.com/Article/550830.shtml
- http://www.read.xwpxi.com/Article/61086.shtml
- http://www.read.xwpxi.com/Article/4703307.shtml
- http://www.read.xwpxi.com/Article/4288745.shtml
- http://www.read.xwpxi.com/Article/429386.shtml
- http://www.read.xwpxi.com/Article/90400.shtml
- http://www.read.xwpxi.com/Article/367871.shtml
- http://www.read.xwpxi.com/Article/05054.shtml
- http://www.read.xwpxi.com/Article/549453.shtml
- http://www.read.xwpxi.com/Article/635209.shtml
- http://www.read.xwpxi.com/Article/5652.shtml
- http://www.read.xwpxi.com/Article/0031.shtml
- http://www.read.xwpxi.com/Article/57900.shtml
- http://www.read.xwpxi.com/Article/791925.shtml
- http://www.read.xwpxi.com/Article/2000094.shtml
- http://www.read.xwpxi.com/Article/510905.shtml
- http://www.read.xwpxi.com/Article/7267.shtml
- http://www.read.xwpxi.com/Article/62999.shtml
- http://www.read.xwpxi.com/Article/55498.shtml
- http://www.read.xwpxi.com/Article/1039148.shtml
- http://www.read.xwpxi.com/Article/0614.shtml
- http://www.read.xwpxi.com/Article/02104.shtml
- http://www.read.xwpxi.com/Article/1721874.shtml
- http://www.read.xwpxi.com/Article/1039267.shtml
- http://www.read.xwpxi.com/Article/2702.shtml
- http://www.read.xwpxi.com/Article/4206000.shtml
- http://www.read.xwpxi.com/Article/640853.shtml
- http://www.read.xwpxi.com/Article/6140152.shtml
- http://www.read.xwpxi.com/Article/5804.shtml
- http://www.read.xwpxi.com/Article/77122.shtml
- http://www.read.xwpxi.com/Article/01351.shtml
- http://www.read.xwpxi.com/Article/50274.shtml
- http://www.read.xwpxi.com/Article/6675073.shtml
- http://www.read.xwpxi.com/Article/69155.shtml
- http://www.read.xwpxi.com/Article/57476.shtml
- http://www.read.xwpxi.com/Article/069889.shtml
- http://www.read.xwpxi.com/Article/1649800.shtml
- http://www.read.xwpxi.com/Article/4265.shtml
- http://www.read.xwpxi.com/Article/1912.shtml
- http://www.read.xwpxi.com/Article/69941.shtml
- http://www.read.xwpxi.com/Article/83556.shtml
- http://www.read.xwpxi.com/Article/57521.shtml
- http://www.read.xwpxi.com/Article/4451667.shtml
- http://www.read.xwpxi.com/Article/3034.shtml
- http://www.read.xwpxi.com/Article/2573324.shtml
- http://www.read.xwpxi.com/Article/20261.shtml
- http://www.read.xwpxi.com/Article/476250.shtml
- http://www.read.xwpxi.com/Article/77950.shtml
- http://www.read.xwpxi.com/Article/76036.shtml
- http://www.read.xwpxi.com/Article/6597424.shtml
- http://www.read.xwpxi.com/Article/9564.shtml
- http://www.read.xwpxi.com/Article/152886.shtml
- http://www.read.xwpxi.com/Article/8722358.shtml
- http://www.read.xwpxi.com/Article/685630.shtml
- http://www.read.xwpxi.com/Article/8257.shtml
- http://www.read.xwpxi.com/Article/19462.shtml
- http://www.read.xwpxi.com/Article/1863.shtml
- http://www.read.xwpxi.com/Article/157332.shtml
- http://www.read.xwpxi.com/Article/0605.shtml
- http://www.read.xwpxi.com/Article/6414.shtml
- http://www.read.xwpxi.com/Article/315139.shtml
- http://www.read.xwpxi.com/Article/3499.shtml
- http://www.read.xwpxi.com/Article/34042.shtml
- http://www.read.xwpxi.com/Article/50600.shtml
- http://www.read.xwpxi.com/Article/6330.shtml
- http://www.read.xwpxi.com/Article/5416811.shtml
- http://www.read.xwpxi.com/Article/727065.shtml
- http://www.read.xwpxi.com/Article/6098.shtml
- http://www.read.xwpxi.com/Article/1270143.shtml
- http://www.read.xwpxi.com/Article/0495.shtml
- http://www.read.xwpxi.com/Article/88405.shtml
- http://www.read.xwpxi.com/Article/805025.shtml
- http://www.read.xwpxi.com/Article/185497.shtml
- http://www.read.xwpxi.com/Article/8102.shtml
- http://www.read.xwpxi.com/Article/342909.shtml
- http://www.read.xwpxi.com/Article/7389.shtml
- http://www.read.xwpxi.com/Article/5638.shtml
- http://www.read.xwpxi.com/Article/7647667.shtml
- http://www.read.xwpxi.com/Article/996362.shtml
- http://www.read.xwpxi.com/Article/797127.shtml
- http://www.read.xwpxi.com/Article/597460.shtml
- http://www.read.xwpxi.com/Article/0824.shtml
- http://www.read.xwpxi.com/Article/469798.shtml
- http://www.read.xwpxi.com/Article/063918.shtml
- http://www.read.xwpxi.com/Article/382058.shtml
- http://www.read.xwpxi.com/Article/9248914.shtml
- http://www.read.xwpxi.com/Article/669402.shtml
- http://www.read.xwpxi.com/Article/44878.shtml
- http://www.read.xwpxi.com/Article/6674.shtml
- http://www.read.xwpxi.com/Article/4326823.shtml
- http://www.read.xwpxi.com/Article/937180.shtml
- http://www.read.xwpxi.com/Article/3902.shtml
- http://www.read.xwpxi.com/Article/10919.shtml
- http://www.read.xwpxi.com/Article/6097476.shtml
- http://www.read.xwpxi.com/Article/16685.shtml
- http://www.read.xwpxi.com/Article/07581.shtml
- http://www.read.xwpxi.com/Article/45530.shtml
- http://www.read.xwpxi.com/Article/7858947.shtml
- http://www.read.xwpxi.com/Article/1992257.shtml
- http://www.read.xwpxi.com/Article/9754.shtml
- http://www.read.xwpxi.com/Article/2342444.shtml
- http://www.read.xwpxi.com/Article/0405.shtml
- http://www.read.xwpxi.com/Article/845678.shtml
- http://www.read.xwpxi.com/Article/828769.shtml
- http://www.read.xwpxi.com/Article/300861.shtml
- http://www.read.xwpxi.com/Article/2234810.shtml
- http://www.read.xwpxi.com/Article/8852188.shtml
- http://www.read.xwpxi.com/Article/96801.shtml
- http://www.read.xwpxi.com/Article/373839.shtml
- http://www.read.xwpxi.com/Article/60345.shtml
- http://www.read.xwpxi.com/Article/409586.shtml
- http://www.read.xwpxi.com/Article/41812.shtml
- http://www.read.xwpxi.com/Article/737438.shtml
- http://www.read.xwpxi.com/Article/9733.shtml
- http://www.read.xwpxi.com/Article/5020.shtml
- http://www.read.xwpxi.com/Article/017203.shtml
- http://www.read.xwpxi.com/Article/0889546.shtml
- http://www.read.xwpxi.com/Article/07112.shtml
- http://www.read.xwpxi.com/Article/2558089.shtml
- http://www.read.xwpxi.com/Article/2795533.shtml
- http://www.read.xwpxi.com/Article/2158.shtml
- http://www.read.xwpxi.com/Article/198857.shtml
- http://www.read.xwpxi.com/Article/15296.shtml
- http://www.read.xwpxi.com/Article/0290715.shtml
- http://www.read.xwpxi.com/Article/620447.shtml
- http://www.read.xwpxi.com/Article/97938.shtml
- http://www.read.xwpxi.com/Article/0507199.shtml
- http://www.read.xwpxi.com/Article/7273683.shtml
- http://www.read.xwpxi.com/Article/539065.shtml
- http://www.read.xwpxi.com/Article/20888.shtml
- http://www.read.xwpxi.com/Article/9359027.shtml
- http://www.read.xwpxi.com/Article/8397807.shtml
- http://www.read.xwpxi.com/Article/7599887.shtml
- http://www.read.xwpxi.com/Article/8188.shtml
- http://www.read.xwpxi.com/Article/4401079.shtml
- http://www.read.xwpxi.com/Article/4847768.shtml
- http://www.read.xwpxi.com/Article/9285.shtml
- http://www.read.xwpxi.com/Article/3507.shtml
- http://www.read.xwpxi.com/Article/4287.shtml
- http://www.read.xwpxi.com/Article/2206718.shtml
- http://www.read.xwpxi.com/Article/2414.shtml
- http://www.read.xwpxi.com/Article/648513.shtml
- http://www.read.xwpxi.com/Article/922530.shtml
- http://www.read.xwpxi.com/Article/10793.shtml
- http://www.read.xwpxi.com/Article/817747.shtml
- http://www.read.xwpxi.com/Article/3949869.shtml
- http://www.read.xwpxi.com/Article/43994.shtml
- http://www.read.xwpxi.com/Article/44367.shtml
- http://www.read.xwpxi.com/Article/22293.shtml
- http://www.read.xwpxi.com/Article/63608.shtml
- http://www.read.xwpxi.com/Article/82429.shtml
- http://www.read.xwpxi.com/Article/5531.shtml
- http://www.read.xwpxi.com/Article/0841852.shtml
- http://www.read.xwpxi.com/Article/53243.shtml
- http://www.read.xwpxi.com/Article/64031.shtml
- http://www.read.xwpxi.com/Article/98348.shtml
- http://www.read.xwpxi.com/Article/90212.shtml
- http://www.read.xwpxi.com/Article/031342.shtml
- http://www.read.xwpxi.com/Article/7106417.shtml
- http://www.read.xwpxi.com/Article/35984.shtml
- http://www.read.xwpxi.com/Article/9148.shtml
- http://www.read.xwpxi.com/Article/1770230.shtml
- http://www.read.xwpxi.com/Article/989261.shtml
- http://www.read.xwpxi.com/Article/2616.shtml
- http://www.read.xwpxi.com/Article/4546.shtml
- http://www.read.xwpxi.com/Article/228883.shtml
- http://www.read.xwpxi.com/Article/1266959.shtml
- http://www.read.xwpxi.com/Article/4605560.shtml
- http://www.read.xwpxi.com/Article/6075.shtml
- http://www.read.xwpxi.com/Article/3985428.shtml
- http://www.read.xwpxi.com/Article/789320.shtml
- http://www.read.xwpxi.com/Article/4468985.shtml
- http://www.read.xwpxi.com/Article/6983554.shtml
- http://www.read.xwpxi.com/Article/110005.shtml
- http://www.read.xwpxi.com/Article/4221.shtml
- http://www.read.xwpxi.com/Article/8825.shtml
- http://www.read.xwpxi.com/Article/1834265.shtml
- http://www.read.xwpxi.com/Article/462196.shtml
- http://www.read.xwpxi.com/Article/1221.shtml
- http://www.read.xwpxi.com/Article/198047.shtml
- http://www.read.xwpxi.com/Article/4547.shtml
- http://www.read.xwpxi.com/Article/12131.shtml
- http://www.read.xwpxi.com/Article/1837915.shtml
- http://www.read.xwpxi.com/Article/7615034.shtml
- http://www.read.xwpxi.com/Article/765474.shtml
- http://www.read.xwpxi.com/Article/7916.shtml
- http://www.read.xwpxi.com/Article/575953.shtml
- http://www.read.xwpxi.com/Article/102232.shtml
- http://www.read.xwpxi.com/Article/0404958.shtml
- http://www.read.xwpxi.com/Article/9740045.shtml
- http://www.read.xwpxi.com/Article/17255.shtml
- http://www.read.xwpxi.com/Article/0363148.shtml
- http://www.read.xwpxi.com/Article/36459.shtml
- http://www.read.xwpxi.com/Article/990616.shtml
- http://www.read.xwpxi.com/Article/7284620.shtml
- http://www.read.xwpxi.com/Article/9117.shtml
- http://www.read.xwpxi.com/Article/57630.shtml
- http://www.read.xwpxi.com/Article/05259.shtml
- http://www.read.xwpxi.com/Article/56342.shtml
- http://www.read.xwpxi.com/Article/5570680.shtml
- http://www.read.xwpxi.com/Article/9322.shtml
- http://www.read.xwpxi.com/Article/680011.shtml
- http://www.read.xwpxi.com/Article/7322.shtml
- http://www.read.xwpxi.com/Article/0688393.shtml
- http://www.read.xwpxi.com/Article/93629.shtml
- http://www.read.xwpxi.com/Article/374829.shtml
- http://www.read.xwpxi.com/Article/17531.shtml
- http://www.read.xwpxi.com/Article/66304.shtml
- http://www.read.xwpxi.com/Article/553026.shtml
- http://www.read.xwpxi.com/Article/5521.shtml
- http://www.read.xwpxi.com/Article/320400.shtml

## 项目结构

```
webreads/
├── src/                               # 应用核心源代码
│   ├── api/                           # RESTful API 路由与控制器
│   │   ├── v1/                        # API 版本 v1 实现
│   │   │   ├── resources/             # 资源链接 CRUD 接口
│   │   │   ├── users/                 # 用户认证与个人信息接口
│   │   │   └── tags/                  # 标签管理与关联接口
│   │   └── middleware/                # 鉴权、限流、日志中间件
│   ├── services/                      # 业务逻辑层
│   │   ├── crawler/                   # 链接健康度检查与元数据抓取服务
│   │   ├── search/                    # 索引构建与搜索服务（Elasticsearch 适配器）
│   │   └── scheduler/                 # 任务调度服务（基于 Bull 队列）
│   ├── models/                        # 数据模型定义（Sequelize / TypeORM 实体）
│   │   ├── Resource.ts                # 资源链接主表模型
│   │   ├── User.ts                    # 用户账户模型
│   │   ├── Collection.ts              # 收藏夹模型
│   │   └── AuditLog.ts                # 操作审计日志模型
│   ├── frontend/                      # 前端静态资源（React / Vue 构建输出）
│   │   ├── components/                # 可复用 UI 组件
│   │   ├── pages/                     # 页面级组件（首页、分类浏览、搜索、个人中心）
│   │   └── assets/                    # 样式表、图片与字体文件
│   └── utils/                         # 通用工具函数
│       ├── validator.ts               # URL 校验与规范化工具
│       ├── markdown.ts                # Markdown 元数据解析器
│       └── cache.ts                   # Redis 缓存封装
├── data/                              # 静态数据存储目录
│   ├── resources/                     # 资源链接原始数据（YAML / JSON 格式）
│   │   ├── programming/               # 编程语言分类
│   │   ├── frameworks/                # 框架分类
│   │   ├── databases/                 # 数据库分类
│   │   └── operations/                # 运维与基础设施分类
│   ├── categories.yml                 # 分类体系定义文件
│   └── tags.yml                       # 预设标签白名单
├── docs/                              # 项目文档
│   ├── user-guide/                    # 用户手册
│   ├── admin-guide/                   # 管理员指南
│   ├── developer-guide/               # 开发者文档
│   └── ops-guide/                     # 部署运维手册
├── tests/                             # 单元测试与集成测试
│   ├── unit/                          # 单元测试用例
│   ├── integration/                   # API 集成测试
│   └── fixtures/                      # 测试数据夹具
├── scripts/                           # 运维与工具脚本
│   ├── health-check.js                # 批量链接健康度检查脚本
│   ├── import-csv.js                  # CSV 批量导入脚本
│   └── migrate-db.js                  # 数据库迁移脚本
├── config/                            # 环境配置文件
│   ├── default.yaml                   # 默认配置
│   ├── development.yaml               # 开发环境配置
│   ├── production.yaml                # 生产环境配置
│   └── test.yaml                      # 测试环境配置
├── .github/                           # GitHub Actions CI/CD 工作流
│   └── workflows/
│       ├── ci.yml                     # 持续集成流水线
│       └── deploy.yml                 # 自动部署流水线
├── docker-compose.yml                 # Docker Compose 本地开发编排文件
├── Dockerfile                         # 生产环境容器镜像构建文件
├── package.json                       # npm 依赖声明
├── tsconfig.json                      # TypeScript 编译配置
├── .eslintrc.js                       # ESLint 代码检查配置
├── .prettierrc                        # Prettier 代码格式化配置
└── README.md                          # 项目介绍文档（本文件）
```

## 贡献指南

贡献者需先查阅项目行为准则并在首次提交时签署贡献者许可协议。所有贡献均通过 GitHub Pull Request 流程进行，主分支为 main，开发分支为 develop。

具体步骤如下：复刻项目仓库至个人账户，在本地将复刻仓库克隆至开发环境，并基于 develop 分支创建新的功能分支，分支命名需遵循 `feature/描述` 或 `fix/描述` 格式。完成代码修改后，运行 `npm run lint` 与 `npm run test` 确保代码风格与测试用例全部通过，并补充或更新相关单元测试与文档。提交 Pull Request 至上游仓库的 develop 分支，在 PR 描述中清晰说明变更目的、影响范围与测试情况，至少需要一位项目维护者审核批准后方可合并。对于资源链接的新增或编辑请求，贡献者需在 `data/resources/` 对应分类目录下创建或修改 YAML 文件，并确保 URL 字段为可访问的有效地址，描述字段不少于 20 个中文字符。

## 常见问题

Q: 系统每日检查链接健康度时，如何处理被屏蔽或需要特殊用户代理的网站？

A: 系统默认使用无头浏览器 User-Agent 字符串，并遵循 robots.txt 协议。对于需要特殊 Cookie 或登录态的目标站点，管理员可在配置文件中为特定域名设置自定义请求头或代理规则。若目标站点频繁返回 403 或 429 状态码，系统会自动将该域名加入降频扫描名单，将检查间隔从每日延长至每周。

Q: 是否可以完全离线使用 WebReads，不依赖 Elasticsearch 和 Redis？

A: 可以。系统提供精简模式，当环境变量 `ELASTICSEARCH_ENABLED=false` 且 `REDIS_ENABLED=false` 时，自动回退至基于 SQL 数据库的 LIKE 查询和内存队列。但该模式不适用于大规模数据场景（资源链接超过 5000 条时查询响应可能超过 3 秒），建议生产环境完整部署所有依赖组件。

Q: 如何将现有浏览器书签或 Pocket 收藏批量迁移至 WebReads？

A: 系统支持导入 Netscape Bookmark HTML 格式文件，该格式为大多数浏览器和书签服务所通用。用户可在个人中心的导入页面选择书签 HTML 文件上传，系统会自动解析并提取 URL、标题和添加时间，随后引导用户对未分类条目进行批量分类操作。对于 Pocket 用户，推荐先使用 Pocket 官方导出功能获取 HTML 文件后再导入。

## 许可证

MIT

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
