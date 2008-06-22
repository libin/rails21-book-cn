## 在 Views 之外访问 Helpers

有多少次你创建了一个 **helper** 希望希望它在一个 **controller** 中使用？要做到这样，你需要包含这个 **helper** module 到这个 **controller** 中，但这使你的代码看起来不干净。 

Rails 2.1已经开发了一个方法在 Views 之外的 Helpers. 它以很简单的方式工作：

 	# To access simple_format method, for example
	ApplicationController.helpers.simple_format(text)

简单而干净。
