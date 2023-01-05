# GCC #3

## 社区发展

### 社区模块

#### 元数据

##### 声明

- “基于 `importlib.metadata` 的读取”

    理想状态下，直接 `ModuleMetadata.from_package("graiax-xxx")` 即可

- “用户直接声明”

    通过支持 `__or__` (或者别的运算符) 来实现方便的元数据覆盖/增强

##### 类别

模块本身的元数据（`pyproject.toml` 已覆盖的部分）

额外元数据（`frameworks` `config_endpoints` `standards` `component_endpoints` etc.）

- `standards`

    - `GraiaCommunity/Standard`
    - `ProjectNull/EricMeta`
    - `sagiri-kawaii/SagiriMeta`

第三方扩展元数据：extra KV pairs

可能的：元数据标准验证器？

#### 发布

GraiaCommunity/Pubdash

基于 Github Action 的中心化 Publish Bot

下载 wheel 后分析 metadata, 之后上传到中心仓库并同步至前端

中心仓库使用 GHA 定时更新元数据

### Luma

#### Runtime 生命周期

- 先籍由已有的 `luma.toml` 知道一些信息, 比如 kayaku configure endpoints.
    ```toml
    [config]
    endpoints = [
        {...} # 单纯的键值对.
    ]
    [[modules]]  # luma 最先能读到的是这里.
    type = "local"
    endpoint = "stellaium.order_std.ping"
    [[modules]]
    type = "pypi"
    name = "stellaium-ping-mcserver"
    # 这样大概就行了.
    
    ```
- 根据 `config.endpoints` 初始化 Kayaku.
- 加载 `luma.toml` 中声明的 Saya 模块，同时获取对应的 metadata （加载 `module.file.parent / "module.jsonc"` 并映射到 `channel.meta`）
- 加载框架主体 (Ariadne / Avilla): luma.framework.[avilla/ariadne]
- Scheduler / Starlette / Playwright 等前置组件的初始化. 直接运行对应逻辑即可（思考：metadata entry-point？）
    ```toml
    [entry_points."luma-thirdparty"] # Package side
    graia-scheduler = "graia.scheduler.luma.loader"
    graiax-playwright = "graiax.playwright.luma.loader"
    ```

    `graia.scheduler.luma.loader(luma: Luma, toml_config_dict: ConfTypedDict) -> None`

    ```toml
    # User side
    [[tool.luma.components]]
    name = "graia-scheduler"

    [[tool.luma.components]]
    name = "graiax-playwright"
    browser = "firefox"

    [[tool.luma.components]]
    name = "graia-amnesia"
    sub_component = "uvicorn" # TBD
    port = 8080
    ```
- 加载 Saya 模块内声明的 Launart 组件
- 启动 Launart

### 社区 Bot

先官方写几个插件, 类似 koishi 那样, 也起一个示范引导作用.
从 Bot 内抽取无耦合模块进行发布应该也是可行的