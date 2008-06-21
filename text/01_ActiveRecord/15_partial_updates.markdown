## Partial Updates

**Dirty Objects**的实现让另一个非常有趣的功能变为可能。 

由于我们现在可以跟踪一个对象的状态是否发生改变，那么为什么不用它来避免那些不必要的对数据裤的更新呢？ 

在之前版本的Rails当中，当我们对一个已经存在的**ActiveRecord**对象调用**save**方法的时候，所有数据库中的字段都会被更新，即使那些没有做任何更改的字段。 

这种方式在使用了Dirty Objects以后应该会有很大的改进，而实际情况也的确如此。看看在保存一个有一点更改的对象时，Rails 2.1生成的SQL查询语句：

	article = Article.find(:first)
	article.title  #=> "Title"
	article.subject  #=> "Edge Rails"

	# Let's change the title
	article.title = "New Title"

	# it creates the following SQL
	article.save
	#=>  "UPDATE articles SET title = 'New Title' WHERE id = 1"
	
注意到，只有那些在应用中被更改的属性才在被更新。如果没有属性被更改，那么**ActiveRecord**就不执行任何更新语句。 

为了开启/关闭这个新功能，你要更改model的**partial\_updates**属性。

	# To enable it
	MyClass.partial_updates = true
         
如果希望对所有的models开启/关闭这个功能，那么你必须编辑*config/initializers/new\_rails\_defaults.rb*：

	# Enable it to all models
	ActiveRecord::Base.partial_updates = true
      
别忘了如果你不通过attr=更改字段，同样要通过*config/initializers/new\_rails\_defaults.rb*来通知Rails，像这样:

	# If you use **attr=**, 
	# then it's ok not informing
	person.name = 'bobby'
	person.name_change    # => ['bob', 'bobby']
	
	
	# But you must inform that the field will be changed
	# if you plan not to use **attr=** 
	person.name_will_change!
	person.name << 'by'
	person.name_change    # => ['bob', 'bobby']
         
如果你不通知Rails，那么上述的代码同样会更改对象的属性，但是却不能被跟踪到，从而也就无法正确的更新数据库中的相应字段。