## Rails 的日志记录，根目录，环境变量和缓存 (Rails.logger, Rails.root, Rails.env and Rails.cache)

在 Rails 2.1里面有新方式可以替代常量： **RAILS\_DEFAULT\_LOGGER**, **RAILS\_ROOT**, **RAILS\_ENV** 和 **RAILS\_CACHE**。取而代之的是：

	# RAILS_DEFAULT_LOGGER
	Rails.logger

	# RAILS_ROOT
	Rails.root

	# RAILS_ENV
	Rails.env

	# RAILS_CACHE
	Rails.cache
