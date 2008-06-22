## config.gem

新特性 **config.gem** 使项目在运行时加载所有必需的 gems 成为可能。在 *environment.rb* 文件里可以指定你项目依赖的gems。如下示例：

	config.gem "bj" 

	config.gem "hpricot", :version => '0.6',
	                      :source => "http://code.whytheluckystiff.net" 

	config.gem "aws-s3", :lib => "aws/s3"

要一次性安装所有的 gem 依赖，我们只需运行如下一个 Rake 任务：

	# Installs all specified gems
	rake gems:install

你也可以在项目运行时列出正在被使用的 gems：

	# Listing all gem dependencies
	rake gems

如果其中有个gem含有文件 **rails/init.rb** 并且你想将它存放在你的项目中，可以用：

	# Copy the specified gem to vendor/gems/nome_do_gem-x.x.x
	rake gems:unpack GEM=gem_name

这将会拷贝这个 gem 到 **vendor/gems/gem\_name-x.x.x**。若不指定 gem 的名称， Rails 将拷贝所有 gems 包到 **vendor/gem** 目录中.

## 在插件里配置 gem (config.gem in plugins)

新特性 **config.gem** 也同样适合在插件中使用。

一直到 Rails 2.0插件里边的 **init.rb** 文件都是按如下方式使用：

	# init.rb of plugin open_id_authentication
	require 'yadis' 
	require 'openid' 
	ActionController::Base.send :include, OpenIdAuthentication 

而在 Rails 2.1中则是这样：

	config.gem "ruby-openid", :lib => "openid", :version => "1.1.4"
	config.gem "ruby-yadis",  :lib => "yadis",  :version => "0.3.4" 

	config.after_initialize do
	  ActionController::Base.send :include, OpenIdAuthentication
	end

那么，当你运行该任务来安装所需要的 gems 时，这些 gems 将在包含之中。
