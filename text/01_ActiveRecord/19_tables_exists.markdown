##table_exists?方法
           
**AbstractAdapter**类有个新方法**table\_exists**，用法非常简单：

	>> ActiveRecord::Base.connection.table_exists?("users")
	=> true
