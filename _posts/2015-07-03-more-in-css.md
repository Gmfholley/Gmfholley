---
layout: post
title:  "More css"
date:   2015-07-03 09:10:41
categories: css
---
It is Friday, July 3rd, and we have a three-day weekend.  And the homework is more css.  

I can feel css slowly become, if not friends, casual acquaintances that can tolerate each other for lunch.  Wine helps.  (No, it doesn't.  And I prefer beer.)  

I discovered a couple of cool tricks.  Over Slack, [someone posted this article on someone's tiny game where the source code can fit in a tweet.](http://boingboing.net/2015/06/30/tiny-twitch.html)  This game is so pretty awesome, and I couldn't come close to matching it.  But it was a nice break from trying to create the appearance of the internet, which I find both tedious and frustrating.

Plus, my challenge was to create a game using css!  Killing two birds!  [Here is my attempt at creating tiny games](https://github.com/Gmfholley/07-04-tiny-games), and here is one of my tiny games in action.
<img src="/assets/2015-07-03-transition.gif" alt="Tiny css game" style="display: block; text-align: center;">

I learned how to use the transition effect.  Here is my code:

```html
  <style>div,a{background:red;}div{width:9;float:left;transition:width 1s}div:hover{width:100%}</style><div>*</div><a>Not Me</a>
  <a>Kick Off
```

As you can see, I didn't follow best practices. :)  But I thought the transition css effect was pretty cool.

No, the real homework was to copy boxes from other web sites.  And again. And again and again and again.

Here are some of my boxes:

<img src="/assets/2015-07-03-gmail.png" alt="gmail inbox" style="display: inline-block; text-align: center;">
<img src="/assets/2015-07-03-ny-times.png" alt="ny times article" style="display: inline-block; text-align: center;">
<img src="/assets/2015-07-03-twitter.png" alt="twitter masthead" style="display: inline-block; text-align: center;">
<img src="/assets/2015-07-03-blog.png" alt="blog entry" style="display: inline-block; text-align: center;">
<img src="/assets/2015-07-03-blog-with-pics.png" alt="block article" style="display: inline-block; text-align: center;">
<img src="/assets/2015-07-03-side-bar.png" alt="blog side bar" style="display: inline-block; text-align: center;">

I think what I learned learned most is not to use the tags to describe any css element, if it could be helped. My Ruby mind had been thinking, "Ok, you have an object called h3, and you can make it have any attributes you want.  And then you just re-use h3 whenever you want those things."

But no, a web page is a big place.  You will use h3 again, in unexpected places.  Places that should look and behave nothing alike.  You don't want to be confused. 

Ids are okay.  Classes are best.

Focusing on making small parts of a website was far less daunting than trying to build an entire one from scratch, but all websites can be built piece-by-piece like this.  Yes, there are parts that you will duct tape together and won't understand and will break next time you make a change.  That's okay too.  Expect it to happen.  Make it part of the plan.

Sometimes simply adding a paragraph of text above or below my boxes broke them.  That was a sign that I hadn't completed them entirely.  It was a good test.  So I added paragraphs above and below all my elements to make sure I was building them correctly.

I'm no css expert.  (Nor, do I think, do I want to be.)  But parts of it are really cool.  This is just scratching the surface.

And last and most importantly, I love cats. : )