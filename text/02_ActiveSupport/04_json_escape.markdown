## JSON escape

**json\_escape** 方法行为类似 **html\_escape**。在我们想要在 **HTML** 页面中显示 **JSON** 字符串的时候非常有用。例如，在一个文档处理中：

	puts json_escape("is a > 0 & a < 10?")
	# => is a \u003E 0 \u0026 a \u003C 10?

我们也能使用简写 **j** 在 ERB 中：

	<%= j @person.to_json %>

如果你想所有的 **JSON** 代码默认都被 'escaped', 在你的 *environment.rb* 文件中包含下面的代码：

	ActiveSupport.escape_html_entities_in_json = true
