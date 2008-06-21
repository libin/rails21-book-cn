##Removing whitespaces with squish method

两个新方法被加入到 **String** 对象中， **squish** 和 **squish!**。

这两个方法和 **strip** 方法一样。它删除文本前后的空格，它也删除文本中间无用的空格。看这个例子：

	“    A    text    full    of     spaces    “.strip
	#=> “A    text    full    of     spaces”

	“    A    text    full    of     spaces    “.squish
	#=> “A text full of spaces”
