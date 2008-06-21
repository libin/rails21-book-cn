##Eager Loading

为了解释这个新的功能，我们看如下代码：

	Author.find(:all, :include => [:posts, :comments])
	
我在查询**authors**这个表的记录，同时通过**author_id**包含进**posts**和**comments**表。这个查询原来会产生这样的sql查询语句：

	SELECT
	  authors."id"          AS t0_r0,
	  authors."created_at"  AS t0_r1,
	  authors."updated_at"  AS t0_r2,
	  posts."id"            AS t1_r0,
	  posts."author_id"     AS t1_r1,
	  posts."created_at"    AS t1_r2,
	  posts."updated_at"    AS t1_r3,
	  comments."id"         AS t2_r0,
	  comments."author_id"  AS t2_r1,
	  comments."created_at" AS t2_r2,
	  comments."updated_at" AS t2_r3
	FROM
	  authors
	  LEFT OUTER JOIN posts ON posts.author_id = authors.id
	  LEFT OUTER JOIN comments ON comments.author_id = authors.id


这个sql可真是够长的，在**authors**，**posts**和**comments**三个表之间用了joins。我们管这叫做笛卡尔乘积(**cartesian product**)。 

这类查询往往在效率上边不高，所以在Rails 2.1中有了一些改进。同样的对于**Author**表的查询，现在使用了一种不同的方式从所有三个表当中取得信息。原来用了一条sql语句获得三个表记录，现在Rails用三条不同的查询语句，每个表一条，这要比之前生成的查询语句更短。新的结果可以在执行了上述代码后的log中看到：

	SELECT * FROM "authors"
	SELECT posts.* FROM "posts" WHERE (posts.author_id IN (1))
	SELECT comments.* FROM "comments" WHERE (comments.author_id IN (1))

绝大多数情况下，三个简单的查询要比一个复杂的场查询语句执行的更快。
