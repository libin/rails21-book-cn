## Polymorphic url

一些多态URL的辅助方法也被引入到新的Rails当中，用来提供一种更为简洁优雅的操作routes的方式。 

这些方法在你想生成基于**RESTful**资源的URL，同时又不必显示指定资源的类型的时候，会现得十分有用。

使用方面，非常的简单，来看看一些例子（注释的部分是Rails 2.1之前的做法）                         

	record = Article.find(:first) 
	polymorphic_url(record) #-> article_url(record)

	record = Comment.find(:first)
	polymorphic_url(record)  #->  comment_url(record)

	# it can also identify recently created elements
	record = Comment.new
	polymorphic_url(record)  #->  comments_url()
	                  
注意到**polymorphic_url**方法是如何确认传入参数的类型并且生成正确的routes。内嵌资源（**Nested resources**）和**namespaces**也同样支持：

	polymorphic_url([:admin, @article, @comment])
	#-> this will return:
	admin_article_comment_url(@article, @comment)
	           
你同样能够使用**new**, **edit**, **formatted**等前缀。看看下边的例子：

	edit_polymorphic_path(@post)
	#=> /posts/1/edit

	formatted_polymorphic_path([@post, :pdf])
	#=> /posts/1.pdf
