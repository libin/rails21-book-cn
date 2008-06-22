## 定义你的 routes 文件地址

在 Rails 2.1你可以定义你的 routes 存在哪一个文件中，包含以下行在你的 *environment.rb* 文件中：

	config.routes_configuration_file

这将有用于当你拥有两种分开的前端共享相同models时，libraries 和 plugins。

例如，getsatisfaction.com 和 api.getsatisfaction.com 共用相同的 models, 但使用不同的 controllers, helpers 和 views.getsatisfaction 拥有它自己针对 SEO 优化的 routes 文件，但 API routes 不需要任何关于 SEO 的优化。