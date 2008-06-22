## Mime Types

不允许定义分配过的属性 **request.format** 使用符号的 bug 已经被解决了。现在你可以使用下面的代码：

	request.format = :iphone
	assert_equal :iphone, request.format
