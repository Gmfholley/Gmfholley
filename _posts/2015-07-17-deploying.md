---
layout: post
title:  "Launching in Ten, Nine, Eight..."
date:   2015-07-17 09:10:41
categories: heroku web deploying
---

Pretty quickly, as we're finishing up our AJAX API project and thinking about the weekend, Sumeet taught us how to deploy a Sinatra project.

I am so excited I can hardly breathe.  Because it's like, Finally!  We can show our work, not just our code.

Having said that, know that I was unsuccessful today.  Firstly, we need to be using ActiveRecord to deploy to the site he showed us called Heroku.  None of my projects are updated that way yet.

Secondly, there are a lot of steps.  And it feels a bit weird.  We have our computers set up to push our code to Heroku from command line (which is awesome), but I am not certain of what every step is doing.

So to break it down, these are the steps...

1. Create a Gemfile and Gemfile.lock that have a list of all current gems, so the server that receives your application knows what to install.
2. Use a gem called Bundler to handle the Gemfile installation and bundling for you.
3. Create a config.ru (Rack Up) file that connects to the database (defining different types for deployment vs. testing) and that tells the server which file to run when it's ready.
4. Push it all to the deployment server.  (Hope for the best.)


Heroku offers free server hosting...with caveats.  It requires that your site sleep for part of the day, meaning if there is no steady traffic, it falls asleep, and the first user during sleep time will have to wait for the server to wake up your application.  But still ok if 99% of users are, for example, on normal daytime schedules in North America.

It doesn't promise that it will run any scheduled task exactly on time.

It only allows five sites without a credit card (even if the charge is $0.)

Still pretty cool!  I'm going to try this on the weekend!

##Update
Here is a link to a working Heroku site.  Just a user login for now, but feel free to click and see!
http://thawing-brushlands-5743.herokuapp.com/
