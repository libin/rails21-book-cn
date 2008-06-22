## Bug fixes in change\_column

一个已经存在的 bug， 当使用 **change\_column** 方法时， 使用 **:null=>true** 在 column 中，创建过使用 **:null=>false** 也已经被解决了。当你使用这个方法的时候，这个 bug 不会造成任何改变。