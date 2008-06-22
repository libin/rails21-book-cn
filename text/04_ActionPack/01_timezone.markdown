## TimeZone

### 定义一个默认的时区

一个新的选项被加入到 **time\_zone\_select** 方法，在你的用户没有选择任何 **TimeZone** 的时候，或当数据库字段为空时，你现在可以显示一个默认值。它已经创建了一个 **:default** 选项，你可以按照下面的方式使用这个方法：

	time_zone_select("user", "time_zone", nil, :include_blank => true)
	
	time_zone_select("user", "time_zone", nil, 
		:default => "Pacific Time (US & Canada)" )
	
	time_zone_select( "user", 'time_zone', TimeZone.us_zones, 
		:default => "Pacific Time (US & Canada)")

如果我们使用 **:default** 选项，它必须显示哪一个 **TimeZone** 已经被选择。

### formatted_offset 方法

**formatted\_offset** 方法被包含在 **Time** 和 **DateTime** 类中，返回 **+HH：MM** 格式的 UTC 时差。例如，在我们的时区（北京时间），这个方法返回的时差是一个字符串 **"+08:00"**。

让我们看看一些示例：

从一个 DateTime 得到时差：

	datetime = DateTime.civil(2000, 1, 1, 0, 0, 0, Rational(-6, 24))
	datetime.formatted_offset         # => "-06:00″
	datetime.formatted_offset(false)  # => "-0600″

从 Time：

	Time.local(2000).formatted_offset         # => "-06:00″
	Time.local(2000).formatted_offset(false)  # => "-0600″

注意这个方法返回字符串，可以格式化或不依赖于一个被给予的参数。

### with\_env\_tz 方法

**with\_env\_tz** 方法允许我们以非常简单的方式测试不同的时区：

	def test_local_offset
	  with_env_tz 'US/Eastern' do
	    assert_equal Rational(-5, 24), DateTime.local_offset
	  end
	  with_env_tz 'US/Central' do
	    assert_equal Rational(-6, 24), DateTime.local_offset
	  end
	end

这个 Helper 可以调用 **with\_timezone**, 但为了避免使用 **ENV['TZ']** 和 **Time.zone** 时混乱，它被重命名为 **with\_env\_tz**.

### Time.zone_reset!

该方法已经被删除

### Time#in\_current\_time\_zone

该方法修改为当 **Time.zone** 为空时返回 **self**

### Time#change\_time\_zone\_to\_current

该方法修改为当 **Time.zone** 为空时返回 **self**

### TimeZone#now

该方法修改为返回 **ActiveSupport::TimeWithZone** 显示当前在 **TimeZone#now** 中已设定的时区。例如：

	Time.zone = 'Hawaii'  # => "Hawaii"
	Time.zone.now         # => Wed, 23 Jan 2008 20:24:27 HST -10:00

### Compare\_with\_coercion
	
在 **Time** 和 **DateTime** 类中新增加了一个方法 **compare\_with\_coercion**(和一个别名 <=>), 它使在**Time**,**DateTime**类和**ActiveSupport::TimeWithZone**实例之间可以按年代顺序排列的比较。为了更好的理解，请看下面的示例（行尾 注释显示器结果）：

	Time.utc(2000) <=> Time.utc(1999, 12, 31, 23, 59, 59, 999) # 1
	Time.utc(2000) <=> Time.utc(2000, 1, 1, 0, 0, 0) # 0
	Time.utc(2000) <=> Time.utc(2000, 1, 1, 0, 0, 0, 001)) # -1

	Time.utc(2000) <=> DateTime.civil(1999, 12, 31, 23, 59, 59) # 1
	Time.utc(2000) <=> DateTime.civil(2000, 1, 1, 0, 0, 0) # 0
	Time.utc(2000) <=> DateTime.civil(2000, 1, 1, 0, 0, 1)) # -1

	Time.utc(2000) <=> ActiveSupport::TimeWithZone.new(Time.utc(1999, 12, 31, 23, 59, 59) )
	Time.utc(2000) <=> ActiveSupport::TimeWithZone.new(Time.utc(2000, 1, 1, 0, 0, 0) )
	Time.utc(2000) <=> ActiveSupport::TimeWithZone.new(Time.utc(2000, 1, 1, 0, 0, 1) ))

### TimeWithZone#between?

在 **TimeWithZone** 类中包含 **between?** 方法检验一个实例被创建在两个日期之间。

	@twz.between?(Time.utc(1999,12,31,23,59,59),
	              Time.utc(2000,1,1,0,0,1))
	
### TimeZone#parse
	
这个方法从字符串创建一个 **ActiveSupport::TimeWithZone** 实例。例如：

	Time.zone = "Hawaii"
	# => "Hawaii"
	Time.zone.parse('1999-12-31 14:00:00')
	# => Fri, 31 Dec 1999 14:00:00 HST -10:00


	Time.zone.now
	# => Fri, 31 Dec 1999 14:00:00 HST -10:00
	Time.zone.parse('22:30:00')
	# => Fri, 31 Dec 1999 22:30:00 HST -10:00

### TimeZone#at

这个方法可以从一个 Unix epoch 数字创建一个 **ActiveSupport::TimeWithZone** 实例，例如：

	Time.zone = "Hawaii" # => "Hawaii"
	Time.utc(2000).to_f  # => 946684800.0

	Time.zone.at(946684800.0)
	# => Fri, 31 Dec 1999 14:00:00 HST -10:00

### 其他方法

**to\_a**, **to\_f**, **to\_i**, **httpdate**, **rfc2822**, **to\_yaml**, **to\_datetime** 和 **eql?** 被加入 TImeWithZone 类中。更多关于这些方法的信息请查阅相当的 Rails 文档。

### TimeWithZone 为 Ruby 1.9 准备

在 Ruby 1.9中，我们有了一些新的方法在 **Time** 类中，如：

	Time.now
	# => Thu Nov 03 18:58:25 CET 2005

	Time.now.sunday?
	# => false

一周中的每一天都有对应的方法。

另一个新的是 **Time** 的 **to\_s** 方法将会有一个不同的返回值。现在当我们执行 **Time.new.to\_s**, 将得到：

	Time.new.to_s
	# => "Thu Oct 12 10:39:27 +0200 2006″

在 Ruby 1.9 中我们将得到：

	Time.new.to_s
	# => "2006-10-12 10:39:24 +0200″

Rails 2.1拥有哪些相关的东西? 答案是所有东西，从 Rails 开始准备这些修改。 **TimeWithZone** 类，例如，刚收到一个为第一个示例工作的方法实现。