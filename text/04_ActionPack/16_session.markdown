## session(:on)

或许你还不知道这个， Rails 可以关闭 sessions：

	class ApplicationController < ActionController::Base
	  session :off
	end

注意在我的示例中，我关闭了所有 controllers 中的 session(**ApplicationController**)，但我也能单独关闭某一个 controller 的 Session。

但如果我只想打开一个 controller 的 session, 在 Rails 2.1中，该方法允许 **:on** 选项，这样做：

	class UsersController < ApplicationController
	  session :on
	end
