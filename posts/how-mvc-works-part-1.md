---
title: 'How MVC Works pt.1'
date: '2014-07-22'
description: 
tags: [MVC, design patterns, rails, ruby]
---
&nbsp;&nbsp;If you are using the Ruby on Rails framework,  it is necessary  to understand the basics of the Model-View-Controller MVC architectural  pattern since it is incorporated in Rails. Although it serves many different purposes, its main purpose in web applications is to help developers implement user-interfaces. The pattern separates the web application into three core components: the Model, View, and Controller. Each of these components has a separate responsibility to process what occurs after the Rails application has received a web request. 
  <p>&nbsp;&nbsp;On a conceptual level, a browser sends a request to a web
application, which is received by a web server and then passed on to the Rails router and subsequently to the controller.
The controller will then interact with the model, which will then query the database for the data that the browser has
requested for. After invoking the model, the controller will then renders the view accompanied with any data related to the
corresponding model and returns a complete web page to the browser as HTML.</p>

&nbsp;&nbsp;Before I talk about the main components of the MVC pattern in Rails, I would like to share a 
conceptual picture of what occurs after a web application receives a HTTP request: <br/>
<img class="img-responsive" src="{{urls.media}}/mvc.jpg">