# LinkMaster 聚合资源导航系统

LinkMaster 是一个面向技术内容聚合与资源导航的开源平台，专注于将分散在网络各处的优质技术文章、教程、工具文档和开发资源进行系统化收录与分类管理。该系统定位于个人开发者、技术团队和知识管理爱好者，旨在解决技术资料检索效率低下、收藏夹混乱、好内容容易被遗忘等问题。

LinkMaster 通过自动化的资源采集接口与人工标注相结合的方式，为每个资源条目生成标签、摘要和关联推荐，并提供全文检索与分类筛选能力。项目本身不存储资源内容，仅保留元数据与跳转链接，确保版权合规的同时为开发者提供高速、稳定的导航服务。

## 功能概览

批量资源导入与去重 系统提供命令行导入工具和 RESTful API，支持从 CSV、JSON 和 Markdown 列表批量导入 URL，并基于 URL 指纹和页面标题进行智能去重，避免重复收录。

自定义标签与分类体系 用户可以为每个资源创建多级标签，支持父子分类、别名映射和颜色标记，便于构建符合个人或团队认知习惯的知识树。

全文检索引擎 基于 SQLite FTS5 或可选的 Elasticsearch 后端，对资源的标题、摘要、标签和自定义备注进行全文检索，支持布尔查询、短语匹配和模糊搜索。

资源健康度检查 定期对已收录的 URL 发起 HEAD 请求，检测链接是否可访问、响应时间是否异常、页面标题是否变更，并将异常状态通过 Webhook 通知管理员。

用户收藏与阅读清单 注册用户可以将资源加入个人收藏夹或创建主题阅读清单，支持公开清单的分享与嵌入，方便团队内部进行知识传递。

数据导出与备份 支持将全部资源元数据导出为 JSON、CSV 或 SQLite 数据库文件，方便用户进行离线分析或迁移至其他知识管理工具。

浏览器书签同步插件 提供 Chrome 和 Firefox 浏览器扩展，用户可以从插件端快速提交新资源，或将浏览器书签一键同步至 LinkMaster 系统。

## 应用场景

个人技术博客的扩展阅读推荐 技术博主可以在文章底部嵌入 LinkMaster 提供的相关资源挂件，为读者自动推荐本博客历史文章以及站外优质资料，提升文章的信息密度和读者停留时长。

开源项目文档站的外部资源引用 开源项目维护者可以在项目的 README 或文档站中引用 LinkMaster 收录的教程、视频和工具列表，避免在项目仓库中维护庞大的外部链接列表，降低维护成本。

技术团队内部知识库的素材来源 技术团队的 Leader 或文档管理员可以使用 LinkMaster 构建团队专属的「精选技术资料库」，将团队成员日常分享的好文章统一收录，并通过共享清单实现知识沉淀与新人培训。

技术社区的内容聚合与推荐 中小型技术社区或垂直领域论坛可以接入 LinkMaster 的公共 API，在首页或板块顶部展示热门资源排行，减轻社区编辑人工采集内容的压力。

个人开发者每日阅读路线规划 开发者可以在每日工作开始前，通过 LinkMaster 的「随机推荐」和「未读清单」功能快速筛选出当天值得阅读的 5-10 篇文章，形成规律的技术输入习惯。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境。

```bash
# 克隆项目仓库
git clone https://github.com/your-org/linkmaster.git
cd linkmaster

# 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化 SQLite 数据库和配置文件
cp .env.example .env
python scripts/init_db.py

# 运行开发服务器
python app.py --host 0.0.0.0 --port 8080
```

访问 http://localhost:8080 即可进入系统首页。管理员初始账号为 admin / admin123，首次登录后请立即修改密码。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 - 3.11 | 核心运行环境，3.12 及以上暂未测试 |
| SQLite | 3.35.0+ | 内置 FTS5 全文索引支持，需编译开启 |
| Redis | 6.0+ | 用于缓存和任务队列（可选，生产环境推荐） |
| Node.js | 18.x | 仅用于前端资产构建，不影响后端运行 |
| Elasticsearch | 7.x 或 8.x | 可选全文检索引擎，用于替代 SQLite FTS5 |
| Nginx | 1.20+ | 生产环境反向代理和静态资源服务 |
| Supervisor | 4.2+ | 进程守护（生产环境推荐） |
| Git | 2.30+ | 版本控制和自动部署脚本依赖 |
| make | 3.82+ | 用于执行自动化构建任务 |
| curl | 7.68+ | 健康检查脚本的依赖工具 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 入门 | /docs/quickstart.md | 如何在 5 分钟内完成安装并导入第一批资源？ |
| 使用 | /docs/user-guide.md | 如何添加标签、创建清单、检索资源和共享列表？ |
| 管理 | /docs/admin-operations.md | 如何配置健康检查、Webhook 通知和用户权限？ |
| 开发 | /docs/contributing.md | 如何本地调试 API、编写插件和提交代码变更？ |
| 部署 | /docs/deployment.md | 如何使用 Docker Compose 或 Kubernetes 进行生产部署？ |
| API | /docs/api-reference.md | 所有 RESTful 端点的请求/响应格式和鉴权方式是什么？ |

