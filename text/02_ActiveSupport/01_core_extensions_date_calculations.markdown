## ActiveSupport::CoreExtensions::Date::Calculations

### Time#end\_of\_day

返回当日结束时间 11:59:59 PM.

### Time#end\_of\_week

返回周末时间 (Sunday 11:59:59 PM).

### Time#end\_of\_quarter

返回一个 Date 对象，代表本季度最后一天。换句话说，它根据当前日期返回三月，六月，九月或者十二月的最后一天。

### Time#end\_of\_year

返回十二月31日 11:59:59 PM

### Time#in\_time\_zone

本方法类似于 **Time#localtime**, 除了它使用 **Time.zone** 而不是底层操作系统的时区。你可以传入 **TimeZone** 或者 **String** 作为参数。看下面的例子:

	Time.zone = 'Hawaii'
	Time.utc(2000).in_time_zone
	# => Fri, 31 Dec 1999 14:00:00 HST -10:00

	Time.utc(2000).in_time_zone('Alaska')
	# => Fri, 31 Dec 1999 15:00:00 AKST -09:00

### Time#days\_in\_month

方法 **days\_in\_month** 中的一个 bug 被修正了, 当没有指定年的时候，对于2月它返回错误的天数。 

这个改变使得在没有指定年的情况下，当前年在方法调用的作为默认值。假设你处于闰年，看下面的例子：

	Loading development environment (Rails 2.0.2)
	>> Time.days_in_month(2)
	=> 28

	Loading development environment (Rails 2.1.0)
	>> Time.days_in_month(2)
	=> 29

### DateTime#to_f

**DateTime** 类得到了一个新的方法名为 **to_f**，它把日期以浮点数的形式返回。这个浮点数代表从 Unix 纪元（1970,1月1日午夜)开始的秒数。

### Date.current

**Date**Date 类得到了一个新方法名为 **current** 来代替 **Date.today**, 因为它考虑到 **config.time\_zone** 中设置的时区，如果它设置了, 返回 **Time.zone.today**. 如果没有设置, 它返回**Date.today**。