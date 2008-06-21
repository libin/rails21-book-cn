## MySQL中使用Smallint, int还是bigint？
                       
现在在创建或者更改整型列的时候**ActiveRecord**的**MySQL**适配器会处理的更为聪明，它可以根据**:limit**属性确定一个字段的类型应该是**smallint**，**int**还是**bigint**。我们来看个实现上述功能的例子：

	case limit
	when 0..3
	  "smallint(#{limit})"
	when 4..8
	  "int(#{limit})"
	when 9..20
	  "bigint(#{limit})"
	else
	  'int(11)'
	end

现在我们在**migration**中使用它，看看每一个字段应该匹配什么类型：

	create_table :table_name, :force => true do |t|

	  # 0 - 3: smallint
	  t.integer :column_one, :limit => 2 # smallint(2)

	  # 4 - 8: int
	  t.integer :column_two, :limit => 6 # int(6)

	  # 9 - 20: bigint
	  t.integer :column_three, :limit => 15 # bigint(15)

	  # if :limit is not informed: int(11)
	  t.integer :column_four # int(11)
	end
      
**PostgreSQL**适配器已经有这个功能了，现在**MySQL**也不甘落后了。