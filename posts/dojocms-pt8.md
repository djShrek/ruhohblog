---
title: 'Creating dojoCMS Part 8 - Creating a User with Devise'
date: '2015-05-28'
description:
tags: [dojoCMS, Ruby on Rails, ruby]
---

In this post, we will use Devise to generate views for our User.
First, type in the following command:

`rails generate devise:views`

This will generate a bunch of files for us and will allow us to change our sign up page.
The sign up page will be under app/views/devise/registrations/new.html.erb file.
We proceed by creating some form inputs for a User's first name, last name, and profile name.
Within the form_for helper method, we add divs with labels and text fields for our first, last,
and profile names.

<pre class="prettyprint linenums">
	<div>
		<%= f.label :first_name %><br />
		<%= f.text_field :first_name %>
	</div>

	<div>
		<%= f.label :last_name %><br />
		<%= f.text_field :last_name %>
	</div>

	<div>
		<%= f.label :profile_name %><br />
		<%= f.text_field :profile_name %>
	</div>
</pre>

In Rails 4, you cannot mass-assign attributes of any model without first whitelisting them. This feature, known as strong parameters, requires you whitelist attributes in the controller within the context that they will be used in. Because we are customizing our own views and adding new attributes to our form, we need to let Devise know of any parameters that will be pass down to the model. In order to permit additional parameters (the lazy way), we can do so using a simple before filter in our ApplicationController:

<pre class="prettyprint linenums">
	class ApplicationController < ActionController::Base
	  ..omitted code..

	  before_action :configure_permitted_parameters, if: devise_controller?

	  protected

	  def configure_permitted_parameters
        devise_parameter_sanitizer.for(:sign_up) do |u|
		  u.permit(:first_name, :last_name, :profile_name, :email, :password, :password_confirmation, :remember_me)
        end
	  end
	end
</pre>

If you start your server and go to localhost:3000/users/sign_up, you will be able to see a functioning sign-up page. 

Useful links:

[-http://easyactiverecord.com/blog/2014/04/01/rails4-strong-parameters-and-the-attr-accessible-macro/](http://easyactiverecord.com/blog/2014/04/01/rails4-strong-parameters-and-the-attr-accessible-macro/)
[strong parameters](http://guides.rubyonrails.org/action_controller_overview.html#strong-parameters)