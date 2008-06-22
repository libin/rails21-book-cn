## DateTime 类的新方法 (New methodos for DateTime class)

为了保证对 **Time** 类的兼容性（duck-typing），为 **DateTime** 添加了三个新方法，分别为： **#utc** ， **#utc?** 和 **#utc\_offset**，看个例子吧：

	>> date = DateTime.civil(2005, 2, 21, 10, 11, 12, Rational(-6, 24))
	#=> Mon, 21 Feb 2005 10:11:12 -0600

	>> date.utc
	#=> Mon, 21 Feb 2005 16:11:12 +0000

	>> DateTime.civil(2005, 2, 21, 10, 11, 12, Rational(-6, 24)).utc?
	#=> false

	>> DateTime.civil(2005, 2, 21, 10, 11, 12, 0).utc?
	#=> true

	>> DateTime.civil(2005, 2, 21, 10, 11, 12, Rational(-6, 24)).utc_offset
	#=> -21600
