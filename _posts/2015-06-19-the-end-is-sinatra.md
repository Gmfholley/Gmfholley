---
layout: post
title:  "The End Is the Beginning: Sinatra"
date:   2015-06-19 09:10:41
categories: ruby models database sql third-week sinatra
---

I feel like...I have bitten off more than I can chew with my models.  Maybe because I am so *obsessed* with getting it DRY and having as few special cases as possible and having each model basically work the same.

But...but...but!!  Two of my models have Foreign Keys as instance variables and one model has a Composite Key.  These models have been a challenge to say the least.

So I got as far as this.  [I have a nice repository here](https://github.com/Gmfholley/06-12-Database).  It all *works*.  CRUD is complete.  Cool SQL joins are called.  As a theatre manager, I can schedule movies (on a single day) to a particular time and location and then crunch some numbers on what it all means.

Whew.  Yes, I am proud.  I am also disappointed.  This is not as polished as I hoped it would be.

But there is no time.  Because today, we learned Sinatra, and now we're going to move from a ruby driver and Command Line as the user experience to...the web!

I am simultaneously excited and scared.  In a good way!

#Sinatra
Sinatra is a ruby gem that turns your own computer into a web server and creates the framework to create a basic Controller with requests and responses.

So the controller in Sinatra might look like this:

```ruby
  get "/home" do
    m = TheatreManager.new
    @menu = m.home
    erb :menu
  end
```

And that means that if you ran Sinatra and typed in "localhost:`whatever_port_Sinatra_uses`/home" into your web browser, this controller would find "/home", load the erb file called "menu", and the "menu" file would have access to @menu.

So you create controllers for all the urls your user should have access to, and you generate the correct views or erb files, that should be sent to the user in response to their request.

#Assignment
>Your task is to build a browser-based UX for your Warehouse Manager using Sinatra. At bare minimum, your application should fulfill all of the functionality that it currently has via its command-line "driver".


Pretty cool! But daunting, right?

I wonder if I can still use those menus.