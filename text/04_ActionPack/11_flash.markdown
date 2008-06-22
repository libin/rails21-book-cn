## flash.now 现在可以在 tests 中工作

谁没有这因为这而头痛过？这个问题在我们测试期间，无法确定信息已经存储到了 Flash 中，因为它在到你的测试代码之前就被 Rails 清除了。 

在 Rails 2.1中这个问题已经被解决。现在你可以包含下面的代码行在你的测试中：

	assert_equal '>value_now<', flash['test_now']
