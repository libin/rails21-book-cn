## 小心使用 method\_missing (Used method\_missing, then don't leave loose ends)

由于 Ruby 是动态语言，这样就使得 **respond\_to?** 非常重要，你是否经常检查某个对象是否拥有某个方法？你是否经常使用 **is\_a?** 来检查某个对象正是我们需要的。

然而，人们常常忘记这么做，先看个例子使用 **method\_missing** 的例子吧：

	class Dog
	  def method_missing(method, *args, &block)
	    if method.to_s =~ /^bark/
	      puts "woofwoof!"
	    else
	      super
	    end
	  end
	end

	rex = Dog.new
	rex.bark #=> woofwof!
	rex.bark! #=> woofwoof!
	rex.bark_and_run #=> woofwoof!

我认为你肯定知道 **method\_missing** ，在上面的例子中，我创建了一个 **Dog** 类的实例变量，然后调用三个并不存在的方法 **bark** ， **bark!** 和 **bark\_and\_run**，他就会去调用 **method\_missing** 按照我用正则表达式规定的只要方法是以 **bark** 开头，就输出 woofwoof!。 

没有什么问题，是吧？那么请继续看我使用 **respond\_to?** 来检查下：

	rex.respond_to? :bark #=> false
	rex.bark #=> woofwoof!

看到没有，它返回 false ，也就是说，他认为该对象并没有 bark 方法！怎么办？是时候来按照我们的规则来完善 **respond\_to?** 了。

	class Dog
	  METHOD_BARK = /^bark/

	  def respond_to?(method)
	    return true if method.to_s =~ METHOD_BARK
	    super
	  end

	  def method_missing(method, *args, &block)
	    if method.to_s =~ METHOD_BARK
	      puts "woofwoof!"
	    else
	      super
	    end
	  end
	end

	rex = Dog.new
	rex.respond_to?(:bark) #=> true
	rex.bark #=> woofwoof!

OK，没问题了！这样的问题在 Rails 中普遍存在，你可以试试用 **respond\_to?** 来检查下 **find\_by\_name** 方法就很明白了。 

Ruby 的扩展性能让人称奇，但如果你不注意，会把自己搞得一头雾水。 

当然，你应该猜到我要说什么了，在 Rails 2.1 中，这个问题已经修复了，不信的话，你可以使用 **respond\_to?** 再检测下 **find\_by\_something** 试试看。