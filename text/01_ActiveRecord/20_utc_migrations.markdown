## 基于时间戳的Migrations (Timestamped Migrations)
              
当你一个人使用Rails开发的时候，**migrations**似乎是所有问题的最好解决方案。不过，当和团队的其他成员共同开发一个项目的时候，你就会发现(如果你尚未发现)处理**migrations**同步的问题非常棘手。Rails 2.1中基于时间戳的**migrations**解决方案很好的解决了这个问题。 

在基于时间戳的**migrations**引入之前，创建每一个migration都会在其名字之前生成一个数字，如果两个**migrations**分别由两个开发者生成，并且都没有即时的提交到版本库中，那么最后就有可能存在相同前缀数字，但是不同内容的**migrations**，这时你的schema_info表就会过期，同时在版本控制系统中出现冲突。

试图解决这个问题的尝试有很多，人们创建了很多plugins以不同的方式解决这个问题。尽管有一些plugins可用，不过一点是非常清楚的，旧的方式不能满足我们的要求了。

如果你使用Git，那么你可能在给自己挖一个更大的陷阱，因为你的团队可能同时有几个working branches，过期了的migrations则在每一个branch中都存在。这样当合并这些branches的时候就会有严重的冲突问题。

为了解决这个大问题，Rails核心团队已经改变了**migrations**的工作方式。他们废弃了原有的以当前schema_info中version列的值作为migration前缀的依据的方法，取而代之的是基于**UTC**时间，按照YYYYMMDDHHMMSS格式的字符串表达方式作为前缀。 

同时创建了一个新的叫**schema_migrations**的表，表中存着哪些**migrations**已经被执行了，这样如果发现有人创建了一个有较小值的**migration**，rails会回滚**migrations**到之前的那个版本，然后重新执行所有的**migration**直到当前的版本。 

显然，这样做解决了migrations带来的冲突问题。 

有两个新的和**migrations**相关的rake命令：

	rake db:migrate:up
	rake db:migrate:down

