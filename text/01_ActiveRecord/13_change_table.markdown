## change\_table
        
在Rails 2.0当中，创建的**migrations**要比之前版本更为性感，不过要想用**migrations**修改一个表可就不那么性感了。

在Rails 2.1中，修改表也由于新方法**change\_table**而变得同样性感了。我们来看个例子：

	change_table :videos do |t|
	  t.timestamps # this adds columns created_at and updated_at
	  t.belongs_to :goat # this adds column goat_id (integer)
	  t.string :name, :email, :limit => 20 # this adds columns name and email
	  t.remove :name, :email # this removes columns name and email
	end
              
新方法**change\_table**的使用就和他的表兄**create\_table**一样，只不过不是创建一个新表，而是通过添加或者删除列或索引来更改现有的表。

	change_table :table do |t|
	  t.column # adds an ordinary column. Ex: t.column(:name, :string)
	  t.index # adds a new index.
	  t.timestamps
	  t.change # changes the column definition. Ex: t.change(:name, :string, :limit => 80)
	  t.change_default # changes the column default value.
	  t.rename # changes the name of the column.
	  t.references
	  t.belongs_to
	  t.string
	  t.text
	  t.integer
	  t.float
	  t.decimal
	  t.datetime
	  t.timestamp
	  t.time
	  t.date
	  t.binary
	  t.boolean
	  t.remove
	  t.remove_references
	  t.remove_belongs_to
	  t.remove_index
	  t.remove_timestamps
	end
