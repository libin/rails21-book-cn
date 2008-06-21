## 只读关联 (Readonly relationships)

一个新的功能被添加到了models之间的关联当中。为了避免更改关联模型的状态，你现在可以使用**:readonly**来描述一个关联。我们看几个例子：

	has_many :reports, :readonly => true

	has_one :boss, :readonly => :true

	belongs_to :project, :readonly => true

	has_and_belongs_to_many :categories, :readonly => true
	      
这样，关联的models就能够避免在model中被更改，如果试图更改他们，那么将得到一个**ActiveRecord::ReadOnlyRecord**异常