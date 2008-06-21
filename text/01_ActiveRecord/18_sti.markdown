## 使用单表继承(STI)的时候存储类的全名

当我们的**models**有**namespace**，并且是单表继承(STI)的时候，**ActiveRecord**仅仅将类名，而不是包括n**amespace**(**demodulized**)在内的全名存起来。这种情况仅仅当单表继承的所有类在一个**namespace**的时候有效，看个例子：

	class CollectionItem < ActiveRecord::Base; end
	class ComicCollection::Item < CollectionItem; end

	item = ComicCollection::Item.new
	item.type # => 'Item’

	item2 = CollectionItem.find(item.id)
	# returns an error, because it can't find
	# the class Item
      
新的Rails添加了一个属性，从而使**ActiveRecord**能存储类的全名。 
可以在**environment.rb**当中添加如下代码来启动/关闭这个功能：

	ActiveRecord::Base.store_full_sti_class = true
                             
默认值是true。