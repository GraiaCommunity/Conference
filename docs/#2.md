# GCC #2

## Ariadne 相关

### Provider Support

`Ariadne.construct` 之类的类方法注入配置

### Ariadne.create

Create Spec:

Broadcast.param_compile?

#### "Ensurable" 


### CoolDown

利用 `amnesia` 的 `CacheStorage` 实现作为后端

更多的控制？s

### Message Parser/Matcher 相关



## 社区发展

### graiax-cli

将 pypi 作为资源基建，将 cli 作为社区资源的集中点

### 社区管理

"Editor's Choice" 和 "upvote" "downvote"

### Provider

填充字段至全局字典，通过描述器声明字段与默认值。

利用 `chainmap` 提供 Layer，避免字段污染:

```json5
a = {"a": "a_value"}
b = {"a": "b_value"}

a | b == {"a": "?"} # 未定义行为!
```

基于上下文的值推断 (利用 `tag`)

```json5
a = {"key": "a_value"}
a_tag = {
    "env": "a"
}

b = ...
b_tag = ...

access("key", env="a") == "a_value"
```

## Mina

处理 “插件” 和基础设施共享相关的发布.

## Launart + Saya

Launart 为 Ariadne 0.7.0 的底层库, 是生命周期管理工具.

Launart 已经对 Saya 编写了支持, 你们可以通过 Saya 获得 Launart 的完整生命周期,
最重要的, 是 Service 和 ExportInterface

Launart 支持热插拔

Example:

热注册，热注销的数据库接口

热重载

“跨框架加载”

Q：两个 "http.universal_client"

A: 优先级策略（PriorityType）

e.g.:

{AbstractHttp: <通用的部分>}

{Awesome1: <牛逼特性_1号>}

...

{AbstractHttp: <性能好就哪个优先级高>, Awesome1: <性能好的, 当然如果没有其他的就只能选有这个的>}

```py
interface_supported_types = {Interface1: 1, Feature1: 3, ...}
```

### Launart.current 相关

- Saya.current

- Channel.current

- Ariadne.current

- Launart.current?

## Avilla

架构设计完成，进入内容填充阶段

仍需对平台间通用字段进行抽象


## I18N / L10N

graia-i18n

