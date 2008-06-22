## 超时

由于ActiveResource使用 **HTTP** 来访问RESTful API，当服务器响应缓慢或者服务器不工作的时候会出问题。在某些情况下，调用ActiveResource会超时失效。现在可以使用timeout属性来设置失效时间了。

	class Person < ActiveResource::Base
	  self.site = "http://api.people.com:3000/"
	  self.timeout = 5 # waits 5 seconds before expire
	end

本例中将超时设置为5秒钟。推荐的作法是将该值设得小一些以使系统能快速检测到失败，以避免相关错误引发服务器出错。

ActiveResource内部使用Net::HTTP库来发起HTTP请求。当对timeout属性设值时，该值同时被设置到所使用的Net::HTTP对象实例的 **read\_timeout** 属性上。

该属性的默认值为60秒。