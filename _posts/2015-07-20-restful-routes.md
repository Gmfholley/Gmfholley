---
layout: post
title:  "Are you sure that you like RESTful Routes?"
date:   2015-07-20 09:10:41
categories: routes route-handler controller
---

[RESTful routes](https://en.wikibooks.org/wiki/Ruby_on_Rails/Routing) is a way of creating default routes for oh-so-common CRUD applications, so that it's the standard across the board.


## Methods of routes
To start, we learned that there are different methods for routes.  We have been using 'get' as the default (and it is the default!), and a few of us found code using AJAX to use 'post' to submit a form.  But there are really the following methods, one for each of the CRUD operations.

- get (for normal routes) #read
- post (for new records) #create
- put/patch (for changes to records) #update
- delete (for deletion) #delete


## Basic Routes and their associated Methods
The basic routes, in the case of a User class, for complete CRUD functionality, are:

- get 'users' => 'users#index'
- get 'users/new' => 'users#new'
- post 'users' => 'users#create'
- get 'users/:id/edit' => 'users#edit'
- put/patch 'users/:id' => 'users#update'
- delete 'users/:id' => 'users#destroy'
- get 'users/:id' => 'users#show'


RESTful Routes is the last knot undoing any need for my Menu class.  

I'm sad, but...I think I had come to the conclusion two weeks ago that it was time.  As we were adding css to past Sinatra projects (lo these...two weeks ago) I realized that part of my problem with css is that I don't have enough html to really build anything pretty.  I was constrained by my own efficiency.  Everything looks the same because it is the same.

To really build a good user application, I need to treat every model like a snowflake.  Instead of homogenizing all the colors until I get a most-efficient brown.  It served a purpose for a time.  Abandon what no longer works.

##Why you might NOT want to build RESTful routes?

- It looks ugly.  No user cares about users/6, if they are user 6.  They care who they are.
- Sometimes you care about what kind of information you give the user access to.  If you don't want them to copy a url, don't use one.

I think that's probably the only reason I can think of not to use a RESTful Route.  In the meantime, it's a nice framework to use.  No use reinventing the wheel!

Our Assignment today was to create a REStful Routes application.  [Here's mine!](https://github.com/Gmfholley/07-20-Restful-Routes)