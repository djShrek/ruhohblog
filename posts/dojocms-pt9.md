---
title: 'Creating dojoCMS Part 9 - Adding has_many / belongs_to relationship'
date: '2015-06-02'
description:
tags: [dojoCMS, Ruby on Rails, ruby]
---

In this post, we will associate our statuses with our users so that our users can generate statuses when logged into their account. We first generate a new migration:

`rails generate migration add_user_id_to_statuses`

This will create a new migration file where we can add statuses column to our users table. Go to db/migrate and click on the most recently created migration file(the name of the files will be different depending on the time you create the file). Once inside, add this code to your file:

<pre class="prettyprint linenums">
	def change
	  add_column :statuses, :user_id, :integer
	end
</pre>

What this code does is that it will add a column "user_id" with a type "integer" to your statuses table. Since we will also want to find the user based on the status, we will also add an index as well:

<pre class="prettyprint linenums">
	def change
	  add_column :statuses, :user_id, :integer
	  add_index :statuses, :user_id
	  remove_column :statuses, :name
	end
</pre>

If you noticed, I also added a remove_column :statuses, :name since we wont' be needing the name attribute of the status anymore. Our statuses will now be linked to the user who created that status. Once this is done, we will run the migration:

`rake db:migrate`

After this, you can go into the rails console and delete all the previous statuses so you will only have statuses containing the new attributes:

`rails c`

then:

`Status.delete_all`

Once you are done with this, your statuses will now "belong" to users and users will "have many" statuses.

If you have been following along up until this point, your sign up page should look something like this:

<img class="img-responsive" src="{{urls.media}}/revised_sign_up.png">

Statuses#index should look something like this:

<img class="img-responsive" src="{{urls.media}}/revised_statuses.png">




