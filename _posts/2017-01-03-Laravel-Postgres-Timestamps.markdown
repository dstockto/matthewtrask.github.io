---
layout: post
title:  "Two ways to fix the Laravel Postgres Timestamp issue"
date:   2017-01-03
comments: yes
description: Working on a sideproject with Postgres and Laravel, we noticed the timestamp from Postgres didnt play nice with Laravel.
tags: Php, Laravel, Postgres
---

## Laravel vs Postgres.

Tonight we were working on an issue with timestamps coming from our Postgres database and rendered in Laravel. However we noticed that Carbon hated them and would throw exceptions rather then just manipulate our timestamps. We looked around and found a few ideas, but the one we liked most was this:

```
publuc $timestamps = false;
```

and it disables the ```getDateFormat()``` method from Eloquent. The reason an issue is caused is that the ```getDateFormat()``` is built for MySQL. Since Postgres handles timestamps a bit differently, it gets screwed up when run through the ```getDateFormat()``` method. By setting the timestamp value to false, you are passing a raw Unix timestamp up to Carbon which Carbon can interpret and manipulate. 

## One more way

Another way to solve this issue is a little more complex, but easily implemented. It would be to create a model called ```PostGresModel``` and extend the ```Illuminate\Database\Eloquent\Model```. In this new model class, which you will extend all your models from now, you would create a new ```getDateFormat()``` method and inside it, return ```'Y-m-d H:i:s.u'``` which is how you handle timestamps with Postgres. And there you go! We override the base Eloquent ```getDateFormat()``` method to handle Postgres, and now its publicaly availble to your models as long as you extend the new PostgresModel. 

Hopefully these two solutions will help others in the same spot!
