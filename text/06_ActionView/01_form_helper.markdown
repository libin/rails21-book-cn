## ActionView::Helpers::FormHelper

### fields\_for form\_for with index option.

**#fields\_for** 和 **form\_for** 方法接受 **:index** 选项，在 form 对象中，如果需要去掉就必须使用 **:index => nil**。

下面是示例代码：

	<% fields_for "project[task_attributes][]", task do |f| %>
	  <%= f.text_field :name, :index => nil %>
	  <%= f.hidden_field :id, :index => nil %>
	  <%= f.hidden_field :should_destroy, :index => nil %>
	<% end %>

紧随的是新的方法：

	<% fields_for "project[task_attributes][]", task,
	              :index => nil do |f| %>
	  <%= f.text_field :name %>
	  <%= f.hidden_field :id %>
	  <%= f.hidden_field :should_destroy %>
	<% end %>