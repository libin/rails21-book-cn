## action\_name

现在，要知道在运行时哪一个 view 被调用， 我们只需要使用 **action\_name** 方法：

	<%= action_name %>

返回值将和使用 **params[:action]** 一样，但更优雅。
