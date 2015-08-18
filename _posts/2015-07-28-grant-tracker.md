---
layout: post
title:  "Do I know things?  Let's find out"
date:   2015-07-28 09:10:41
categories: rails ruby project week-nine
---

This week, we are working on group projects.  Ambitious group projects.  To build something, for real people, from scratch.

It feels like a test, right?  We've been doing 'projects', sure, but really...it was homework.  It was practice.

Now there's a real client involved, a real need.  And we have a week.  I've been mainlining Bojack Horseman over the weekend, so my first thought was this was like a game of OCS Students and Classmates...What do they Know?  Do they Know Things?  Let's Find out!!


<p style="text-align: center;"><img src="/assets/2015-07-28-hollywoo.png" alt="mr peanutbutter's quiz game asks..."></p>


Our project is to build a grant tracker for a nonprofit.  It is a combination of a warehouse for storing the files associated with Organizations and Grants, a task management system to manage the various deadlines and tasks associated with those grants, and a report generator that can help the nonprofit manage their cash flow.

On Sunday, when I read the spec, there were so many pieces of this that I didn't know how to do:

Wendy Doesn't Know How To:

- Store files
- Send emails, at all
- Or, on a schedule 
- Display items as a calendar
- Create gannt or similar charts
- Deploy secrets (like passwords and account settings) to Heroku

But it's Tuesday, and I feel like we have a plan for all of these today.  So! exciting!  Every time we're given a streeeeeetch, the discomfort has been worth it.

Here are our solutions so far: 

- We're using [Google Drive](https://github.com/gimite/google-drive-ruby) to store our files.  Haven't yet perfected (but are working on) a system to store them in folders by Organization
- [Rails has a built-in ActionMailer class to send emails](http://guides.rubyonrails.org/action_mailer_basics.html)
- ""
- Still working on this, but so far, we are just using the order method to get the tasks in date order
- Gannt charts are hard.  The only solutions I found were in very elaborate Task Management gems.  But [chartkick](http://chartkick.com/)'s timeline chart looks pretty close!
- [Figaro gem](https://github.com/laserlemon/figaro).  Even has Heroku deployment compatability.  Whaaaaat?

~~[Here is a link to our project so far.](https://github.com/omahacodeschool/grant-tracker)~~  #Edit - This repository is private, sorry.  I think we have one of the harder ones.  I am working with [Nick Emanuel](https://github.com/njemanuel01) again and [Sam Stephen](https://github.com/samstephen).  

Nick and I are working on the back end together.  Sam has the front end.  He is using a framework called [Foundation](http://foundation.zurb.com/), which I hope I get to learn more about.  It looks amazing and versatile.  

This way, we don't have to write our css from scratch.  Just like a lot of our code is either Ruby scaffolding or gems that we're employing.

Should be fun!!