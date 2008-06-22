## ActionController::Routing

### Map.root

现在你可以通过别名，更加 **DRY** 的用 **map.root**。 

在早期的 Rails 版本里边，你可能是像下边这样用的：

	map.new_session :controller => 'sessions', :action => 'new'
	map.root :controller => 'sessions', :action => 'new'
	
现在的你可以这样用：

	map.new_session :controller => 'sessions', :action => 'new'
	map.root :new_session
	
### 路由识别 （Routes recognition）

路由识别的早期实现是一个接着一个的遍历所有路由，这样做是非常耗时的。新的路由识别则更加聪明，它生成一棵路由树，并通过前缀来跳过相似的路由。这种实现将路由识别的时间降低了近2.7倍。

**recognition\_optimisation.rb** 文件中新的方法和他们的工作细节都在注释中写得很详尽。通过直接阅读源代码的方份可以获得这些实现的更多信息。

### Assert_routing

现在可以通过一个 HTTP 方法来测试路由，看下面的例子：

	assert_routing({ :method => 'put',
	                 :path => '/product/321' },
	               { :controller => "product",
	                 :action => "update",
	                 :id => "321" })
	
### Map.resources
	
假设你的网站全部都是用非英文写的，你想在路由当中也使用和网站同样的语言。换句话说，你想用：

	http://www.mysite.com.br/produtos/1234/comentarios

而不是：

	http://www.mysite.com.br/products/1234/reviews

现在已经支持了，虽然用起来并比简单，但是没有违反 Rails 的约束。

现在我们可以使用 **map.resources** 里的 **:as** 来个性化我们的路由。比如上边葡萄牙语的那个例子：

	map.resources :products, :as => 'produtos' do |product|
	  # product_reviews_path(product) ==
	  # '/produtos/1234/comentarios’
	  product.resources :product_reviews, :as => 'comentarios'
	end