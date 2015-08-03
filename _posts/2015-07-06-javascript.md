---
layout: post
title:  "A new programming language: how do I even get started?"
date:   2015-07-06 09:10:41
categories: javascript how-to-learn-a-new-language how-to-code
---
##Say hello to curly braces!  Javascript

Today, we're learning a new language - javascript.  I've attempted to learn four or five programming languages before* - python, java, c++, c#, and of course VBA, which until a few weeks ago was my preferred language.**


## Rabbit holes for new programmers
I think there are three major rabbit holes people fall into when they are trying to learn a new language (or trying to learn their first programming language.)  I've fallen victim to all three of them.

  - 1. The set up is too hard.

This sounds like a silly problem, but it is critical.  If you can't set your computer up to run the programs you'll create, you'll never get to the actual *programming*. I am talking about it taking *hours* to configure on your specific computer, especially if you don't know why you're doing what you're doing.

Some books/guides start you off by downloading the text editor, setting up your folders using command line (itself a new language!), and skimming past what an editor and compiler are doing.  The reason this is skimmed over is that command line and config settings and compiler/debuggers are skills and programs that could take up a whole book themselves.  

If it works, great.  Do not get distracted by this!

But half the time, I know this was the step (the very first step!) that I would get stuck on.

  - 2. Boring yourself

My approach to learning new languages was always pretty much the same.  Buy a book.  Work through it.  Something like "Learn Java in 21 days" or the incredibly awesome Learn ____ the Hard Way series (which are free!).

This isn't really a bad plan, and there is nothing wrong with these books. But for those that know some programming (and even for those who don't), those books are typically incredibly dull to start.  Ugh, data types.  "Two pages on the difference between an integer and a float? Really?"  Ugh, variables.  "Yeah, I get the concept.  I took basic algebra."  Loops?  "Yeah, ok.  It's not like this is alien DNA or something.  May poles. Track.  Nascar." 

And the books are also typically too thorough later on.  They cover all the ways the language can be used - from folders and files to software to web.  "It's not like this is hard, but why are there three chapters on how to read a text file?  My company uses a database."

So I went to the other extreme...

 - 3. Skipping the Boring Bits

Because I know what I'm doing!  Totally.  So I would pick something I really *wanted* to do, and decide to do it in the new language.

This isn't really a bad plan either.  But I skipped right to this part.  And then I was looking things up left and right.

Wait, how do I make a for loop in this language again?  Wait, does this language need a semi-colon at the end?  Will this language allow += syntax or not?  What do you mean, you won't compile?

And I would grow frustrated and think, 
  
  "Why am I doing this anyway?"  

  "Why do I do *anything*?"
  
  ...Long existential freak out later...

  "Let's code this in the language I already know."

##How Code School does it

What I *really* like about the way Omaha Code School approaches languages is that they save you from all three rabbit holes.

 - Solution 1)

The set up was what we learned *last* at Code School. \(With help.  From experienced techies.\)  That is how it should always be.

For the prep work before class, Omaha Code School sent us to [this awesome site - repl.it](http://repl.it/languages), standing for Read Evaluate Print Loop.  It's free.  Choose your language, type in your code on the left side, hit run, and out it spits on the right.  You can create an account to save your code or copy and paste it into your own files to use later.  Genius.  _Use this!_

 - Solution 2)

When we did the prep work for this class, a lot of it was like those boring books. Lots of learning to use variables.  Lots of work on different loops.  But I think the genius was the mixing of difficult logic problems with basic syntax.  After the initial few problems, you were solving challenging logic problems, and learning ruby syntax was just a byproduct. 

For example, Week Two's practice problems were about loops. The first few problems are pretty standard...

>1. Write a program that uses a loop (any type) to count from 1 to 10 on-screen.
>2. Write a program that uses a loop (any type) to count down from 10 to 1 on-screen.

But then the last few problems are:

>17. Implement the [divisibility by 7](http://www.aaamath.com/div66_x7.htm) check. Check your work by using the % operator.
>18. Implement the [Luhn Algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm). Test it against your own credit card number.
>19. (Advanced) Implement the Taylor Series out to 7 terms for sin(x) and cos(x). Compare this with Math.sin() and Math.cos(). Even if you haven't taken Calculus II, this problem should still be approachable, though may require some extra work (as a hint, look up the Taylor Series and implement it rote, instead of deriving it by hand). For fun, see how many terms you have to go out to before the rounding error is less than 0.001.

I had never heard of the Luhn Algorithm.  It has been a long time since I worked on the Taylor Series.  And even if I had solved these problems before (in math or physics for example), I hadn't attempted them in code, which sometimes requires a completely different approach to the problem.

These problems would be a fun challenge in any language.  But it was also perfect, because these problems in particular require only a few basic Ruby skills.  They sneakily encouraged me to use pretty boring skills for something pretty cool.

And by the time I was done, I felt satisfied *and* I knew ruby loops.

 - And Today: Solution 3)

Now that we *know* a language really well \(ruby\), we shouldn't take so long to learn a new language.  But we can't be thrown in either or we'll get frustrated and distracted, and we won't learn the syntax.  

So today, Sumeet's advice for learning a language *now* is really simple. Spend the afternoon \(just the afternoon\w) learning how to do all the basic things by heart.

 - How to create variables in this language
 - How to display Output 
 - How to get Input from a User
 - Basic Math
 - Conditionals
 - Basic Loops
 - Input Validation with Loops

It isn't that hard.  And it's only that much.  [Here are my Atomics](https://github.com/Gmfholley/07-06-javascript-atomics). 

And tomorrow, we'll get thrown into more exciting projects, that, yes, will be in javascript!  :)  Can't wait.

##One last piece of advice for new programmers

Which is going to be a bit hypocritical, forgive me.

_Don't listen to advice._

There is so much conflicting advice about what to start with and how to learn and what the basics are.  Pick a language that is still in use.  Pick a guide or a book or a website.  Learn it.  Stick to it.  Don't get distracted by feeling that you should really be learning something else *first* or *too*.  There is plenty of time for that after.  In fact, if you program, you will be learning for the rest of your life.

And now here's my pep talk:

Do it.  The first is the hardest.  You're learning to program as well as a language.  Allow it to be hard.

Know that it gets easier.  

It gets a LOT more fun.

Ask for help, but don't forget that Google is often the best resource.  (For reals.)

Do it.

Do it.

Do it.

### Footnotes
*Brief digression on my very first programming language:

  I am revealing my age here, but [Hypercard](https://en.wikipedia.org/wiki/HyperCard) was actually my very first programming language.  _Back in the day!_  I took typing, Latin, and French, and programming each for a quarter in junior high.  Hypercard, as I remember, was like a cross between paint, HTML and PowerPoint.  You created static cards, programmed the links between them, and could even do some programming on the back end to create animated effects or simple logic games.  The file sizes (for computers of the time) got bloated very quickly, so many of the games were in black and white with hypercard-drawn images, so even the most advanced products had an amateurish vibe.  

  Our favorite time-waster in the typing class was a Hypercard game similar to space invaders.  A plane and a wagon full of hay cross the screen at different speeds.  Speed increased as time went on, and the plane gradually descended. You had to time the exit of parachuting troops from the plane so they landed in the hay or they died.  I would time myself to finish the typing in 20 minutes so I could play this game.  I couldn't find this particular game, but [this site](http://macintoshgarden.org/engine/hypercard) of Hypercard games brings back a lot of memories.

**Ruby, beautiful, expressive ruby, you are my favorite now.  Just this week, I broke my VBA code by ending a conditional with just 'End' instead of 'End If'.  Sorry, VBA.