---
layout: post
title:  "Building Our First Model"
date:   2015-06-12 09:10:41
categories: ruby models sql sqlite3 week-two
---
Model...airplane?  Fashion model?  Model of the solar system?

No!  Apparently, if you add database design/functionality to a class in Ruby, you call it a model.  (I also have the sneaking suspicion, it has something to do with the Model-View-Controller design I heard mentioned at the Ruby Lightning Talks Meetup, but I am told we will learn more about this when we get to Ruby on Rails.*)

So yesterday, we built a really simple model (and actually, I didn't actually build a model.  I stopped at building a module that could be included in a class, which would then become a model).  


#Assignment
Today, actually, the whole weekend's assignment, is to build a Product Inventory Manager with three models.

(Whenever I hear, "Your assignment for the weekend...yada yada yada", I hear, "This project will be extremely difficult."  Just to keep that in mind.)

>An inventory management system is a tool that a shopkeeper might use; it lets you keep track of everything you have in stock, and is useful when you have several different places whose stock you're managing so that you can make sure everyone has what they need.
> ...
>Here's what we've got:
>
> -    Some number of locations (shelves, bins, buildings, etc.)
> -    Some number of product categories (e.g. books, movies, death rays, etc.) or classifications (manufacturer?)
> -    Some number of products, each with a serial number, name (optional), description, cost, and anything else you like
>
>Each product has a category and lives in some location. Many products can share the same category and many different products can be in the same location.

Here are my models:

Movie Class stored in movies table

 - id | Name | Rating | Studio | Length | Description
    - Rating and Studio are Foreign Keys
    
Location Class stored in locations table

 - id | Name | Number of seats  | Number of staff  | Number of movie slots per day|

LocationTime Class stored in location_times table

 - Location |  TimeSlot |  Movie  |  Number of Tickets sold
   - Location & TimeSlot are composite key
   - Location, TimeSlot, and Movie are Foreign Keys

Rating Class stored in ratings table

 - id | Rating

Studio Class stored in studios table

 - id | Studio


TimeSlot Class stored in timeslots table

 - id | TimeSlot



Six models.  Not the three required.  I had wanted to keep my models nice and simple, just movies, location, and ratings.  But looking ahead at the assignment where you must be able to have many Movies in a single location (which works well with books and shelves), the only way that works for movie-locations is if you play the many movies at different times.

So my LocationTime class has a composite key.  Let's hope that doesn't get me into trouble.

*coding coding coding*


*Spoiler alert: It does!