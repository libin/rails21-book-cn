## 获取一个插件的相关信息 （Getting information about a plugin）

Rails 2.0 的新特性之一，或许你从未用过。我是说“大概，或许”，可能在一些比较特殊情况下会有用，举个例子，比如获知一个插件的版本号。 

不妨来尝试下，我们要在 plugin 目录里面新建一个 *about.yml* 文件，写入如下一些内容：

	author: Carlos Brando
	version: 1.2.0
	description: A description about the plugin
	url: http://www.nomedojogo.com

然后我们可以使用如下方式来获取相关信息：

	plugin = Rails::Plugin.new(plugin_directory)
	plugin.about["author"] # => “Carlos Brando”
	plugin.about["url"] # => “http://www.nomedojogo.com”

如果你能在这个新特性中找到一些好的用处并愿与我分享，也许将改变我对于它的一些看法若真有需要的话。
