I know there is a beautiful gem [Gibbon][1] available for Mailchimp, but sometime there come some conflicts and issues when you try to install Gibbon. For example i got many conflicts of Gibbon dependencies with other gems. I know there is [sample application][11] available for mailchimp-api but i believe instead of going through sample application it would be much better if there would be some documentation for mailchimp-api gem.

So i try to integrate **Mailchimp official gem**, ([mailchimp-api][2]) and succeeded. Now when I try to find some documentation of it i got nothing.  

So i thought it would be a good idea to have some documentation, that would be helpful for others.

Make the following constants, in your enviornment file or where ever you are mentioning the constants.


    MAILCHIMP-API-KEY = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-xxx"


You can have a look [here][4] (mailchimp documentation), how you can get the API-KEY.

Now there are multiple things that you can do from mailchimp-api. I am metioning the basic's that used commonly.

Now create the List at mailchimp and get the listId [here][5] you go, you can create the list and get the listId.

Add it in your constants, where you mentioned the API-KEY.


MAILCHIMP-LIST-ID = "xxxxxxxxxx"

Now the time is to get to know how to use [mailchimp-api gem][6]

UseCases
--------

Following line will create the object of mailchimp, we will access the mailchimp-api method using this object.

    mailchimp = Mailchimp::API.new(MAILCHIMP-API-KEY)


Use cases that we will be using are listed below.

 1. **Fetch All Members**
 2. **Get Members Info** 
 3. **Get All Lists**
 4. **Subscirbe Single User**
 5. **Subscribe Members in Batch**
 6. **Get All Campaigns**

Fetch All Members
----------------

    mailchimp.lists.members(MAILCHIMP-LIST-ID)['data']


Get Members Info
----------------


    emails = [{
                "email" => {
                             "email" => "awais@testing.com",
                             "euid"  => "275",
                             "leid"  => "27546289917a6"
                           }
             }]

    mc.lists.member_info(MAILCHIMP-LIST-ID, emails)

for further information of this method you can have look [here][7]

Get All Lists
----------------

      lists = mailchimp.lists.list
      list  = lists['data']


Subscirbe Single User
---------------------

    mailchimp.lists.subscribe(MAILCHIMP-LIST-ID, 
                       { "EMAIL" => { "email" => awais545@gmail.com,
                         "EUID" => "123",
                         "LEID" => "123123"
                       })

for further information of this method you can have look [here][8]

Batch Subscribe
----------------

Example for this method is not even given in [mailchimp-api sample project][9]. 

Inorder to do bulk upload of subscribers. MailchimpApi provides you a method using which you can simply pass the hash of data and in single call all of your subscribers will be added at mailchimp.

Hash would be created in following format


    subscribers = [{ "EMAIL" => { "email" => awais545@gmail.com,
                     "EUID" => "123",
                     "LEID" => "123123"
                   },

                   :EMAIL_TYPE => 'html',
                   :merge_vars => { "FIRSTNAME" => "Muhammad Awais",
                                    "LASTNAME"  => "Muhammad Ilyas",
                                    "STATUS"    => "Subscribed",
                                    "LBOOKCNTRY" => "United States"
                                  }
                  }]

Now you can simply call the following method and it will do bulk upload at mailchimp.

    mailchimp.lists.batch_subscribe(MAILCHIMP-LIST-ID, subscribers, false, true, false)

You can have look [here][10](mailchimp api documentation) or [here][11] (ruby-docs)to get further information about batch-subscribe.

Get All Campaigns
-----------------

    mailchimp.campaigns.list

You can also filtered the campaigns on there status as follow

    mailchimp.campaigns.list({:status=>'sent'})


Contributing
------------

 1. Fork it
 2. Create your feature branch (git checkout -b my-new-feature)
 3. Commit your changes (git commit -am 'Added some feature')
 4. Push to the branch (git push origin my-new-feature)
 5. Create new Pull Request


  [1]: https://github.com/amro/gibbon
  [2]: http://rubydoc.info/gems/mailchimp-api/2.0.4/Mailchimp/Lists#batch_subscribe-instance_method
  [3]: https://github.com/mailchimp/mcapi2-ruby-examples
  [4]: http://http://kb.mailchimp.com/article/where-can-i-find-my-api-key
  [5]: http://kb.mailchimp.com/article/how-can-i-find-my-list-id/
  [6]: https://rubygems.org/gems/mailchimp-api
  [7]: http://rubydoc.info/gems/mailchimp-api/2.0.4/Mailchimp/Lists#batch_subscribe-instance_method
  [8]: http://rubydoc.info/gems/mailchimp-api/2.0.4/Mailchimp/Lists#batch_subscribe-instance_method
  [9]: https://github.com/mailchimp/mcapi2-ruby-examples
  [10]: http://apidocs.mailchimp.com/api/2.0/lists/batch-subscribe.php
  [11]: http://rubydoc.info/gems/mailchimp-api/2.0.4/Mailchimp/Lists#batch_subscribe-instance_method
