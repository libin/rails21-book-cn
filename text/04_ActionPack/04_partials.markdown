## 一种使用 partials 的新方法

在 Rails 开发过程中使用 **partials** 避免重复代码是很正常的方式。例如：

	<% form_for :user, :url => users_path do %>
		<%= render :partial => 'form' %>
		<%= submit_tag 'Create' %>
	<% end %>

**Partial** 是一个代码片断（模板）。使用 **partial** 的是避免不需要的代码重复。使用 **partial** 非常简单，你可以这样开始 **:render :partial => "name"**. 之后，你必须创建一个与你的 **partial** 同名的文件，但使用一个下划线在这之前。 

上面的代码是我们通常的方式，但在新的 Rails 版本中，我们使用不同的方式做相同的事，如：

	<% form_for(@user) do |f| %>
		<%= render :partial => f %>
		<%= submit_tag 'Create' %>
	<% end %>

在这个示例中我们使用了 partias "users/\_form", 将接收到一个名为 "form" 的被 **FormBuilder** 创建的变量。 

以前的方式将继续工作。