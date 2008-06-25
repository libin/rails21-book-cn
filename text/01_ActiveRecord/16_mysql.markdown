## MySQL中使用Smallint, int还是bigint？
                       
现在在创建或者更改整型列的时候**ActiveRecord**的**MySQL**适配器会处理的更为聪明，它可以根据**:limit**属性确定一个字段的类型应该是**smallint**，**int**还是**bigint**。我们来看个实现上述功能的例子：

  case limit
  when 1; 'tinyint'
  when 2; 'smallint'
  when 3; 'mediumint'
  when 4, nil; 'int(11)'
  else; 'bigint'
  end

现在我们在**migration**中使用它，看看每一个字段应该匹配什么类型：

	create_table :table_name, :force => true do |t|

	  # 2: smallint
	  t.integer :column_one, :limit => 2 # smallint(2)

	  # 4: int(11)
	  t.integer :column_two, :limit => 4 # int(11)

	  # 5 - : bigint
	  t.integer :column_three, :limit => 15 # bigint(15)

	  # if :limit is not informed: int(11)
	  t.integer :column_four # int(11)
	end
      
**PostgreSQL**适配器已经有这个功能了，现在**MySQL**也不甘落后了。