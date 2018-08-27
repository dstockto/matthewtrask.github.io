---
layout: post
title:  "Laravel, JSON API and OpenAPI"
date:   2018-08-17
comments: yes
description: Building an OpenAPI spec JSON:API with Laravel.
---

What do you need to build a specced JSON:API (link) that also follows the OpenAPI (link) spec? Surprisingly, not a whole lot. 
With one PHP package (nemoarx/json-api) and one Javascript package (wework/speccy), we can take an idea to API with the confidence we are
following a standard that is known and used by many other developers across the world. Let's dive in and figure this all out. This is to compliment my
talk at Cascadia PHP (link) next month.

### JSON API and OpenAPI - A marriage of awesome.

Per the JSON:API Spec: "If you’ve ever argued with your team about the way your JSON responses should be formatted, JSON API can be your anti-bikeshedding tool."
In the same vein as PSR-2, this aims to remove people from the "this is better" type conversation of implementing JSON for your API endpoint. Instead, you can follow this
standard and know that your API will follow the same style as many other APIs. OpenAPI on the other hand: "a specification for machine-readable interface files for describing, producing, consuming, and visualizing RESTful web services.".
This means we now have a standard to document and share your API. Pretty cool right? The tooling around OpenAPI gets better every day and I'll shamelessly plug [OpenAPI.tools](http://openapi.tools)
as a directory of tools you can use to write OpenAPI specs. 

### An API around Walt Disney World

I struggled for a while with what to actually build. I wanted something more then just "simple". I wanted to demonstrate the power of JSON:API and OpenAPI. The Star Wars API
already exists so I couldn't dupelicate that, so I figued I would pick something fun that had a good set of relationships: an API for Walt Disney World in Orlando. So lets walk through it all.

We will use Laravel to get us started. 

```bash
$ composer create-project laravel/laravel --prefer-dist DisApi
```

