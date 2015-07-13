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

Movie Class stored in movies table                Foriegn Key   |  Foreign Key
ID    |  Name                                  |   Rating       |   Studio          |  Length  |  Description
------|----------------------------------------|----------------|-------------------|----------|-------------
	1		|	Avengers: Age of Ultron		             |	PG-13			    |  Marvel Studios		|	160      | In a world!
	2		|	Kingsman: And there is a colon		     |	R		    	    |  20th Century Fox	|	129      | Some movie I don't know.
	3		|	Guardians of the Galaxy		             |	PG-13			    |  Marvel Studios		|	121      | Chris Pratt!
	5		|	Boyhood		                             |	R		      	  |  IFC Productions	|		165    |   A boy's life.
	6		|	Frozen		                             |	PG		  	    |  Disney		        |	91       | Let it go!
	7		|	Inside Out		                         |	PG		  	    |  Pixar		        |  	89     |   I like Pixar.
	8		|	Indiana Jones and the Temple of Doom	 |	PG		  	    |  Paramount		    |  	118    |   True classic.
                                                                |
  
  
Location Class stored in locations table
ID| Name    | Number of seats  | Number of staff  |   Number of movie slots per day
--|---------|------------------|------------------|--------------------------------
1	| Purple	|   300	           |    2	            |      5
2	| Red	    | 300	             |  2	              |    3
3	| Yellow	|   200	           |    2	            |      5
4	| Green	  | 200	             |  2	              |    5
5	| Gold	  |   100	           |    1	            |      4
6	| Blue	  |   100	           |    1	            |      3
7	| Orange	|    50	           |    1	            |      6
8	| Silver	|    50	           |    1	            |      2
9	| Shamrock|	 300	           |    2	            |      90
                               
 
 
LocationTime Class stored in locationtimes table
Composite Key   |  Composite Key|
Foreign Key     |  Foreign Key  |   Foreign Key                             |
Location        |  TimeSlotslot |       Movie                               |      Number of Tickets sold
----------------|---------------|-------------------------------------------|-----------------------------
Purple			    |  12:00:00			|  Avengers: Age of Ultron                  |
Purple			    |  22:00:00			|  Avengers: Age of Ultron                  |
Purple			    |  17:00:00			|  Avengers: Age of Ultron                  |
Red			        |  12:00:00			|  Kingsman: And there is a colon           |
Yellow			    |  12:00:00			|  Kingsman: And there is a colon           |
Shamrock			  |  12:00:00			|  Frozen                                   |
Shamrock			  |  14:30:00			|  Avengers: Age of Ultron                  |
Silver			    |  12:00:00			|  Indiana Jones and the Temple of Doom     |


Rating Class stored in ratings table
id    |  Rating
------|----------
1     |  G


Studio Class stored in studios table
id      Studio
-----|---------
1    |  Paramount


TimeSlotslot Class stored in timeslots table
id  |    TimeSlotslot
----|------------------
1   | 12:00 pm


Six models.  Not the three required.  I had wanted to keep my models nice and simple, just movies, location, and ratings.  But looking ahead at the assignment where you must be able to have many Movies in a single location (which works well with books and shelves), the only way that works for movie-locations is if you play the many movies at different times.

So my LocationTime class has a composite key.  Let's hope that doesn't get me into trouble.

*coding coding coding*


*Spoiler alert: It does!