## Auto Link

为那些不知道这个方法的人，**auto\_link**  方法接收所有文本参数，如果这个文本包含一个 e-mail 地址或一个网址，它将返回相同的文本，但有了超链接。

例如：

	auto_link("Go to this website now: http://www.rubyonrails.com")
	# => Go to this website now: http://www.rubyonrails.com

一些网站，象 Amazon, 使用 "=" 号在URL中，该方法不认可这个字符，看这个方法怎样处理这种情况：

	auto_link("http://www.amazon.com/Testing/ref=pd_bbs_sr_1")
	# => http://www.amazon.com/Testing/ref

注意该方法截断链接地址在 "=" 号前，因为它不支持这个符号。我产意思是，它通常是不被支持的，在 Rails 2.1中，我们解决了这个问题。

同样的方法将在稍后更新，允许在URL's中使用括号。

一个使用括号的示例：

	http://en.wikipedia.org/wiki/Sprite_(computer_graphics)
