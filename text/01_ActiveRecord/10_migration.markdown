## add\_timestamps和remove\_timestamps方法     
  
现在我们有两个新的方法**add\_timestamps**和**remove\_timestamps**，他们分别添加，删除**timestamp**列。看个例子：

	def self.up
	  add_timestamps :feeds
	  add_timestamps :urls
	end

	def self.down
	  remove_timestamps :urls
	  remove_timestamps :feeds
	end
