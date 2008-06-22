## Tasks

### rails:update

从 Rails 2.1 开始，每次你运行 **rake rails:freeze:edge** 命令的时候，它将自动运行 **rails:update** 来更新配置文件（config）和 *JavaScripts* 文件。

### Database in 127.0.0.1

databases.rake 以前只操作 local 数据库，现在增加对 IP 为 127.0.0.1 的数据库的操纵。其主要用在创建（**create** ）和删除(**drop**)任务。databases.rake 采取 refactored 避免代码重复。

### 冻结指定的 Rails 版本 (Freezing a specific Rails release）

在 Rails 2.1 之前，你不能在项目组指定一个需要冻结的 Rails 版本库，你只能使用版本信息做为参数；而在 Rails 2.1 后，我们可以在如下的命令中直接指定版本号:

	rake rails:freeze:edge RELEASE=1.2.0

## 时区 (TimeZone)

#### rake time:zones:all

按照 offset 分组返回 Rails 支持的所有时区，你可以使用 OFFSET 参数来过滤返回值，例如：OFFSET=-6

#### rake time:zones:us

显示美国的所有时区，OFFSET 依然有效。

#### rake time:zones:local

返回你本地 OS 上 Rails 支持的时区信息。
