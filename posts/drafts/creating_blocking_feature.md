---
title: 'Creating a Simple User Blocking Feature Pt.1'
date: '2015-05-28'
description:
tags: [ruby, features, ruby on rails]
---

Creating a simple blocking feature for one of my old RoR applications has been
one of the main features I have been lagging for a long time. I have finally
got around to thinking of ways to implement this feature, but it is no easy
task. There are quite a number concerns to account for, namely, the problem
of state. The models involved are simply a User and its Relationship with "other"
Users. The setup I have is that a User has a Relationship model that acts as a 
join table with another user. The Relationship join table has 3 attributes:

1. user id
2. other user id
3. status

Example: 

<pre class="prettyprint linenums">
class Relationship < ActiveRecord::Base

  attr_accessible :other_user_id, :status, :user_id
  belongs_to :user
  belongs_to :other_user, class_name: "User"

  ..omitted methods..
end
</pre>

The user id is the id of the "current user" (that is signed into the app), 
while the "other user id" is the id of the user that is going to be blocked.
Finally, the status will either contain a string of "friendly" or "blocked." (and
possibly a simple "default" status, but I haven't decided a reason for that yet)

In the profile page of each user is a link to allow the current user to block
the user of the profile page. Once clicked, the application will send a HTTP
request to application's Relationship controller#create action. It looks like this:

<pre class="prettyprint linenums">
class RelationshipsController < ApplicationController
  ..omitted code..

  def create
    user = User.find(params[:user_id])
    blocked_user = User.find(params[:blocked_user])
    unless user.relationships.find_by_other_user_id(params[:blocked_user])
      user.relatiotnships.create({:status => "blocked", :other_user_id => params[:blocked_user]})
    end
      flash[:success] = "You have successfully blocked #{blocked_user.steam_name}"
      redirect_to :root
  end

  ..omitted code..
end

</pre>

As you can see from the code, the user will create a relationship with a status of "blocked"
and with the other user id that is submitted by the clicked link. 


