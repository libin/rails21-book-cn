## **sum**方法

### **sum**方法中的表达式

现在我们可以在**ActiveRecord**方法当中使用表达式来处理诸如**sum**等各种计算，如：

	Person.sum("2 * age")

### **sum**方法默认返回值的改变

在之前的版本中，当我们使用**ActiveReocrd**的**sum**方法来计算表中所有记录的和的时候，如果没有跟所需条件匹配的记录的时候，则默认的返回值是**nil** 。在 Rails2.1 中，默认返回值(当没有匹配的记录的时候)是0。如:

	Account.sum(:balance, :conditions => '1 = 2') #=> 0
