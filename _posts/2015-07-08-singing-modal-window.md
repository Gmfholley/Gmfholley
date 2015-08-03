---
layout: post
title:  "Javascript But Now for the Web!"
date:   2015-07-08 09:10:41
categories: javascript pair-programming
---

##A simple game...in javascript

Yesterday, we pair programmed for the first time.  I paired with the lovely [Kerry Rosenberg](https://github.com/klrosenberg), and we got along great.

Pair programming is simultaneously fast and slow.  One person is typing, but there's someone there to strategize with, someone there to catch your mistakes.  You're moving at the speed of the other person instead of your own, but slowing down that much makes you more focused.

We had a great day.

Our project was to make a quiz game entirely in javascript.  The coolest part was learning DOM (Document Object Model) manipulation...which is a fancy, technical way of saying that we could reference, manipulate, and change any HTML element using javascript.

You can also do this directly in the browser using the Console tools.  In Chrome, if you inspect element, you get a Developer pane to the right of your browser.  If you switch to the Console section, you can use the Console to type in javascript live, just like a repl.it function, but accessing any HTML element on that page. 

You are not changing the website.  That was still given to your browser by the server.  But you can edit it to your heart's content locally.

Here's me accessing the h1 element of my Javascript game using console.

<img src="2015-07-08-dom-manipulation.gif" alt="using console to get the h1 tag" style="text-align: center;">

So yesterday, entirely in javascript, we made a simple game.

##Now that we know the language, let's practice what people *normally* do with javascript

No one actually creates quizzes like we built them in javascript yesterday.  We were using alerts and logs to communicate with the user.  Annoying.  Impractical.  The web site still looks pretty shitty.

We need to use web elements to do the same thing.  And further, we need to know how to do some basic things in the web that we all experience but hadn't yet learned how to do.

Today, we are pair programming again to create HTML functionality that you have probably seen all the time. Things you expect to happen when you click or scroll but that are not possible with html and css.  For example:

1. An Accordion
<img src="2015-07-08-accordion.gif" alt="an accordion style menu" style="text-align: center;">

2. Appearing/disappearing menu
<img src="2015-07-08-hamburger-menu.gif" alt="a menu apears when you click on it" style="text-align: center;">

3. Appearing/disappearing Modal window
<img src="2015-07-08-modal-window.gif" alt="a pop-up window appears" style="text-align: center;">

4. Automatic tabbing to the next input field when a certain character limit is reached
<img src="2015-07-08-phone-number.gif" alt="tab to the next phone number slot after three digits" style="text-align: center;">

5. Changing screen at a certain scroll height

Since there's not much on this screen, it's hard to see because there's not much on the page.  But the nav par is 'sticky', staying at the top when you scroll down, and when you scroll down far enough, the nav bar shortens in height and the picture at upper left changes.

<img src="2015-07-08-scroll-effect.gif" alt="nav bar changes when you scroll down" style="text-align: center;">

6. Tabs that display their content when clicked
<img src="2015-07-08-tabs.gif" alt="content changes according to the tab you click" style="text-align: center;">

Nothing today was hard, but everything was important.  These elements are so much a part of the user experience of the web, that we will be creating these same features in almost every web application.

It's all coming together!  It feels like we're finally playing with a complete set of tools.  I can imagine, with what we know now, that *given time*, we could create something that users would recognize as part of today's web.

##Pair Programming

These exercises were all a result of pair programming.  Today, I was working with [Andrew Lodes](https://github.com/alodes999) and [Nick Emanuel](https://github.com/njemanuel01).

Some reasons to pair program are:

- It's faster.
  - Because it's easier to stay on task when you pair
  - Constant [rubber ducking*](https://en.wikipedia.org/wiki/Rubber_duck_debugging) 
  - You have two minds tackling a problem
- Your code is better.
  - You notice somebody else's mistakes; they notice yours
  - Being watched makes you slow down
  - Slowing down means fewer rabbit holes
  - Again: You have two minds tackling a problem

But downsides...it's usually frustrating.  Or it can be. Here were some tips on pair programming that Sumeet gave us:

> - Take a break every now and then. Make a rule: Every 22 minutes, you switch typists and the new typist shares one interesting/funny/weird (and appropriate) video before you begin coding again.

I really like this rule.  The 22 minutes especially stuck in my head.  We literally set a timer. At 22 minutes, the typist is usually *ready* to switch because it's hard to think and listen and type all at once.  The non-typists have the easier job.  And 22 minutes is also super specific.  If you say, '20 minutes', what you'll think in your mind is 'about 20 minutes', which could be anywhere between 20 and 40 minutes.

Really switch at 22 minutes!  And break after three switches.  It was really the perfect shcedule.

> - Try communicating your frustrations with each other.

I love this rule too.  Sometimes you think, "Ugh!  This person!  They won't listen to me!"  But what they're thinking is, "Ugh!  This person!  I wish they would communicate more!"  Or something.  Or neither of you can solve the problem.  And it's frustrating!

Sharing the frustration is a bonding experience.  It defuses tension.  It allows you to be on the same team, with your mutual frustration of having to work together being the thing you both hate, not each other.

> - But also recognize that not all frustration is the fault of others. What can you do to decrease the tension...?

Heh.  Yeah.  Do this too.  Remember, it's *probably* you.  At least a little.  That's what you can control anyway.  Do what you can about it.

Our group was great.  I learned a lot from Nick and Andrew today.  We had several different approaches, so it was eye-opening in that I wouldn't have attempted that way, and it was cool to explore how to tackle the same problem in different ways.  We got a lot out of stretching ourselves.  

But perhaps because the work was more challenging or three was harder than two or because it was the second day of pair programming in a row or because I had a bad night of sleep last night...

Man, I am dead tired today!  *lol* Going to sleep.  

Today was a good day.  And it was a satisfying experience to learn something that I know we'll use 100 times.  I feel like with ruby and Sinatra and HTML and css and now javascript, we've been given the keys to the kingdom.  And now it's just a matter of learning all about the kingdom! No pressure! ;)

*I cannot help humming the Rubbery Ducky song when somebody mentions rubber ducking.  Since I'm singing it, I thought I'd share this with you.
  <iframe width="420" height="315" src="https://www.youtube.com/embed/Mh85R-S-dh8" frameborder="0" allowfullscreen></iframe>