## 资源列表

- http://www.read.xwpxi.com/Article/510070.shtml
- http://www.read.xwpxi.com/Article/701196.shtml
- http://www.read.xwpxi.com/Article/12663.shtml
- http://www.read.xwpxi.com/Article/6974553.shtml
- http://www.read.xwpxi.com/Article/8315.shtml
- http://www.read.xwpxi.com/Article/115455.shtml
- http://www.read.xwpxi.com/Article/2871204.shtml
- http://www.read.xwpxi.com/Article/44653.shtml
- http://www.read.xwpxi.com/Article/9334.shtml
- http://www.read.xwpxi.com/Article/8015.shtml
- http://www.read.xwpxi.com/Article/04417.shtml
- http://www.read.xwpxi.com/Article/8872.shtml
- http://www.read.xwpxi.com/Article/7910.shtml
- http://www.read.xwpxi.com/Article/950147.shtml
- http://www.read.xwpxi.com/Article/5965.shtml
- http://www.read.xwpxi.com/Article/41880.shtml
- http://www.read.xwpxi.com/Article/0949974.shtml
- http://www.read.xwpxi.com/Article/80324.shtml
- http://www.read.xwpxi.com/Article/279622.shtml
- http://www.read.xwpxi.com/Article/10075.shtml
- http://www.read.xwpxi.com/Article/10612.shtml
- http://www.read.xwpxi.com/Article/679838.shtml
- http://www.read.xwpxi.com/Article/83856.shtml
- http://www.read.xwpxi.com/Article/908144.shtml
- http://www.read.xwpxi.com/Article/972079.shtml
- http://www.read.xwpxi.com/Article/83356.shtml
- http://www.read.xwpxi.com/Article/2189.shtml
- http://www.read.xwpxi.com/Article/34663.shtml
- http://www.read.xwpxi.com/Article/272475.shtml
- http://www.read.xwpxi.com/Article/2636.shtml
- http://www.read.xwpxi.com/Article/59621.shtml
- http://www.read.xwpxi.com/Article/085557.shtml
- http://www.read.xwpxi.com/Article/8860753.shtml
- http://www.read.xwpxi.com/Article/06573.shtml
- http://www.read.xwpxi.com/Article/6172956.shtml
- http://www.read.xwpxi.com/Article/0610660.shtml
- http://www.read.xwpxi.com/Article/93970.shtml
- http://www.read.xwpxi.com/Article/23289.shtml
- http://www.read.xwpxi.com/Article/3914808.shtml
- http://www.read.xwpxi.com/Article/30674.shtml
- http://www.read.xwpxi.com/Article/0671726.shtml
- http://www.read.xwpxi.com/Article/74924.shtml
- http://www.read.xwpxi.com/Article/0445038.shtml
- http://www.read.xwpxi.com/Article/252436.shtml
- http://www.read.xwpxi.com/Article/8408.shtml
- http://www.read.xwpxi.com/Article/514841.shtml
- http://www.read.xwpxi.com/Article/9014.shtml
- http://www.read.xwpxi.com/Article/9766.shtml
- http://www.read.xwpxi.com/Article/6850896.shtml
- http://www.read.xwpxi.com/Article/23710.shtml
- http://www.read.xwpxi.com/Article/3012.shtml
- http://www.read.xwpxi.com/Article/259785.shtml
- http://www.read.xwpxi.com/Article/233003.shtml
- http://www.read.xwpxi.com/Article/9140994.shtml
- http://www.read.xwpxi.com/Article/79142.shtml
- http://www.read.xwpxi.com/Article/6719107.shtml
- http://www.read.xwpxi.com/Article/0862.shtml
- http://www.read.xwpxi.com/Article/8799.shtml
- http://www.read.xwpxi.com/Article/5906.shtml
- http://www.read.xwpxi.com/Article/86401.shtml
- http://www.read.xwpxi.com/Article/88122.shtml
- http://www.read.xwpxi.com/Article/66798.shtml
- http://www.read.xwpxi.com/Article/630351.shtml
- http://www.read.xwpxi.com/Article/71870.shtml
- http://www.read.xwpxi.com/Article/7653525.shtml
- http://www.read.xwpxi.com/Article/6657.shtml
- http://www.read.xwpxi.com/Article/214196.shtml
- http://www.read.xwpxi.com/Article/939740.shtml
- http://www.read.xwpxi.com/Article/3236.shtml
- http://www.read.xwpxi.com/Article/0563999.shtml
- http://www.read.xwpxi.com/Article/376934.shtml
- http://www.read.xwpxi.com/Article/74396.shtml
- http://www.read.xwpxi.com/Article/4271.shtml
- http://www.read.xwpxi.com/Article/6558880.shtml
- http://www.read.xwpxi.com/Article/7999120.shtml
- http://www.read.xwpxi.com/Article/4622.shtml
- http://www.read.xwpxi.com/Article/10239.shtml
- http://www.read.xwpxi.com/Article/94990.shtml
- http://www.read.xwpxi.com/Article/946065.shtml
- http://www.read.xwpxi.com/Article/402054.shtml
- http://www.read.xwpxi.com/Article/0641.shtml
- http://www.read.xwpxi.com/Article/00000.shtml
- http://www.read.xwpxi.com/Article/7177.shtml
- http://www.read.xwpxi.com/Article/5283548.shtml
- http://www.read.xwpxi.com/Article/8416234.shtml
- http://www.read.xwpxi.com/Article/8337.shtml
- http://www.read.xwpxi.com/Article/63156.shtml
- http://www.read.xwpxi.com/Article/9566895.shtml
- http://www.read.xwpxi.com/Article/456448.shtml
- http://www.read.xwpxi.com/Article/9828717.shtml
- http://www.read.xwpxi.com/Article/455739.shtml
- http://www.read.xwpxi.com/Article/98179.shtml
- http://www.read.xwpxi.com/Article/5328678.shtml
- http://www.read.xwpxi.com/Article/0350657.shtml
- http://www.read.xwpxi.com/Article/4276.shtml
- http://www.read.xwpxi.com/Article/4010.shtml
- http://www.read.xwpxi.com/Article/23361.shtml
- http://www.read.xwpxi.com/Article/3125081.shtml
- http://www.read.xwpxi.com/Article/511291.shtml
- http://www.read.xwpxi.com/Article/1981.shtml
- http://www.read.xwpxi.com/Article/1210572.shtml
- http://www.read.xwpxi.com/Article/0400.shtml
- http://www.read.xwpxi.com/Article/382953.shtml
- http://www.read.xwpxi.com/Article/3799575.shtml
- http://www.read.xwpxi.com/Article/5546.shtml
- http://www.read.xwpxi.com/Article/6598093.shtml
- http://www.read.xwpxi.com/Article/6939488.shtml
- http://www.read.xwpxi.com/Article/8963.shtml
- http://www.read.xwpxi.com/Article/515162.shtml
- http://www.read.xwpxi.com/Article/668765.shtml
- http://www.read.xwpxi.com/Article/5583684.shtml
- http://www.read.xwpxi.com/Article/9919206.shtml
- http://www.read.xwpxi.com/Article/689131.shtml
- http://www.read.xwpxi.com/Article/0741257.shtml
- http://www.read.xwpxi.com/Article/2426.shtml
- http://www.read.xwpxi.com/Article/49884.shtml
- http://www.read.xwpxi.com/Article/45466.shtml
- http://www.read.xwpxi.com/Article/22470.shtml
- http://www.read.xwpxi.com/Article/80988.shtml
- http://www.read.xwpxi.com/Article/72065.shtml
- http://www.read.xwpxi.com/Article/9868428.shtml
- http://www.read.xwpxi.com/Article/086034.shtml
- http://www.read.xwpxi.com/Article/23373.shtml
- http://www.read.xwpxi.com/Article/23764.shtml
- http://www.read.xwpxi.com/Article/457677.shtml
- http://www.read.xwpxi.com/Article/181914.shtml
- http://www.read.xwpxi.com/Article/5351576.shtml
- http://www.read.xwpxi.com/Article/663576.shtml
- http://www.read.xwpxi.com/Article/75747.shtml
- http://www.read.xwpxi.com/Article/2059.shtml
- http://www.read.xwpxi.com/Article/2037.shtml
- http://www.read.xwpxi.com/Article/200663.shtml
- http://www.read.xwpxi.com/Article/1329.shtml
- http://www.read.xwpxi.com/Article/73921.shtml
- http://www.read.xwpxi.com/Article/589269.shtml
- http://www.read.xwpxi.com/Article/696700.shtml
- http://www.read.xwpxi.com/Article/4282.shtml
- http://www.read.xwpxi.com/Article/2254320.shtml
- http://www.read.xwpxi.com/Article/9261.shtml
- http://www.read.xwpxi.com/Article/919269.shtml
- http://www.read.xwpxi.com/Article/008976.shtml
- http://www.read.xwpxi.com/Article/7949719.shtml
- http://www.read.xwpxi.com/Article/3050.shtml
- http://www.read.xwpxi.com/Article/1080341.shtml
- http://www.read.xwpxi.com/Article/5606034.shtml
- http://www.read.xwpxi.com/Article/2140426.shtml
- http://www.read.xwpxi.com/Article/23380.shtml
- http://www.read.xwpxi.com/Article/95455.shtml
- http://www.read.xwpxi.com/Article/197448.shtml
- http://www.read.xwpxi.com/Article/9044032.shtml
- http://www.read.xwpxi.com/Article/378743.shtml
- http://www.read.xwpxi.com/Article/8625.shtml
- http://www.read.xwpxi.com/Article/404772.shtml
- http://www.read.xwpxi.com/Article/47053.shtml
- http://www.read.xwpxi.com/Article/935286.shtml
- http://www.read.xwpxi.com/Article/2814234.shtml
- http://www.read.xwpxi.com/Article/919709.shtml
- http://www.read.xwpxi.com/Article/9507.shtml
- http://www.read.xwpxi.com/Article/1144394.shtml
- http://www.read.xwpxi.com/Article/144561.shtml
- http://www.read.xwpxi.com/Article/498781.shtml
- http://www.read.xwpxi.com/Article/9922916.shtml
- http://www.read.xwpxi.com/Article/38716.shtml
- http://www.read.xwpxi.com/Article/3399006.shtml
- http://www.read.xwpxi.com/Article/639177.shtml
- http://www.read.xwpxi.com/Article/79033.shtml
- http://www.read.xwpxi.com/Article/1160527.shtml
- http://www.read.xwpxi.com/Article/432024.shtml
- http://www.read.xwpxi.com/Article/6214932.shtml
- http://www.read.xwpxi.com/Article/8541.shtml
- http://www.read.xwpxi.com/Article/613144.shtml
- http://www.read.xwpxi.com/Article/6149.shtml
- http://www.read.xwpxi.com/Article/43207.shtml
- http://www.read.xwpxi.com/Article/49974.shtml
- http://www.read.xwpxi.com/Article/29083.shtml
- http://www.read.xwpxi.com/Article/750964.shtml
- http://www.read.xwpxi.com/Article/5895.shtml
- http://www.read.xwpxi.com/Article/7113273.shtml
- http://www.read.xwpxi.com/Article/376560.shtml
- http://www.read.xwpxi.com/Article/86527.shtml
- http://www.read.xwpxi.com/Article/211169.shtml
- http://www.read.xwpxi.com/Article/68676.shtml
- http://www.read.xwpxi.com/Article/8169.shtml
- http://www.read.xwpxi.com/Article/62574.shtml
- http://www.read.xwpxi.com/Article/21190.shtml
- http://www.read.xwpxi.com/Article/2771.shtml
- http://www.read.xwpxi.com/Article/3770613.shtml
- http://www.read.xwpxi.com/Article/59758.shtml
- http://www.read.xwpxi.com/Article/57417.shtml
- http://www.read.xwpxi.com/Article/2656.shtml
- http://www.read.xwpxi.com/Article/91926.shtml
- http://www.read.xwpxi.com/Article/964309.shtml
- http://www.read.xwpxi.com/Article/300887.shtml
- http://www.read.xwpxi.com/Article/8096806.shtml
- http://www.read.xwpxi.com/Article/9548363.shtml
- http://www.read.xwpxi.com/Article/240223.shtml
- http://www.read.xwpxi.com/Article/7577189.shtml
- http://www.read.xwpxi.com/Article/90003.shtml
- http://www.read.xwpxi.com/Article/1608.shtml
- http://www.read.xwpxi.com/Article/66291.shtml
- http://www.read.xwpxi.com/Article/368439.shtml
- http://www.read.xwpxi.com/Article/447301.shtml
- http://www.read.xwpxi.com/Article/76470.shtml
- http://www.read.xwpxi.com/Article/3617.shtml
- http://www.read.xwpxi.com/Article/21814.shtml
- http://www.read.xwpxi.com/Article/72311.shtml
- http://www.read.xwpxi.com/Article/87768.shtml
- http://www.read.xwpxi.com/Article/27212.shtml
- http://www.read.xwpxi.com/Article/810490.shtml
- http://www.read.xwpxi.com/Article/587849.shtml
- http://www.read.xwpxi.com/Article/84965.shtml
- http://www.read.xwpxi.com/Article/4746.shtml
- http://www.read.xwpxi.com/Article/09223.shtml
- http://www.read.xwpxi.com/Article/7303.shtml
- http://www.read.xwpxi.com/Article/74501.shtml
- http://www.read.xwpxi.com/Article/254170.shtml
- http://www.read.xwpxi.com/Article/770091.shtml
- http://www.read.xwpxi.com/Article/851166.shtml
- http://www.read.xwpxi.com/Article/5708.shtml
- http://www.read.xwpxi.com/Article/9852.shtml
- http://www.read.xwpxi.com/Article/9553110.shtml
- http://www.read.xwpxi.com/Article/10664.shtml
- http://www.read.xwpxi.com/Article/1432672.shtml
- http://www.read.xwpxi.com/Article/0308.shtml
- http://www.read.xwpxi.com/Article/717332.shtml
- http://www.read.xwpxi.com/Article/17210.shtml
- http://www.read.xwpxi.com/Article/7716.shtml
- http://www.read.xwpxi.com/Article/080388.shtml
- http://www.read.xwpxi.com/Article/6346308.shtml
- http://www.read.xwpxi.com/Article/84940.shtml
- http://www.read.xwpxi.com/Article/62915.shtml
- http://www.read.xwpxi.com/Article/4875204.shtml
- http://www.read.xwpxi.com/Article/743326.shtml
- http://www.read.xwpxi.com/Article/700604.shtml
- http://www.read.xwpxi.com/Article/1477739.shtml
- http://www.read.xwpxi.com/Article/9511.shtml
- http://www.read.xwpxi.com/Article/2715428.shtml
- http://www.read.xwpxi.com/Article/9354590.shtml
- http://www.read.xwpxi.com/Article/4367778.shtml
- http://www.read.xwpxi.com/Article/634723.shtml
- http://www.read.xwpxi.com/Article/9967671.shtml
- http://www.read.xwpxi.com/Article/68632.shtml
- http://www.read.xwpxi.com/Article/18778.shtml
- http://www.read.xwpxi.com/Article/02641.shtml
- http://www.read.xwpxi.com/Article/4485.shtml
- http://www.read.xwpxi.com/Article/248425.shtml
- http://www.read.xwpxi.com/Article/9028591.shtml
- http://www.read.xwpxi.com/Article/5011.shtml
- http://www.read.xwpxi.com/Article/79683.shtml
- http://www.read.xwpxi.com/Article/278907.shtml

