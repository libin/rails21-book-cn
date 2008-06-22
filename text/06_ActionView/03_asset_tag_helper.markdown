## ActionView::Helpers::AssetTagHelper

### register\_javascript\_expansion

当一个被程序员定义的符号作为一个参数，赋值给 **javascript\_include\_tag** 这个方法。 register_javascript_expansion 方法用来注册一个或者多个 javascript 文件被引用。这个是在 **init.rb** 中调用你的方法，将位于文件夹 **public/javascript** 下面的 javascript 文件注册进来。让我们看看它是如何进行工作的：

	# In the init.rb file
	ActionView::Helpers::AssetTagHelper.register_javascript_expansion 
		:monkey => ["head", "body", "tail"] 

	# In our view:
	javascript_include_tag :monkey

	# We are going to have:
	<script type="text/javascript" src="/javascripts/head.js"></script>
	<script type="text/javascript" src="/javascripts/body.js"></script>
	<script type="text/javascript" src="/javascripts/tail.js"></script>


### register\_stylesheet\_expansion

这个方法实际上类似于 **ActionView::Helpers::AssetTagHelper#register\_javascript\_expansion** 方法。不同的是它针对的是 CSS 而不是 Javascript。 看下面的例子：

	# In the init.rb file
	ActionView::Helpers::AssetTagHelper.register_stylesheet_expansion 
		:monkey => ["head", "body", "tail"] 

	# In our view:
	stylesheet_link_tag :monkey

	# We are going to have:
	<link href="/stylesheets/head.css"  media="screen" rel="stylesheet" 
		type="text/css" />
	<link href="/stylesheets/body.css"  media="screen" rel="stylesheet" 
		type="text/css" />
	<link href="/stylesheets/tail.css"  media="screen" rel="stylesheet" 
		type="text/css" />