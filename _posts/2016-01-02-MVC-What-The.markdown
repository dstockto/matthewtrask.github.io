---
layout: post
title:  "MVC, What The ...?"
date:   2016-01-02
comments: yes
description: New developers step into the OOP arena with little understanding of the MVC idea.  
tags: MVC, OOP, Concepts
---

# Lets talk MVC.

So one of my resolutions is to blog more. Why not right? Its a great way to grasp concepts. I dont want to write something and seem like a complete fool, so I do my research, which in turn lets me learn more.

As some of y'all know, I help run a local chapter of Free Code Camp. If you havent heard of Free Code Camp, or FCC; its a way to get people to code for free. It covers the MEAN Stack, ya know Mongo DB, Node Js, Angular JS and Express JS. Thats a lot of Javascript. Even the database is Javascript/JSON based. Opinions aside, its a cool initiative to get people coding. They aim to get you real world experience through helping non-profits with some coding issues. Rad right? Pretty much yes. Well, as I'm one of the moderators and more senior programmers in the group, I help answer questions. One I get a lot is MVC frameworks, when to use them, why are they use etc.

Its funny though, because while I field these questions; certain angry yet brilliant German developers are teaching me how to let go of the MVC. However, its not something that is easily let go. I understand the flaws of it, and I understand the uses. So lets talk about that.

## Some Examples of MVC in the Wild.

The first thing we should look at is some examples. Everyone loves a good example, and there are a lot to look at.

* [Laravel](https://laravel.com)
* [Symfony](https://symfony.com)
* [Zend Framework 2](http://framework.zend.com)
* [CakePHP](http://cakephp.org)

Outside of the PHP community we have

* [Ruby on Rails](http://rubyonrails.org)
* [Django](https://www.djangoproject.com)

The list goes on. There are hybrids even. EmberJs, AngularJs, BackboneJs, and others are MV* types of frameworks. Mainly they are built on the Model-View layer, using both as a hybrid controller situation. Not a bad idea to use them, and combined with a more powerful back end framework, you can build some really powerful web apps with them.

## What is it exactly?

The MVC pattern creates a separation of concern. It allows you to create reusable code, yet separate the logic from the views from the data modeling. Lets look deeper. First, what does MVC stand for? M is for Model, which is where we model the data for our database. Should names be split to firstName and lastName, or fullName? Well, thats the models job, to take the data passed to it, and pass it to a database the way the tables are expecting it. Next, we have V for View. Views only have the purpose of displaying data for the user. Admin sections, blogs, user pages, etc are all views you could have in an application. And that's it! The view should, and is, inherently stupid. The view should have absolutely no responsibility, no logic. It should display or take in data via a form. If you have anything else in the view, you have completely broken the MVC paradigm. Last but not lease, the most powerful component of the MVC is the C, which is for Controller. Before we go further, Controllers should have specific rules. Those rules being the SOLID concept:

* Single Responsibility Principle
* Open/Close Principle
* Liskov Substitution Principle
* Interface segregation principle
* Dependency Inversion Principle

The first four are fairly simple and straight forward. The fifth is always one developers have a tough time with. Its a complete shift in thinking. But Im not going deep into those concepts right now. Thats for a later post. Back to the controller, the logic of your application lives here. Users assigned to a sales rep, sales people assigned to an office, users shopping carts and check out are all hanlded in the controller. Its the glue, or, its the traffic cop. It directs the traffic of your application as it enters the app from the view.

## A basic MVC application

So lets walk through a simple idea. A blog for instance. We have a model. Our models are responsible for three actions. Remember two things, one we are working towards the SOLID idea I just mentioned, and we are going simple. There is a lot of functionality Im skipping right now for the sake of reading. Anyways, our model with pass data to the SQL tables, another model method will fetch all posts, and one more model will handle any updates we want to do. So three models? Yes. A little granular, but I figure why not? Lets follow the Single Responsibility Principle(SRP) as closely as we can. So each model has one method. Does this satisfy the SRP? Yes! Score!

For our controllers, we will have one that takes in the post from the user, and another controller that passes the data to the views. With a router, we can dictate how the blog responds to requests. We would set /blog/ as the last 5 blog posts we make. Anything after that is a specific post, like /blog/april/my-birthday which is a specific post. That is all controlled by the controller, and dispatched in a request to a router. Most MVC based frameworks will have a router in place for you. Now, based on the request the router gets will determine which view we get. Do we get the past posts, or a specific or the view to edit our post, thats the job of the controller and router. And then the view is hanging out, just waiting to be used in some way. It has the data and form, it just needs a friend.

## Wrap Up

Obviously the example wasnt a full blown example of a blog, or big MVC application, but its the most granular level of an application. While we mentioned SOLID, I didnt do it justice. That is coming up shortly in another post. What I hope you take away from this is an understanding of the MVC framework style. While it may not always be the best answer, it can work well for a lot of simple situations. Now go out and code something awesome!
