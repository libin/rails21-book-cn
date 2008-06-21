## has\_one和belongs\_to中的:select选项

已经为人熟知的**has\_one**和**belongs\_to**方法现在接收一个新属性**:select**。 

它的默认值是“*”(正如"SELECT * FROM table")，不过你可以更改默认值来获得任何你希望的列。

别忘了包括进主键和外键，否则你会得到一个错误。

**belongs_to**方法不再支持**:order**选项了，不过不要担心，因为那基本上没什么用处。