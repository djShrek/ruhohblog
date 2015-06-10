---
title: 'Creating dojoCMS Part 6 - Adding Authentication with Devise'
date: '2015-05-27'
description:
tags: [dojoCMS, Ruby on Rails, ruby]
---

Adding [authentication](http://www.gotealeaf.com/blog/authentication-methods-in-rails) is one of the most important steps to securing your application. For this project, we will be using the Devise gem to provide basic authentication. To install [Devise](https://github.com/plataformatec/devise), go your Gemfile and add:

`gem 'devise'`

Then go into your terminal and type 

`bundle install`

After it is finished [bundling](http://bundler.io/deploying.html), we use the rails command to install Devise into our project:

`rails generate devise:install`

After Devise is installed, you will see a list of commands in the terminal.
Followng the instructions, you would first add the following to 
config/environments/development.rb:

`config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }`

Then you need to add a root to your application in routes.rb:

`root to: 'statuses#index'

(To understand what this means, please checkout the Rails Guides on Routing)

Next we need to the [flash](http://guides.rubyonrails.org/action_controller_overview.html#the-flash) messages to our application laylot. They will be helpful for user feedback later on in the development of our application.

Since we are using a Rails 4.+ application, we won't have to do the next step.
The last step is related to setting up views for Devise, which we will not yet
need. With that said, that is the last step to setting up Devise in our Rails
application. If you are interested in knowing how to create a custom authentication
system, the Ruby on Rails [tutorial](https://www.railstutorial.org/) by Michael Hartl has a basic introduction to creating a authentication system so check it out. 
