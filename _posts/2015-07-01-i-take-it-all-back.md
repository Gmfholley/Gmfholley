---
layout: post
title:  "I take it all back - I definitely cannot do this"
date:   2015-07-01 09:10:41
categories: css
---

Yesterday felt...almost...ok.  Like, ok, if a designer gave me pictures of what a website looked like, I could piece together something that looked pretty close.

Today, we were designing the exact same BarCamp website.  Only this time, we were making it for a slightly wider mobile screen.  And from the narrow to the wider version, it should expand.

Sure, sure.  I think I can handle that.

But (twist!), the assets (pictures) are from the actual BarCamp website.  I hadn't noticed this, but the very first section consists of FIVE different pictures, all layered on top of one another.  Here is the web site.

<img src="http://gmfholley.github.io/2015-07-01-hero.png" style="text-align: center">

And here are each of the layers.

<img src="http://gmfholley.github.io/2015-07-01-mountains.jpg" style="width: 25% padding: 10px display: inline">
<img src="http://gmfholley.github.io/2015-07-01-lake.png" style="width: 25% padding: 10px display: inline">
<img src="http://gmfholley.github.io/2015-07-01-trees.png" style="width: 25% padding: 10px display: inline">
<img src="http://gmfholley.github.io/2015-07-01-hero_logo.png" style="width: 25% padding: 10px display: inline">




Wha- eh wha?

Also...WHYYYYYYYYYY? (Ok, setting aside momentary panic.)

And then, notice this effect as the browser window gets wider.  The entire logo remains centered within the viewing window.  It is set to a specific width, yes.  But it is *centered* within that width.  So you see more and more of the sides of the shot until it reaches a certain width, and then it expands with the size of the window.

![Bar Camp Shrinks]({{http://gmfholley.github.io}}/2015-07-01-bar-camp-shrink.gif)


Sumeet did warn us that the very first section was the very hardest section.  And to maybe try the easier parts first, to make progress.  I did not do that, since most of the rest of my site worked okay with a slight increase in browser width.  

So join me in chiding this silly Wendy, who should have followed directions maybe, hmm?  I might have felt a midge more accomplished and a mite less dispirited.

But...omg...I could *not* figure out how to get the dang layers to stay on top of each other, in the correct dimensions, *and* centered.  Just would not stay!

I am cribbing from the original BarCamp site like a mad woman, and googling all the shit they did to figure out what it means, but I don't understand parts of it, I'll be honest.  I feel like yelling at the css. I just want you to center?  Why isn't that something I can tell you to do?  WHY ARE YOU DOING THIS TO ME?

Tomorrow is another day.  That's what I'll cling to.  [Here's my sad little BarCamp 2.](https://github.com/Gmfholley/07-01-css-barcamp)