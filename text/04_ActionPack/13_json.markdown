## JSON

Rails 现在允许 POST's 一个 JSON 内容的请求，例如，你可以象这样发送一个 POST：

	POST /posts
	{"post": {"title": "Breaking News"}}

所有参数都将到 **params** 中。例如：

	def create
	  @post = Post.create params[:post]
	  # …
	end

为了那些不知道JSON是一个XML竞争者的人，它在JavaScript数据交换中使用相当广泛，因为它呈现为这种语言。它的名字来源于： **JavaScript Object Notation**.