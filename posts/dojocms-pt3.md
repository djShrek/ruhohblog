---
title: 'Creating dojoCMS Part 3 - Adding Basic Styling to Layout with Bootstrap'
date: '2015-05-18'
description:
tags: [dojoCMS, Ruby on Rails, ruby]
---

In this article, we are going to make some changes to the layouts of our web application.

We want to make a change towards the layout of every single page in our application. So in
order to do that, we navigate to the views/application.html.erb file.

We want to add some margins where our content is stored, so we add the [container](http://getbootstrap.com/css/#grid) (Twitter Bootstrap) class around the <%= yield %> [ERB](http://stackoverflow.com/questions/7996695/what-is-the-difference-between-and-in-erb-in-rails) tags. This will made sure all the content in all our pages are centered with margins. 

Ex:

<pre class="prettyprint linenums">
&lt;div class="container"&gt;
  <%= yield %>
&lt;/div&gt;
</pre>

Now this looks better, but now we would like a navigation bar. 
You can go to the Twitter Bootstrap documentation page to determine the different
configurations you can set, but for now we will just install a basic navbar.

Ex:

<xmp class="prettyprint linenums" id="htmlXmp">
    <nav class="navbar navbar-default navbar-fixed-top">
      <div class="container-fluid">
        <div class="navbar-header">
          <a class="navbar-brand" href="#">
            DojoCSM
          </a>
        </div>
        <div class="collapse navbar-collapse">
            <ul class="nav navbar-nav">
                <li class="active">
                    ...link to all statuses here...
                </li>
            </ul>
        </div>
      </div>
    </nav>
</xmp>

The erb code that should be replaced above in the "link to all statuses here" should look like:

`<%= link_to "All Statuses", statuses_path %>`

This is taken from the Twitter Bootstrap [documentation](http://getbootstrap.com/components/#navbar)
If you notice, we have also used the "navbar-fixed-top" class, which "sticks" the navbar to the top.
Because we are using a sticky navigation, the Bootstrap documentation states that we should set 
a padding-top of 70px to offset the navbar. So we will do this in our app/assets/stylesheets/applications.css file:

`body {  padding-top: 70px; }`

After this, refresh the page and you will see that the nav bar will always stay on top no matter how far down
you scroll.

Another thing to note is the code:

`<%= link_to "All Statuses", statuses_path %>`

The `<%= link_to %>` method is a Rails helper method that allows for easy creation of links.
Here we use a `url_helper` method which is Statuses path. (More info on url helpers: [url_helpers](http://guides.rubyonrails.org/routing.html#path-and-url-helpers)).
To see all your url_helpers, type 

`rake routes`

in your terminal and it will list all the helper [methods](http://guides.rubyonrails.org/routing.html#inspecting-and-testing-routes) that are available.





