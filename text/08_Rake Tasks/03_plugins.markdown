## 插件 (Plugins)

### Gems可插件化 (Gems can now be plugins)

现在，任何包含 **rails/init.rb** 文件的 gem 都可以以插件的方式安装在 **vendor** 目录。

### 使用插件中的生成器 (Using generators in plugins)

可以配置 **Rails** 使得其在除了 **vendor/plugins** 之外的地方加载插件，配置方法为在 *environment.rb* 中添加如下代码:

	config.plugin_paths = ['lib/plugins', 'vendor/plugins']
	
Rails 2.0 中这个地方存在一个 Bug，该 Bug 是其只在 **vendor/plugins** 中寻找有生成器的插件，而其上配置的路径下的插件的生成器并不生效。在 Rails 2.1 中已经修复。