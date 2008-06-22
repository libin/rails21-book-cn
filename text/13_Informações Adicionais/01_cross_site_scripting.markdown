## 防止跨站攻击 (Protecting from Cross Site Scripting)

在 Rails 2.0 的 *application.rb* 中，你应该留意到如下这段代码：

	class ApplicationController < ActionController::Base
	  helper :all

	  protect_from_forgery
	end

请注意上面这段代码中对 **protect\_from\_forgery** 的调用。

你听说过跨站 (XSS) 么？最近一段时间, XSS 日益风行，就目前而言，在大多数的网站中都存在或多或少的 XSS 缺陷；而 XSS 缺陷会被一些怀有恶意的人 利用，可以修改网站内容，钓鱼，甚至通过 JS 来控制其他用户的浏览器等。尽管攻击方式不同，但是其主要目的都是使得用户在不知情的情况下做了一些“邪恶” 的事情。其最新的攻击手段为 “cross-site request forgery”。Cross Site Request Forgery 和前面说的 XSS 原理差不多，但是其更有危害性，随着 Ajax 的日渐盛行，这类漏洞的利用空间和手段更加灵活。

（补充：CSRF在这里介绍的不是很多，我以前写了一篇介绍CSRF的文章，感兴趣的请自行查看《CSRF: 不要低估了我的危害和攻击能力》） 

**protect\_from\_forgery** 用来确保您的系统接收到的 form 信息都来自于你系统本身，而不会是从第三方提交过来的；其实现的原理是在你的 form 中和 Ajax 请求中添加一个基于 session 的标识 （token），控制器接收到 form 的时候检查这个 token 是否匹配来决定如何响应这个 Post 请求。

另外，值得一提的是这个方法并不保护 Get 方式的请求，不过也无所谓， Get 方式的只是取数据，而不会存数据到数据库中。

如果你想更多的了解 CSRF (Cross-Site Request Forgery)，请参考如下两个地址： 

* [http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750](http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750)

* [http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750](http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750)

请切记，这个方法不能保证万无一失，就像我们平时喜欢说的那样，他并不是银弹！
