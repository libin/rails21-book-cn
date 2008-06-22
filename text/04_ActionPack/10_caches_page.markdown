## 在 caches\_page method 方法中的条件

**caches\_page** 方法现在支持 **:if** 选择，例如：

	# The Rails 2.0 way
	caches_page :index

	# In Rails 2.1 you can use :if option
	caches_page :index, :if => Proc.new { |c| !c.request.format.json? }
