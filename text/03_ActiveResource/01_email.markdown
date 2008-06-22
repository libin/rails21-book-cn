## 使用Email作为用户名

某些服务使用Email作为用户名，这会要求使用如下形式的URL：

	http://ernesto.jimenez@negonation.com:pass@tractis.com

这个URL中有两个"@"，这会带来问题：解释器无法正确解析这个URL。为此，对 **ActiveResource** 的使用方式作了扩展，以方便使用Email进行身份验证。可以这样来使用：

	class Person < ActiveResource::Base
	  self.site = "http://tractis.com"
	  self.user = "ernesto.jimenez@negonation.com"
	  self.password = "pass"
	end
