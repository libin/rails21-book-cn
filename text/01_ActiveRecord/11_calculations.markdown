## Calculations 
                         
**ActiveRecord::Calculations**做了一些更改以支持数据库表名。这个功能在几个不同表之间存在关联且相关列名相同时会非常有用。我们有两个选项可选：

	authors.categories.maximum(:id)
	authors.categories.maximum("categories.id")
