---
title: 'Why Rails noobs should use RVM'
date: '2014-06-27'
description:
tags: [ruby, rvm]
categories: ['code, ruby']
---

&nbsp;&nbsp;If you are just getting started with Ruby or Ruby on Rails, chances that you are likely have come across the Ruby Version Manager, or a.k.a RVM.
As stated in the introduction of the home page, "RVM is a command-line tool which allows you to easily install, manage, and work with multiple environments from interpreters to sets of gems." If you have not been acquainted with RVM, now is your chance to do so.

Why would this be important for someone who is just starting Ruby / Ruby on Rails?

&nbsp;&nbsp;&nbsp;&nbsp;RVM lets you keep your projects self-contained within their own environments, "from the specific version of ruby, all the way down to the precise set of required gems to run your application." RVM allows you to switch between different versions of Ruby (its named Ruby Version Manager after all..) and organize your gems in a different sets depending on your application's needs without different versions of the gems conflicting with one another. Having a different gem sets also avoids the issue of version conflicts between projects, which can cause HUGE, pain-in-the-neck for any newbie starting on a new project or tutorial. 

&nbsp;&nbsp;&nbsp;&nbsp;There are many more other benefits to using RVM, many that I haven't even touched upon, but the main use for it for myself is creating different gem sets when I start a new project or work on a new tutorial. For example, I am a student at teamtreehouse.com and they have two courses that are related to Ruby on Rails. The first course (called "Build A Simple Application") requires Ruby 1.9 and RoRails 3.2.7 and several gems. Their second course (titled "Build a Todo List Application") requires Ruby 2.0 and Ruby on Rails 4. If I were to do course 1 but with installing Ruby 2.0 and RoRails 4 instead of their older versions, I would no doubt come across gem conflicts and/or gem incompatibility issues with the project and a massive headache would ensue. In fact, when following any online tutorial, I recommend installing the exact version numbers as you see them in the tutorial, and not just simple doing "gem install [insert gem name]" or simple adding " gem '[insert gem name]' " to your gemfile. Trust me, it's better to be specific and explicit so you would avoid gem installation problems and/or errors when working on your tutorials/application.

&nbsp;&nbsp;&nbsp;&nbsp;A simple example would be that I install Ruby 1.9  and RoRails 3.2.7 or the first course. Then create a gemset called "course1gemset" and install the required gems for the tutorial application. Then install Ruby 2.0 and create a new gemset called "todogemset" and install RoRails 4 with required gems for the tutorial. You can switch back and forth depending on which tutorial / project you are working on without having to worry about gem conflicts. Example on the command line:

<pre class="prettyprint">
    rvm install Ruby --version 2.0
    /* installs version of Ruby 2.0 */

    rvm gemset create "todogemset" 
    /* creates gemset */

    rvm install Rails --version 4.0.0
    /* installs 4.0 version of Rails into gemset*/
</pre>

Another example would be lets say you wanted to start your own project that uses Ruby 1.9.3 and Rails 3.2.7 but it uses gems that you might or might have not yet installed and they might be a different version from the gems you have previously installed. You can simply create a new gemset without having to worry if the old gem and its dependencies will be compatible with the gem required in your new project since this gemset is self-contained in its own environment. Example on the command line:

<pre class="prettyprint">
    rvm install Ruby --version 1.9.3 
    /* installs older version of Ruby */

    rvm gemset create "rorTutgemset"
    /* creates gemset */

    rvm install Rails --version 3.2.7 
    /* installs older version of Rails into gemset*/
</pre>

Now these two gemsets will be encapsulated in their own environments.

&nbsp;&nbsp;&nbsp;&nbsp;For documentation on rvm and how to create gem sets, go to https://rvm.io/ and https://rvm.io/gemsets/basics. Good luck!  
