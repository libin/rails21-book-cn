## 简单的 Testing Helpers

Rails 早期版本的确 **helpers** 是一个非常烦人的事。我早已经非常痛苦的保证 100% 覆盖，创建 tests 为一些 **helpers**. 

由于 **ActionView::TestCase** 类，在 Rails 2.1中这变得简单得多了。看个示例：

	module PeopleHelper
	  def title(text)
	    content_tag(:h1, text)
	  end

	  def homepage_path
	    people_path
	  end
	end

现在看我们在 Rails2.1中怎样做同样的事：

	class PeopleHelperTest < ActionView::TestCase
	  def setup
	    ActionController::Routing::Routes.draw do |map|
	      map.people 'people', :controller => 'people', :action => 'index'
	      map.connect ':controller/:action/:id'
	    end
	  end

	  def test_title
	    assert_equal "<h1>Ruby on Rails</h1>", title("Ruby on Rails")
	  end

	  def test_homepage_path
	    assert_equal "/people", homepage_path
	  end
	end
