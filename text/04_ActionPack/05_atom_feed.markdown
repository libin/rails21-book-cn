## Atom Feed 中新的 namespaces

你知道 **atom\_feed** 方法吗？这是 Rails 2.0的一个新特性，使创建 Atom feeds 变得更容易。看一个使用方法：

在一个 *index.atom.builder* 文件中：

	atom_feed do |feed|
	  feed.title("Nome do Jogo")
	  feed.updated((@posts.first.created_at))

	  for post in @posts
	    feed.entry(post) do |entry|
	      entry.title(post.title)
	      entry.content(post.body, :type => 'html')

	      entry.author do |author|
	        author.name("Carlos Brando")
	      end
	    end
	  end
	end

什么是一个 Atom feed? Atom 的名字是基于 XML 样式的 meta 数据。 在互联网中它是一个发布经常更新的内容的协议，如Blog。例如，Feeds 经常以 XML 或 Atom 的格式发布标示为 application/atom+xml 类型. 

在 Rails 2.0的第一个版本中，该方法允许 **:language**, **:root_url** 和 **:url** 参数，你可以从 Rails 文档中获得更多关于这些方法的信息。但基于这一个更新，我们可以包含新的命名空间在一个Feed的root元素中，例如：

	atom_feed('xmlns:app' => 'http://www.w3.org/2007/app') do |feed|

将返回：

	<feed xml:lang="en-US" xmlns="http://www.w3.org/2005/Atom" 
		xmlns:app="http://www.w3.org/2007/app">

修改这个示例之前，我们这样使用它：

	atom_feed({'xmlns:app' => 'http://www.w3.org/2007/app',
		'xmlns:openSearch' => 'http://a9.com/-/spec/opensearch/1.1/'}) do |feed| 

	  feed.title("Nome do Jogo")
	  feed.updated((@posts.first.created_at))
	  feed.tag!(openSearch:totalResults, 10) 

	  for post in @posts
	    feed.entry(post) do |entry|
	      entry.title(post.title)
	      entry.content(post.body, :type => 'html')
	      entry.tag!('app:edited', Time.now) 

	      entry.author do |author|
	        author.name("Carlos Brando")
	      end
	    end
	  end
	end
