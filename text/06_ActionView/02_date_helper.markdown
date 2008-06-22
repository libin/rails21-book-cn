## ActionView::Helpers::DateHelper

现在，所有的与处理时间有关的模块方法 (**date\_select**, **time\_select**, **select\_datetime**, etc.) 都接受 **HTML** 选项。请看下面使用 **date\_select** 的例子：

	<%= date_select 'item','happening', :order => [:day], :class => 'foobar'%>
	
### date\_helper

通过使用 **Date.current**，用来定义默认值的 **date\_helper** 方法也被更新。