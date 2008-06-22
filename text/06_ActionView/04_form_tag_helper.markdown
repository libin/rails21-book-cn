## ActionView::Helpers::FormTagHelper

### submit\_tag

一个 **:confirm** 选项已经被添加在 **#submit\_tag** 方法中，同样的选项仍然可以在 **link\_to** 方法中使用.看下面的例子：

	submit_tag('Save changes', :confirm => "Are you sure?")