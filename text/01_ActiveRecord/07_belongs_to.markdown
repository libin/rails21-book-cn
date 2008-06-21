## Belongs_to

为了能在关联中使用**:dependent=>:destroy**和**:delete**, **belongs\_to**方法做了一些更改，比如：

	belongs_to :author_address
	belongs_to :author_address, :dependent => :destroy
	belongs_to :author_address_extra, :dependent => :delete, 
		:class_name => "AuthorAddress"
