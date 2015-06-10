---
title: 'Creating dojoCMS Part 5 - Adding Some Interactivity'
date: '2015-05-26'
description:
tags: [dojoCMS, Ruby on Rails, ruby]
---

In this post, we want to add some interactivity to our page by hiding our edit 
and delete links when our mouse is hovered over our "status." 

So first we add some CSS rules to hide our edit and delete links:

<pre class="prettyprint linenums">
    .status .admin {
        display: none;
    }

    .status.hover .admin {
        display: inline;
    }
</pre>

Our first css rule sets display to none to any class that contains "status" followed by "admin."
The second rule sets and class with "status" AND "hover" followed by "admin" to display
inline. We need to use Javascript to add the hover class whenever the house mouse
hovers over any of our statuses. As soon as our status contains a hover class, the bottom
rule containing the "hover" class will override the top rule without it.

So in order to add our [Javascript](http://learn.jquery.com/using-jquery-core/document-ready/), we open up app/assets/javascripts/statuses.js.coffee:

<pre class="prettyprint linenums">
$(document).ready(function(){
    $('.status').hover(function(){
        $(this).toggleClass("hover");
    });
});
</pre>

So now everytime we hover over our status, the [toggleClass](http://api.jquery.com/toggleclass/) ("hover") method will
toggle the class as we hover in and out of the class.

Next, we want to add some styling to the background of each status that we hover
over:

<pre class="prettyprint linenums">
    .status.hover {
        display: inline;
    }
</pre>

So now we are missing now is a link to posting a new status. 

So above our statuses, we add:

<pre class="prettyprint linenums">
    <%= link_to "Post a New Status", new_status_path %>
</pre>

It looks okay for now, but since we have the Bootstrap framework installed,
we can utilize the classes they give us for adding style on buttons.

<pre class="prettyprint linenums">
    <%= link_to "Post a New Status", new_status_path, class: "btn btn-success" %>
</pre>

So now, we have a nice button that will allow us to create new statuses as well
as some interactivity to give our users some feedback when they hover under 
statuses. 





