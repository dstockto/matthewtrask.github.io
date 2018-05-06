---
layout: post
title:  "Two nifty things I learned about Doctrine over the past week"
date:   2018-02-05
comments: yes
description: I had a fun thing to work on at work and it let me dive into some cool Doctrine stuff.
tags: ORM, Doctrine, Work
---

This is now the 4th different database tool I've worked with in PHP. It helps that the original author is just 25 feet or so awat from me
at work, but as I grew as a PHP developer, the debate I always heard was: Eloquent vs Doctrine. Active Record ORM vs Data Mapper ORM. Personally
I never dove into what the difference was, I just went with what was being used and learned it to make sure I could leverage whichever tool Im using.

### A brief primer on ORM's

From Wikipedia: 

> Object-relational mapping (ORM, O/RM, and O/R mapping tool) in computer science is a programming technique for converting data between incompatible type systems using object-oriented programming languages. This creates, in effect, a "virtual object database" that can be used from within the programming language.[1] 

So from this, we can infer that an ORM is a layer in between our application and the database itself. Wikipedia uses an example of a Person class with properties like 

* Name
* Address
* PhoneNumber

and more. But we can't store a phone number as is, if we follow the American format (111-867-5309) right? So we "let" the ORM transform it when it goes into the database to 
something easy for the database to deal with such as one big integer (1118675309), and when we pull it out of the database, we can then transform it back to 111-867-5309 or something else. 

But there are two types of ORM's out there, what is the main difference? Martin Fowler's [blog](https://www.martinfowler.com) has a definition of each:

#### Data Mapper

"The Data Mapper is a layer of software that separates the in-memory objects from the database. Its responsibility is to transfer data between the two and also to isolate them from each other. With Data Mapper the in-memory objects needn't know even that there's a database present; they need no SQL interface code, and certainly no knowledge of the database schema. (The database schema is always ignorant of the objects that use it.) Since it's a form of Mapper (473), Data Mapper itself is even unknown to the domain layer."

#### Active Record

"An object carries both data and behavior. Much of this data is persistent and needs to be stored in a database. Active Record uses the most obvious approach, putting data access logic in the domain object. This way all people know how to read and write their data to and from the database."

The main difference we can infer is that Active Record carries more then just data, it carries behavior and lets you do some cool and powerful things. Data mapper works in the background, almost hidden, doing its job and forgetting once the job is finished. I may also be super wrong. Meh. 

But so no that we clarified that, lets look at Doctrine and the cool things I figured out this week. 

### An event listener pattern in the ORM. 

The task at hand was this: create an audit log for certain parts of our admin system so when a change is made, we have a record of who did it, why and when. My boss mentioned the event system in Doctrine would be ideal for this. At first I had zero idea what he meant. 
In Eloquent, which I used previously, it never exposed events to userland. Things like 
```php
preFlush(), onFlush(), postFlush()
``` were not things we had to deal with. It was all handled in the background through the Active Record pattern. 
