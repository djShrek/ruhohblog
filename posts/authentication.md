---
title: 'What is Authentication and why do we need it in our Rails Apps?'
date: '2014-11-21'
description:
tags: [rails, authentication]
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Generally, authentication is confirming the truth of any entity or piece of data (thanks [wikipedia!](http://en.wikipedia.org/wiki/Authentication) :D). This is the same
for authentication with the different aspects of the web. Some common forms of authentication that you may have come
across on the web include logging into Facebook with your password, using a captcha to confirm that you are not a robot,
and even clicking a confirmation e-mail to verify ownership of an e-mail address. For web applications, a user signs into
their account by inputting their user name or email and password. The authentication system checks that the password matches the one in the database (not entirely true but you will find out why in a second) and then confirms that
the user of an account is in indeed who he/she says they are, which then grants authorization and certain privileges to
perform actions on that account's behalf. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Even after a user has been authenticated and logged into their account, web applications need a way to “prove”
that the user is who they claim to be  when navigating from page to page on a web application. For example once you sign into Facebook, Facebook needs a way to prove that you are the user who logged in with the correct credentials with
each subsequent web request. Because HTTP is [stateless](http://en.wikipedia.org/wiki/Stateless_protocol), there needs to be a system in place that “remembers”
you are the authenticated user every time you make any kind of web request. If Facebook did not have an authentication
system, it would not be able to confirm the identity of users who make web requests and therefore authorization to make
commands (post pictures, create status updates, update profile) would be granted to everyone. With this knowledge in mind,
any web application that is going to have users that do any kind of action must also have an authentication system in
place. 

So what does an authentication system look like in code and in Rails? 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In his book, the Ruby on Rails tutorial, Michael Hartl demonstrates a simple authentication from scratch and I will
summarize it here:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hartl’s authentication system begins with giving the user a secure password that can be used to
authenticate users. Each user’s password is encrypted and stored into the database (so therefore not the actual password itself). With
each subsequent sign-in to the application, a method called “authenticate” will take the submitted password, encrypt it,
and compare the result to the encrypted value stored in the database. If the submitted,  encrypted password matches the
password(also encrypted) stored in the database, the application will authenticate the user. The reason for comparing encrypted passwords
versus the original password themselves is that if the database is somehow hacked or compromised, the hackers would have a
list of encrypted passwords instead of the originals, preventing the hacker from potentially accessing other web
applications that the users may use.

The encryption process begins by adding the bcrypt Ruby gem and you can read more about it in Hartl’s tutorial [here](https://www.railstutorial.org/book/modeling_users#sec-adding_a_secure_password)

Hartl finishes the first part the authentication machinery by a method that retrieves a user by e-mail and passwords.

First, when a user signs into their account, an HTTP request is made to the SessionsController#create action of the Rails
application.

It looks something like this:

<pre class="prettyprint linenums">
class SessionsController < ApplicationController
    def new
      # ..code..
    end

    def create
      user = User.find_by_email(params[:session ][:email])
      if user && user.authenticate(params [:session][:password ])
      # Sign the user in and redirect to the user's show page..
      else
        flash.now [:error] = 'Invalid email/password combination'
        render 'new'
      end
    end

    def destroy
      # ..code..
    end
end
</pre>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;You can see that a dynamic finder method find_by_email is being called by the User class in the create action. If the user
is found <strong>and</strong> the user’s password matches the password found in the database, the user will
then be “signed-in” by the application, otherwise, the new template is rendered and they are essentially taken to the sign
up page:

<pre class="prettyprint"> 
    flash.now [:error] = 'Invalid email/password combination'
    render 'new'
</pre>

 Next, the concept of “sessions” is introduced. According to Hartl, a "session is a semi-permanent connection between two
 computers..." and it is used to implement the pattern of "signing in" to the application that is built in his tutorial. The
 session can be implemented in different ways, but the way he chooses to implement is that when the user signs in, the
 sign in status (just a term, not an actual attribute) will be remembered "forever" and will only be cleared when the user explicitly signs out. To implement a
 session in Rails, it is "convenient to model sessions as RESTful resource", meaning a session model will be created along
 with an accompanying controller that will be used to create and destroy sessions.

Hartl completes the user sign in and authentication system by adding the necessary cookie-manipulation code. He uses a traditional Rails "session" <strong>method</strong> to store a "remember token" equal to the user's id.

<pre class="prettyprint">
  session[:remember_token] = user.id
</pre>

(*Note: This example belove is an example of a session, but is not what is actually implemented in the tutorial)
This session object makes the user id available from page to page by storing it in a cookie that expires upon browser clos
. 
In his implementation, he uses a design called "persistent sessions", that is, the signin status will last even after the browser is closed, so therefore we need to use a permanent identifier for the signed-in user. To accomplish this, we
generate a unique, remember token for each user and store it as a permanent cookie rather than one that expires on browser
close. The remember token needs to be associated with a user and stored for future use, so it has to be added to the User
model as a column to the database. For how he generates the remember token, read that section [insert link to section for
remember token]. 

For more information on sessions, check out the Ruby on Rails [guides](http://guides.rubyonrails.org/security.html#sessions)
It starts with a simple example of sessions and then gets more in-depth for people are interested in Rails security. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The last part of the authentication system ends with a working “sign_in” function. When the user successfully is
authenticated after signing in to their account, the sign_in helper method will set the cookies.permanent[:remember_token]
to to the user’s remember token like this.

<pre class="prettyprint linenums">
module SessionsHelper  
  def sign_in(user)    
    cookies.permanent[:remember_token] = user.remember_token    
    self.current_user = user
  end 
end 
</pre>

The cookies utility is used <strong>like</strong> a hash and each cookie contains two elements as if it were a hash:  a value and an
optional expiration date. After the cookie is set in the browser.

 If you noticed from the code above, 

<pre class="prettyprint">
 self.current_user = user.
</pre>

This code is to set the current user to the signed in user, so that the current user method can be used on each page.


<pre class="prettyprint">
User.find_by_remember_token(cookies[:remember_token]
</pre>

<pre class="prettyprint linenums">
def current_user=(user)    
  @current_user = user
end

def current_user 
  @current_user ||= User.find_by_remember_token(cookies[:remember_token])
end
</pre>

The method current user now will create an instance variable that will either find the user by the remember token and set
it or return the cached value of the instance variable @current_user so that on subsequent invocations it will not hit the
database. 

From here on out, you can use the current user method everywhere in your app and conveniently find the user that is
authenticated and currently signed in.

If you have used the Devise gem, you will be familiar with the current user method as it the does the same in retrieving
the current_user.

When a user “signs out of their account”, their session is essentially destroed and the remember token is reset.

<pre class="prettyprint linenums">
def destroy
  sign_out
  redirect_to root_path
end
</pre>


<pre <pre class="prettyprint linenums">
def sign_out    
  self.current_user = nil    
  cookies.delete(:remember_token)  
end
</pre>

and voila! Thats how you create a basic authentication system for your app! 

Up next: Authorization, Devise, and CanCan 

