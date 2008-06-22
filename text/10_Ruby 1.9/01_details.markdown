## 详细信息 （Details）

Rails 的修改还集中体现在对 Ruby 1.9 的支持，对新版 Ruby 中的细微改变都做了相应的调整以更好地适合要求，例如把 **File.exists?** 修改为 **File.exist?**。 

另外，在 Ruby 1.9 中，去掉了 **Base64** 模块(base64.rb)，因此，在 Rails 中，所有使用这个模板的都相应的修 
改为 **ActiveSupport::Base64**。