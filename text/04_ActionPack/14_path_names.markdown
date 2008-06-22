## Path Names

我的 Blog(http://www.nomedojogo.com) 读者们应该知道我的 **Custom Resource Name** 插件，这想它很快就要死亡了…:( 

在 Rails中你已经包含了 **:as** 选项在 routes（一些我实现在插件中保持兼容的东西）中，现在你将也拥有 **:path_names** 选项改变你 **actions** 的名字。
	
	map.resource :schools, :as => 'escolas', :path_names => { :new => 'nova' }

当然，我的插件当继续对早期的 Rails 版本有用。
