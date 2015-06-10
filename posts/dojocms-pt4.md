---
title: 'Creating dojoCMS Part 4 - More Styling to Layout with Bootstrap'
date: '2015-05-20'
description:
tags: [dojoCMS, Ruby on Rails, ruby]
---

In our previous post, we made some minor changes to the layout of the application.
We will continue to make the layout better by adding more styling to the headers
and centering our main content.

We first add a Twitter Bootstrap "page-header" class to our h1 tag to give it
an underline so that it can make our heading stand out more.

<pre class="prettyprint linenums">
&lt;div class="page-header"&gt;
  &lt;h1&gt;All of the Statuses&lt;/h1&gt;
&lt;/div&gt;
</pre>

Now our users know what the header is referring to.

Next, we want to [loop](http://ruby.bastardsbook.com/chapters/loops/) over all our statuses and display them to the page.

<pre class="prettyprint linenums">
    <% @statuses.each do |status| %>
        &lt;div class="status"&gt;
            &lt;strong&gt;<%= status.name %>&lt;/strong&gt;
        &lt;/div&gt;
    <% end %>
</pre>

The @statuses is an instance [variable](https://rubymonk.com/learning/books/4-ruby-primer-ascent/chapters/45-more-classes/lessons/110-instance-variables) that will contain all our stasues.
The [each](http://www.tutorialspoint.com/ruby/ruby_iterators.htm) method takes a block that will pass each status into the loop
and each status in the @statuses instance variable will be printed to the page.

Next, we would like to add the content of the status right under the name of the
person who wrote the status:

`<p><%= status.content %></p>`

Next we add some links to accompany our status which include showing, editing,
and deleting our status. 

<pre class="prettyprint linenums">
    &lt;div class="meta"&gt;
        <%= link_to time_ago_in_words(status.created_at) + " ago", status %> | &lt;span class="admin"&gt;
              <%= link_to "Edit", edit_status_path(status) %> | 
              <%= link_to "Delete", status, method: :delete, data: { confirm: "Are you sure you want to delete this Status?" } %> &lt;/span>
    &lt;/div&gt;
</pre>

Our statuses is looking pretty good. We will close this part out with some margins
so that our statuses aren't so clumped up together. Go to your app/assets/stylesheets/statuses.scss
file and include these stylings:

<pre class="prettyprint linenums">
    .status {
        border-bottom: solid 1px #CCC;
        padding: 5px 0;
    }

    .status p {
        margin: 4px 0;
    }
</pre>

With this done, your statuses should be nice and centered with margins separating.

