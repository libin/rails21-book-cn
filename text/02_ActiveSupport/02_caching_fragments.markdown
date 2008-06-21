## Fragment\_exist?

两个新方法被加入到 **cache\_store** 中: **fragment\_exist?** 和 **exist?**。

方法 **fragment\_exist?** 顾名思义, 它检验一个 key 所指定的缓存片段是否存在。基本上代替了著名的：

	read_fragment(path).nil?

**exist?** 方法被加入到 **cache\_store**, 而 **fragment\_exist?** 是一个你能够在 Controller 中使用的 helper。