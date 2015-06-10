---
title: 'Creating dojoCMS Part 2 - Installing Twitter Bootstrap'
date: '2015-05-15'
description:
tags: [dojoCMS, Ruby on Rails, ruby]
---

[Twitter Bootstrap](http://getbootstrap.com/) is a robust front-end [framework](http://www.sitepoint.com/5-most-popular-frontend-frameworks-compared/) that makes front-end development fast and easy. It contains a mobile-friendly/responsive grid, a lot of nifty front-end
components (navbars, tabs, styled buttons etc.), and useful Javascript plugins that make
facillitates faster development of user interfaces.

We will be using Twitter Bootstrap in our dojoCMS application to give our application
some basic styling. To install Twitter Bootstrap, we will be using the 
[twitter-bootstrap-rails](https://github.com/seyhunak/twitter-bootstrap-rails) gem.
To get started, add the gem to your gemfile along with its dependencies:

`gem therubyracer`
`gem less-rails`
`gem twitter-bootstrap-rails`

Then run:

`bundle install`

After the gems have been installed, go to the root of your directory and run

`rails g bootstrap:install`

This will install the necessary CSS and Javascript libaries to the application.

If you run your Rails server and go to localhost:3000/statuses, you should
see a change in styles.

You can take a look at the page source (right on click on the page and click view source)
and observe the bootstrap css and javascript libraries that have been loaded. We
may not need all of these libraries for our application, but I will remove them
in a future post.

At this point, I notice that the scaffolds.scss is adding styles that I don't care for
on top of the Bootstrap CSS, so now it would be a good time to delete the scaffolds.scss
to avoid future conflicts.  
