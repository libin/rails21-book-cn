## Increment 和 decrement

**ActiveRecord**的方法**increment**,**increment!**,**decrement**和**decrement!**现在支持一个新的可选参数。之前版本的Rails中你可以通过这些方法指定的属性值加1或减1。在Rails 2.1中，你可以指定要增加或者减少的值，像这样：

	player1.increment!(:points, 5)
	player2.decrement!(:points, 2)
                                      
上边的例子中，我向player1加了5分，从player2减了2分。由于这是一个可选的参数，所以之前的代码不会受到影响。