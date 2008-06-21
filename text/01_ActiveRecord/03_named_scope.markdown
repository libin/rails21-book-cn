## Named_scope

*has\_finder* gem已经添加到Rails当中了，有一个新名字**:named_scope**。

为了全面了解一下这为Rails带来了什么，我们看看下边的例子：

	class Article < ActiveRecord::Base
	  named_scope :published, :conditions => {:published => true}
	  named_scope :containing_the_letter_a, :conditions => "body LIKE '%a%’"
	end 

	Article.published.paginate(:page => 1)
	Article.published.containing_the_letter_a.count
	Article.containing_the_letter_a.find(:first)
	Article.containing_the_letter_a.find(:all, :conditions => {…})
 
通常我会创建一个新的叫做**published**的方法来返回所有的已经发布的帖子，不过在这里我是用了**named\_scope**来做同样的事情，而且还能得到其他的效果。看看另一个例子：

	named_scope :written_before, lambda { |time|
	  { :conditions => ['written_on < ?', time] }
	}

	named_scope :anonymous_extension do
	  def one
	    1
	  end
	end

	named_scope :named_extension, :extend => NamedExtension 

	named_scope :multiple_extensions, 
		:extend => [MultipleExtensionTwo, MultipleExtensionOne]

## 用proxy\_options来测试named\_scope
                                                                                 
**Named scopes**是Rails 2.1中很有趣的新功能，不过使用一段时间以后你就会发现想创建一些复杂情况的测试会有点麻烦，看个例子：

		class Shirt < ActiveRecord::Base
		  named_scope :colored, lambda { |color|
		    { :conditions => { :color => color } }
		  }
		end

如何创建一个能测试scope结果的测试呢？

为了解决这个问题，**proxy\_options**被创建了出来。它允许我们来检测**named_scope**使用的选项。为了测试上述代码，我们可以这样写测试：

		class ShirtTest < Test::Unit
		  def test_colored_scope
		    red_scope = { :conditions => { :colored => 'red' } }
		    blue_scope = { :conditions => { :colored => 'blue' } }
		    assert_equal red_scope, Shirt.colored('red').scope_options
		    assert_equal blue_scope, Shirt.colored('blue').scope_options
		  end
		end
