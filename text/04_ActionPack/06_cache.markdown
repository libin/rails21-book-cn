## Cache

现在所有的 **fragment\_cache\_key** 方法默认返回 'view/' 前缀命名。

所有缓存储存已经从 **ActionController::Caching::Fragments::** 删除，并替换为 **ActiveSupport::Cache::**. 在这种情况下，如果你指定一个储存地址，象 **ActionController::Caching::Fragments::MemoryStore** , 你需要这样写： **ActiveSupport::Cache::MemoryStore**.

**ActionController::Base.fragment\_cache\_store** 已经不再使用，**ActionController::Base.cache\_store** 取代了它的位置。 

由于这个新的 **ActiveSupport::Cache::*** 库，它使在 **ActiveRecord::Base** 中的 **cache\_key** 方法容易缓存一个 Active Records ，它这样工作：

	>> Product.new.cache_key
	=> "products/new"

	>> Product.find(5).cache_key
	=> "products/5"

	>> Person.find(5).cache_key
	=> "people/5-20071224150000"

它包含了 **ActiveSupport::Gzip.decompress/compress** 使得用 **Zlib** 压缩更容易。 

现在你可以在 environment 选项中使用 **config.cache\_store** 指定一个默认的缓存地址。有价值提起的是，如果 **tmp/cache** 目录存在，默认的缓存地址是 **FileStore**, 否则使用 **MemoryStore**. 你可以用以下的方式配置它：

	config.cache_store = :memory_store
	config.cache_store = :file_store, "/path/to/cache/directory"
	config.cache_store = :drb_store, "druby://localhost:9192"
	config.cache_store = :mem_cache_store, "localhost"
	config.cache_store = MyOwnStore.new("parameter")

为了把事情变得更容易，它在 *environments/production.rb* 文件中包含了以下注释，为了提醒你记得这个选项：

	# Use a different cache store in production
	# config.cache_store = :mem_cache_store