## 项目结构

```
linkmaster/
├── app/                              # 核心应用目录
│   ├── api/                          # RESTful API 路由层
│   │   ├── v1/                       # API 版本 v1 端点
│   │   │   ├── resources.py          # 资源增删改查接口
│   │   │   ├── tags.py               # 标签管理接口
│   │   │   ├── users.py              # 用户认证与个人信息接口
│   │   │   └── search.py             # 全文检索接口
│   │   └── webhooks.py               # 外部系统回调处理
│   ├── core/                         # 业务逻辑核心层
│   │   ├── crawler/                  # 资源元数据抓取模块
│   │   │   ├── fetcher.py            # 页面标题与摘要提取
│   │   │   └── dedup.py              # URL 指纹计算与去重
│   │   ├── indexer/                  # 全文索引维护模块
│   │   │   ├── fts5.py               # SQLite FTS5 封装
│   │   │   └── elastic.py            # Elasticsearch 适配器
│   │   └── health/                   # 链接健康度检查
│   │       ├── checker.py            # 定时任务与并发检查
│   │       └── notifier.py           # Webhook 与邮件通知
│   ├── models/                       # SQLAlchemy ORM 数据模型
│   │   ├── resource.py               # 资源表结构
│   │   ├── tag.py                    # 标签表与关联表
│   │   └── user.py                   # 用户及收藏表
│   ├── templates/                    # Jinja2 服务端模板
│   │   ├── admin/                    # 管理后台页面
│   │   └── public/                   # 公共首页与资源列表页
│   └── static/                       # CSS / JavaScript / 图片资源
│       ├── css/                      # 基于 Tailwind 的自定义样式
│       └── js/                       # 前端交互逻辑 (Vanilla JS)
├── scripts/                          # 运维与工具脚本
│   ├── init_db.py                    # 数据库初始化和迁移
│   ├── import_batch.py               # 批量导入工具 (支持 CSV / JSON)
│   ├── export_data.py                # 数据导出为多种格式
│   └── health_cron.py                # 健康检查定时任务入口
├── tests/                            # 单元测试与集成测试
│   ├── unit/                         # 细粒度单元测试 (pytest)
│   └── integration/                  # API 端到端测试
├── docs/                             # 完整项目文档 (Markdown)
│   ├── quickstart.md
│   ├── user-guide.md
│   ├── admin-operations.md
│   ├── contributing.md
│   ├── deployment.md
│   └── api-reference.md
├── extensions/                       # 官方扩展插件
│   ├── chrome-extension/             # Chrome 书签同步插件源码
│   └── firefox-extension/            # Firefox 插件源码
├── docker/                           # 容器化配置文件
│   ├── Dockerfile                    # 主应用镜像构建文件
│   └── docker-compose.yml            # 全栈服务编排 (app + redis + es)
├── config/                           # 环境配置
│   ├── development.py                # 开发环境配置
│   ├── production.py                 # 生产环境配置 (敏感信息从环境变量读取)
│   └── testing.py                    # 测试环境配置
├── logs/                             # 日志存储目录 (gitignored)
├── requirements.txt                  # Python 依赖列表
├── setup.py                          # 包安装与分发配置
├── Makefile                          # 常用命令快捷方式 (make install / make test)
├── .env.example                      # 环境变量示例文件
└── README.md                         # 项目主文档 (本文件)
```

