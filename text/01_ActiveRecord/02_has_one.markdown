## Has\_one

### 支持 through 选项   

**has\_one**方法现在支持**through**选项。他的用法与**has_many:through**相同，不过代表的是和单一一个**ActiveRecord**对象的关联.

	class Magazine < ActiveRecord::Base
	  has_many :subscriptions
	end

	class Subscription < ActiveRecord::Base
	  belongs_to :magazine
	  belongs_to :user
	end

	class User < ActiveRecord::Base
	  has_many :subscriptions
	  has_one :magazine, :through => : subscriptions, 
		        :conditions => ['subscriptions.active = ?', true]
	end
	
### Has\_one :source\_type 选项

上边提到的**has\_one :through**方法还能接收一个**:source\_type**选项，我会试着通过一些例子来解释。我们先来看看这个类：

	class Client < ActiveRecord::Base
	  has_many :contact_cards 

	  has_many :contacts, :through => :contact_cards
	end 

上边的代码是一个**Client**类，**has_many**种联系人(contacts)，由于**ContactCard**类具有多态性，下一步，我们创建2个类来代表**ContractCard**： 

	class Person < ActiveRecord::Base
	  has_many :contact_cards, :as => :contact
	end

	class Business < ActiveRecord::Base
	  has_many :contact_cards, :as => :contact
	end
          
**Person**和**Business**通过**ContactCard**表与**Client**类关联，换句话说，我有两类联系人，私人的(personal)和工作上的(business)。然而，这样做却行不通，看看当我试图获取一个contact时候发生了什么：

	>> Client.find(:first).contacts
	# ArgumentError: /…/active_support/core_ext/hash/keys.rb:48:
	# in `assert_valid_keys’: Unknown key(s): polymorphic 
                       
为了让上述代码成功，我们需要使用**:source_type**。我们更改一下**Client**类：

	class Client < ActiveRecord::Base
	  has_many :people_contacts,
	           :through => :contact_cards,
	           :source => :contacts,
	           :source_type => :person 

	  has_many :business_contacts,
	           :through => :contact_cards,
	           :source => :contacts,
	           :source_type => :business
	end
	                       
注意到现在我们有两种获得联系人的方式，我们可以选择我们期待哪种**:source_type**。

	Client.find(:first).people_contacts
	Client.find(:first).business_contacts
