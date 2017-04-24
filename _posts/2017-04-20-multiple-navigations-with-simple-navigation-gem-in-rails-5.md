---
layout: post
title: "Multiple navigations with simple_navigation gem in Rails 5"
description: ""
category: 
tags: []
---
{% include JB/setup %}

I am using [Materialize](http://materializecss.com){:target="_blank"} as my application frontend framework and using [simple_navigation](https://github.com/codeplant/simple-navigation){:target="_blank"} to manage navigation of the application.

Materialize is view responsive, therefore it illustrates two navigations, one for web view, other for mobile view, the difference between the two is the class name of ul elements.

Customizing class name in simple_navigation is implemented in simple_navigation config file.

With rule in simple_navigation, I should specify only one class for ul element in the config file for each navigation, so I have to create more than one navigation config file.

![nav_doc](/images/nav_doc.png)

From the [wiki](https://github.com/codeplant/simple-navigation/wiki/FAQ#-can-i-conditionally-render-links-to-model-edits-only-when-a-record-is-shown){:target="_blank"} above I got that the render_navigation method specifies navigation config file by the 'context' param, so I created a navigation config file named mobile_navigation, corresponding to the default named navigation config file.

![nav_wrong_config](/images/nav_wrong_config.png)

I coded the camelcase name according to the file name by [convention](http://stackoverflow.com/questions/38810857/rails-ruby-class-name-must-base-on-file-name){:target="_blank"}, next step, I applied the configuration for rendering mobile navigation.

![nav_code](/images/nav_code.png)

I got an error after refreshing the page.

![nav_error](/images/nav_error.png)

It shows that the constant name is undefined, I should define a class named MobileNavigation and the class MobileNavigation behaves all the same as class SimpleNavigation.

I used to try to create a custom renderer before in wrong thought, it's [boring](https://github.com/codeplant/simple-navigation/wiki/Custom-renderers){:target="_blank"} and it's not what I want actually, I just need two navigations with different css style but with common behavior.

Before doing the boring thing as before, I tried to change the constant name to the existent constant SimpleNavigation.

![nav_right_config](/images/nav_right_config.png)

To my surprise, the error page disappeared, there came the right page.

I recognized that the config file is not a class definition, the naming convention is not for a config file, the convention should be based on the 'Class' keyword, I just thought in wrong way.

Anyway, the two navigations work pretty well now.