## 贡献指南

我们欢迎所有形式的贡献，包括但不限于新功能、Bug 修复、文档改进和插件开发。请遵循以下步骤：

1. 在 GitHub 上 Fork 本仓库，并将 Fork 后的仓库克隆到本地。创建新的功能分支，分支命名格式为 `feature/功能简述` 或 `fix/问题简述`，避免在 master 分支上直接修改。

2. 确保本地 Python 环境和依赖已正确安装，运行 `make test` 确认所有现有测试通过。新增功能需同步编写对应的单元测试和集成测试，测试覆盖率不低于 80%。

3. 提交代码前执行 `make lint` 进行代码风格检查（基于 Black 和 Flake8），并确保所有类型注解完整。提交信息采用 Conventional Commits 规范，例如 `feat: add batch import progress bar` 或 `fix: dedup logic for malformed URLs`。

4. 将分支推送到你的 Fork 仓库，然后在 GitHub 上向本仓库的 master 分支发起 Pull Request。PR 描述需清晰说明改动内容、关联 Issue 编号以及测试结果摘要。

5. 项目维护者将在 48 小时内进行 Code Review，可能要求修改或补充。合并后你的贡献将出现在下一个版本的 Release Notes 中，并列入贡献者名单。

## 常见问题

Q: 系统收录的资源内容是否会存储在本地？
A: 不会。LinkMaster 仅存储资源的 URL、标题、摘要、标签和元数据，不缓存或存储页面正文内容。用户点击资源链接时直接跳转至原始站点，版权归属原发布者所有。如果版权方要求移除某个链接，管理员可通过后台直接删除该条目。

Q: 如何从旧版书签工具迁移到 LinkMaster？
A: 系统提供了通用的导入适配器。你可以将浏览器导出的 HTML 书签文件、Raindrop.io 的 CSV 导出、Pocket 的 JSON 导出等格式，通过 `scripts/import_batch.py --format [html|csv|json] --input 文件路径` 命令一键导入。导入过程中会自动进行去重和标题补全。

Q: 生产环境下如何提高检索性能？
A: 对于超过 5 万条资源的场景，建议切换至 Elasticsearch 作为检索引擎。修改 `.env` 中的 `SEARCH_BACKEND=elasticsearch` 并配置 `ES_HOST` 和 `ES_INDEX` 即可。同时建议启用 Redis 缓存热点查询结果，并在 Nginx 层开启 gzip 压缩以减小响应体积。

## 许可证

MIT License

Copyright (c) 2026 LinkMaster Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 250 | 生成时间: 2026-07-07 00:32:21
