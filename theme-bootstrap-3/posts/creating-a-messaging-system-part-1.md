---
title: 'Creating a Messaging System From Scratch Part 1'
date: '2014-03-25'
description: 
tags: []
---

&nbsp; &nbsp; &nbsp;&nbsp;In this series of posts, I'm going to share my experience of how I created a private messaging system between two users. The reason I picked this topic is because I noticed that many other developers had
<a href="http://stackoverflow.com/questions/5102832/rails-private-message-system">faced similar questions</a> and
<a href="http://stackoverflow.com/questions/18952216/rails-3-set-a-conversation-id-for-private-messaging">problems</a>
while I was browsing the StackOverFlow threads on the same topic. There was not a consensus among the community on how to develop a private messaging system, only that doing it from scratch would be most convenient for (we) the developers without having to implement an entire gem (i.e. mailboxer) for overkill. 

I first started with the logic:  
&nbsp; &nbsp; 1.  A user can send many messages and therefore has many messages.  
&nbsp; &nbsp; 2.  A message can have a sender and a recipient and therefore belongs to a sender and a recipient.  
So the two models I start out with are these:


    class User < ActiveRecord::Base
        has_many :messages, 
           foreign_key: "messenger_id"
        has_many :received_messages, 
           class_name: "Message",
           foreign_key: "recipient_id"
    end    

And this:

    class Message < ActiveRecord::Base
        attr_accessible :content, :messenger_id, :recipient_id

        belongs_to :messenger, 
                   class_name: "User",
                   foreign_key: "messenger_id"


        belongs_to :recipient, 
                    class_name: "User", 
                    foreign_key: "recipient_id"
    end



