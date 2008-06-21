## UTC or GMT?

这是一个修正，但是很有趣。迄今为止，Rails 使用 UTC 缩写很频繁，但是当 **TimeZone** 的 **to\_s** 方法被调用的时候，它打印 GMT，而不是 UTC。这是因为 GMT 缩写 在对于最终用户最熟悉。

如果你观察Windows 控制面板，其中你可以选择时区，你会注意到缩写是 GMT。Google 和 Yahoo 也在他们的产品中使用 GMT。

	TimeZone['Moscow'].to_s #=> "(GMT+03:00) Moscow"
