## Labels

当使用 **scaffold** 生成一个新表单时，它将创建下面的代码：

	<% form_for(@post) do |f| %>
	  <p>
	    <%= f.label :title %><br />
	    <%= f.text_field :title %>
	  </p>
	  <p>
	    <%= f.label :body %><br />
	    <%= f.text_area :body %>
	  </p>
	  <p>
	    <%= f.submit "Update" %>
	  </p>
	<% end %>

这种方式更有意义，它包含了 **label** 方法。该方法在HTML标签中返回一个标题列。

	>> f.label :title
	=> <label for="post_title">Title</label>

	>> f.label :title, "A short title"
	=> <label for="post_title">A short title</label>

	>> label :title, "A short title", :class => "title_label"
	=> <label for="post_title" class="title_label">A short title</label>

你在标签中注意了 **for** 参数吗？ "post\_title" 是包含了我们的 post tile 的文本框。这个<label>标签实际是一个关联到 *post\_title** 对象。当有人点击这个 label（非链接） 时，被关联的控件接收到焦点。 

Robby Russell 在他的Blog中写了一个有趣的关于这个主题的文章。你可以从这里阅读： 
[http://www.robbyonrails.com/articles/2007/12/02/that-checkbox-needs-a-label](http://www.robbyonrails.com/articles/2007/12/02/that-checkbox-needs-a-label)

在 **FormTagHelper** 中同样也拥有 **label\_tag** 方法。该方法的工作方式和 label 一样，但更简单：

	>> label_tag 'name'
	=> <label for="name">Name</label> 

	>> label_tag 'name', 'Your name'
	=> <label for="name">Your name</label> 

	>> label_tag 'name', nil, :class => 'small_label'
	=> <label for="name" class="small_label">Name</label>

该方法同样接收 **:for** 选项，看一个示例：

	label(:post, :title, nil, :for => "my_for")

这将返回这样的结果：

	<label for="my_for">Title</label>
