---
layout: post
title:  "Using Modules to Connect Classes to a Database"
date:   2015-06-16 09:10:41
categories: ruby third-week sql sqlite3 modules mix-ins models database
---

We have been working on our Database project since last Thursday.

Because of my experience creating applications in VBA, I understood that we would be adding the same database functionality to all of our classes, basically a copy and paste of the same functions but changing the variable names.*  But I didn't know how to DRY (Don't Repeat Yourself) up that code in VBA.

But with all we've been learning in ruby, I felt like I had new tools in my toolbox and time to experiment with them.

So in the early design stages, I thought, "Hey, this should be a module!"  Below, I explain how my module works.

<iframe width="560" height="315" src="https://www.youtube.com/embed/bpLx_3QTBJc" frameborder="0" allowfullscreen></iframe>


* Note: I wasn't working with databases in VBA.  Rows in spreadsheets. But same idea. :)