## Mem\_cache\_store now accepts options

**Memcache-Client** 被包含在 **ActiveSupport::Cache** 中使得事情变得比以前更容易了, 但是它也剥夺了灵活性，它除了 **memcached** 服务器的 IP 之外什么都不允许我们配置。

**Jonathan Weiss** 提交给Rails一个补丁，允许额外的选项比如:

	ActiveSupport::Cache.lookup_store :mem_cache_store, "localhost"

	ActiveSupport::Cache.lookup_store :mem_cache_store, "localhost", '192.168.1.1', 
		:namespace => 'foo'

或者

	config.action_controller.fragment_cache_store = :mem_cache_store, 'localhost', 
		{:compression => true, :debug => true, :namespace =>'foo'}
