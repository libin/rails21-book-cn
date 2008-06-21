## Dirty Objects
                  
在新Rails当中，我们同样可以跟踪对**ActiveRecord**所做的更改。我们能够知道是否一个对象被进行了修改，如果有更改，那么我们就能跟踪到最新的更改。我们来看几个例子：

  article = Article.find(:first)
	article.changed?  #=> false

	article.title  #=> "Title"
	article.title = "New Title"
	article.title_changed? #=> true

	# shows title before change
	article.title_was  #=> "Title"

	# before and after the change
	article.title_change  #=> ["Title", "New Title"]

可以看到，使用上边非常的简单，同时你也能够通过下列两种方法的任意一种列出对一个对象的所有更改：

	# returns a list with all of the attributes that were changed
	article.changed  #=> ['title']

	# returns a hash with attributes that were changed 
	# along with its values before and after
	article.changes  #=> { 'title’ => ["Title", "New Title"] }
             
注意到当一个对象被保存后，他的状态也随之改变：

	article.changed?  #=> true
	article.save  #=> true
	article.changed?  #=> false
   
如果你不通过**attr=**来更改一个对象的状态，那么你需要显示的调用**attr\_name\_will\_change!**方法(用对象的实际属性名称替换**attr**)来通知属性已经被更改。我们再看最后一个例子：
    
	article = Article.find(:first)
	article.title_will_change!
	article.title.upcase!
	article.title_change  #=> ['Title', 'TITLE']
