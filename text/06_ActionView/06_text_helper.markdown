## ActionView::Helpers::TextHelper

### excerpt

**excerpt** 方法是一个帮助方法，去搜索一个单词在一个段落，同时返回一个包含给定的数字参数的缩写，在词的前后， 必须使用"…"。请看随后的例子：

	excerpt('This is an example', 'an', 5)
	# => "…s is an examp…"
	
但是这个问题很烦。如果你去计数的话，你需要看每个方法返回6个字符而不是5个。这个bug已经解决了。看下面的正确的输出方法代码：

	excerpt('This is an example', 'an', 5)
	# => "…s is an exam…"
	
###simple\_format

**simple\_format** 方法基本上接受任何文本参数和用简单的方式格式化为 **HTML**。它接受文本并取代换行符 (\n) 采用 **HTML** 标记 "<br />"。同时当我们有2个换行符像这样的 （\n\n），将会采用 <p> 标记将它为一个段落。

	simple_format("Hello Mom!", :class => 'description')
	# => "<p class=’description’>Hello Mom!</p>"

**HTML** 属性将会添加 "<p>" 标记到对应段落上。