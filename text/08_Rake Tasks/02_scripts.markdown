## Scripts

### plugin

命令 *script/plugin install* 现在可以使用 –e/--export 参数来导出 SVN 库，另外，增加了对 Git 库的支持。

### dbconsole

这个脚本和 script/console 一样，但是其操作的是你的数据库，换句话说，它采用命令行的方式连接到你的数据库。

另外，注意代码中说到了，目前只支持 mysql, postgresql 和 sqlite(3)，当你在 database.yml 中配置了其他类型的数据库时，会提示你 “not supported for this database type”（不支持这个数据库类型）。
