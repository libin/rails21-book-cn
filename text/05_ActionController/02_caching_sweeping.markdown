## ActionController::Caching::Sweeping

在早期的 Rails 版本里，当我们在声明 **sweeper** 的时候，我们必须在类里边用 symbols：

	class ListsController < ApplicationController
	  caches_action :index, :show, :public, :feed
	  cache_sweeper :list_sweeper,
	                :only => [ :edit, :destroy, :share ]
	end
	
现在我们可以清楚的申明一个类而不是用 symbol.比如你的 **sweeper** 藏在一个 model 里，这么做是必须的。虽然你可以仍然在其他情况当中使用 symbol,但是从今天开始，你可以这么做：

	class ListsController < ApplicationController
	  caches_action :index, :show, :public, :feed
	  cache_sweeper OpenBar::Sweeper,
	                :only => [ :edit, :destroy, :share ]
	end