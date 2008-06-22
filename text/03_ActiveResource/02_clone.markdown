## clone 方法

现在我们可以复制已有的resource：

	ryan = Person.find(1)
	not_ryan = ryan.clone
	not_ryan.new?  # => true

要注意复制出来的对象并不复制任何类属性，而是仅复制resource属性。

	ryan = Person.find(1)
	ryan.address = StreetAddress.find(1, :person_id => ryan.id)
	ryan.hash = {:not => "an ARes instance"} 

	not_ryan = ryan.clone
	not_ryan.new?            # => true
	not_ryan.address         # => NoMethodError
	not_ryan.hash            # => {:not => "an ARes instance"}