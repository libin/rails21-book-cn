## caches\_action 支持条件

**caches\_action** 方法现在支持 **:if** 选项，允许使用条件指定一个 **cache** 可以被缓存。例如：

	caches_action :index, :if => Proc.new { |c| !c.request.format.json? }

在上面的例子中，只有当请求不是 JSON 的时候 **action index** 将被缓存。