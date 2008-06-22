## 在字符串中应用格式化标题

以前当你在一个包含了 's 的字符串中使用 **String#titleize** 方法时有一个 bug. 这个 bug 返回大写的 'S, 看一个示例：

	>> "brando’s blog".titleize
	=> "Brando’S Blog"
	
看相当的示例，但已经修复了这个bug：

	>> "brando’s blog".titleize
	=> "Brando’s Blog"
