# Graia Community Conference #1 Record

# Graia 社区会议 #1

## Part 1. Ariadne 开发动态

### 0.6.0

1.  Twilight 构造方式大改

2.  Commander 性能提升

## Part 2. Graiax-CLI

1.  init / new 初始化，承担脚手架功能

2.  util 连接，提供 toml load 一类功能

3.  struct update 向主文件添加 saya 等初始化

## Part 3. Avilla Intro

定位：

1.  框架上的框架：抽象通用部分（MessageChain，Event，Execution......）

2.  不定于平台的实现

3.  便民结构：基于Basic Avilla Protocol逻辑即可零成本迁移

内部结构：

1.  Relationship: 将 Group Friend Guild Self 等抽象为 Relationship (mainline)

    对“关系”进行操作（create, destory）通过关系进行操作

2.  Protocol: 平台对接的实现（已实现：OneBot）（画饼：Mirai API HTTP，Discord，Telegram，......）\
    承担消息链序列化等任务，引导开发者对 Avilla 进行更好的适配，实现更好的平台兼容性

3.  Selector: 选择器，通过唯一的 API （dict）通过作用域进行对特定对象的单一选择

    内建作用域（Entity对象，Mainline对象作用域，Resource资源），类型推导支持&#x20;

4.  Config，Permission，Service，Utility

Service：

1.  通过维护特定资源，降低耦合，提高通用性（HttpClient, Server.......) (avilla.io)

2.  向外部提供操作：aiohttp获取HttpClient与WebsocketClient，内置的缓存服务：MemCache by Bryan，RedisCache

    ASGI：uvicorn

3.  调用其他服务的接口进行封装使接口简洁：调用其他Service，Avilla进行以来解析

Config：内置的配置系统：

*   Applicant 申请者

*   Scope 作用域

*   Content 模型/内容

*   泛型支持

Config Provider:

*   来自已配置实例

*   配置文件的配置 （推荐 hocon）

*   来自数据库的配置

*   解析字段声明生成样例文件（包括注释/字段描述）

Permission: 权限系统 ~~（暂时是饼）~~

*   已经实现抽象接口

*   类似于 BroadcastControl oplog 的 智能缓存

*   可切换的数据库后端

*   ~~足够快~~

Relationship 内部相关操作

*   没有基于实例的调用了，通过 MessageSend 一类的 Action 执行相应操作

*   统一模型数据为实体元信息（`rs.meta` ：类似于示例）

*   `rs.meta` 操作：`get` `set` `remove` 等，例如 `await rs.meta.get('member.name')` （内部有缓存）

*   在平台间提供较好的兼容性

### Part 4. 自由讨论 (Q & A)

Q：Saya 是否有接下来的更新计划？

A：大部分扔到 Avilla Launch API 之类的了。长期可以有 Saya CLI（辅助插件开发，自动配置 Behaviour 等）。

Q：Application 的 issue 什么时候统一处理掉？

A：还有这事吗？

Q：Avilla 多账号多平台处理？（Chat Bridge 需求）

A：Relatonship 指向特定账号选择器，Mainline 获取实例等，进行操作检查（权限，频道，平台......）

Q：参加 Avilla 开发有什么门槛吗？（

A：~~没有~~，快来加入 GraiaProject（前提是可以看懂魔女的 ~~魔法~~
