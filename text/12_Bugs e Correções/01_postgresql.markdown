## Add columns in PostgreSQL

在 **PostgreSQL** 中，仍然存在一个 bug。当你对一个已存在的表进行添加 column 的迁移方法。看下面这个例子：

File: *db/migrate/002\_add\_cost.rb*

	class AddCost < ActiveRecord::Migration
	  def self.up
	    add_column :items, :cost, :decimal, :precision => 6, 
	   :scale => 2
	  end

	  def self.down
	    remove_column :items, :cost
	  end
	end

注意我们创建了一个 column cost，**:precision => 6** 和 **:scale => 2** ，现在开始运行 **rake:db:migrate**。下面是我们数据库中的表。

<table border="1" cellspacing="0" cellpadding="5">
	<tr>
		<td><strong>Column</strong></td>
		<td><strong>Type</strong></td>
		<td><strong>Modifiers</strong></td>
	</tr>
	<tr>
		<td>id</td>
		<td>integer</td>
		<td>not null</td>
	</tr>
	<tr>
		<td>desc</td>
		<td>character varying(255)</td>
		<td></td>
	</tr>
	<tr>
		<td>price</td>
		<td>numeric(5,2)</td>
		<td></td>
	</tr>
	<tr>
		<td>cost</td>
		<td>numeric</td>
		<td></td>
	</tr>
</table>

看着 cost 这个我们刚创建的 column 。这是一个常见的数字，但是更加类似于这个 column 类似于 ”price“，基于这个，更精确的描述是 **numeric(6,2)** 。在 Rails 2.1 中，这个错误不会产生，这个 column 将会以正确的方式别创建到数据库中。