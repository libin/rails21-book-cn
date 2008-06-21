## ActiveRecord::Base.create接受blocks

我们已经习惯了**ActiveRecord::Base.new**接受block作为参数了，现在**create**也同样接受blocks了：

	# Creating an object and passing it a block describing its attributes
	User.create(:first_name => 'Jamie') do |u|
	  u.is_admin = false
	end

我们也能用同样的方法一次创建多个对象：

	# Creating an array of new objects using a block.
	# The block is executed once for each of object that is created.
	User.create([{:first_name => 'Jamie'}, {:first_name => 'Jeremy'}]) do |u|
	  u.is_admin = false
	end

同样在关联当中可以使用：

	author.posts.create!(:title => "New on Edge") {|p| p.body = "More cool stuff!"}

	# or

	author.posts.create!(:title => "New on Edge") do |p|
	  p.body = "More cool stuff!"
	end
