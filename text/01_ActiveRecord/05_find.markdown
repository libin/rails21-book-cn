## Find

### Conditions
            
从现在开始，你可以向**ActiveRecord**的**find**方法中传一个对象作为参数。看下边的例子：

	class Account < ActiveRecord::Base
	  composed_of :balance, :class_name => "Money", :mapping => %w(balance amount)
	end

这个例子中，你能向**Account**类的**find**方法中传入一个**Money**实例作为参数，像这样：         

	amount = 500
	currency = "USD"
	Account.find(:all, :conditions => { :balance => Money.new(amount, currency) })
	
### Last

到现在为止我们只能在**ActiveRecord**的**find**方法中使用三个操作符来查找数据，他们是**:first**,**:all**和对象自己的id(这种强况下，我们除了id以外不再传入其他的参数)。

在Rails 2.1当中，有了第四个操作符**:last**，几个例子： 

	Person.find(:last)
	Person.find(:last, :conditions => [ "user_name = ?", user_name])
	Person.find(:last, :order => "created_on DESC", :offset => 5)
	                                                             
为了能明白这个新的操作符如何工作，我们看看下边的测试：

	def test_find_last
	  last  = Developer.find :last
	  assert_equal last, Developer.find(:first, :order => 'id desc')
	end
	
### All

类方法**all**是另一个类方法**find(:all)**的别名。如：
	
	Topic.all is the same as Topic.find(:all)

### First
              
类方法**first**是另一个类方法**find(:first)**的别名。如：

	Topic.first is the same as Topic.find(:first)

### Last

类方法**last**是另一个类方法**find(:last)**的别名。如：

	Topic.last is the same as Topic.find(:last)

             
## 在**named\_scope**中使用**first**和**last**方法

所有上述的方法同样适用于**named\_scope**。比如我们创建一个叫**recnet**的**named\_scope**，下列代码是有效的： 

		post.comments.recent.last
