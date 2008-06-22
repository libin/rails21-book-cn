## ActionView::Helpers::NumberHelper

### number\_to\_currency

**number\_to\_currency** 方法接收 **:format** 选项作为参数，允许我们格式化方法返回值。 在之前的版本中，当我们不得不对本地的货币进行格式化时，我们需要包含在 **:unit** 选项前面包含一个空格，使得输出格式正确。看下面的例子：
	
	# R$ is the symbol for Brazilian currency
	number_to_currency(9.99, :separator => ",", :delimiter => ".", :unit => "R$")
	# => "R$9,99″

	number_to_currency(9.99, :format => "%u %n", :separator => ",", 
		:delimiter => ".", :unit => "R$")
	# => "R$ 9,99″
	
随后，我们优化成另一个 form，例如：

	number_to_currency(9.99, :format => "%n in Brazilian reais", :separator => ",", 
		:delimiter => ".", :unit => "R$")
	# => "9,99 em reais"

当需要创建你自己的字符串格式，只需使用以下的参数：

	%u For the currency
	%n For the number