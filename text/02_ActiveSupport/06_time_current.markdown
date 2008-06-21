## Time.current

**Time** 类中的新方法。 **current** 方法返回值依赖 **config.time\_zone**, 如果之前指定过，方法返回 **Time.zone.now**，否则返回 **Time.now**。

	# return value depends on config.time_zone
	Time.current

**since** 和 **ago** 方法也改变了他们的返回值, 如果 **config.time\_zone** 已经指定，它返回一个 **TimeWithZone**。
 
它让 **Time.current** 方法作为新的默认方法来获取当前时间。代替了 **Time.now** (这个方法仍然存在，但是它不考虑指定的时区)。

**datetime\_select**方法， **select\_datetime** 和 **select\_time** 也已被更新以默认返回 **Time.current**。