---
layout: post
title:  "Aaaaaaactive Record"
date:   2015-07-16 09:10:41
categories: activerecord sql databases ruby gem
---

It is time!  We are here.  And we are finally learning about what we have heard about for so, so long.

ActiveRecord is the gem (or the set of gems) that runs SQL commands through our SQL database (SQLite or PostgreSQL or whatever database type we are using).  ActiveRecord is awesome because it:

- validates data types
- creates associations
- makes complicated SQL calls

And today, we are using it!

I think the hardest thing to understand are the ActiveRecord macros that create associations between models.

For example, for a situation like users and posts...

```ruby
class User
  has_many :posts

end

class Post
  belongs_to :user
end
```
`has_many` seems pretty self-explanatory.  `belongs_to` in my mind pricks my ears as meaning `has a foreign key`.  And what this does is create a method in User called posts, and a method in post called user.  Plus a whole lot more methods that allow you to perform CRUD operations on the association.

So to write it out.

```
class User
  has_many :posts
  # equivalent to
  # def posts
  #   Post.where(user_id: self.id)
  # end
end

class Post
  belongs_to :user
  # equivalent to
  # def user
  #   User.where(id: self.user_id).first
  # end
end


```


But in addition, there are `has_and_belongs_to_many` associations and `has_many, through` relationships.  Which are really just the difference between a many-to-many relationship through a bridge table or through a model.  But which, to clarify in my own mind, I drew out. 

<p style="text-align: center;"><img src="/assets/2015-07-13-active-record.png" alt="grandfather telling it to fred savage"></p>


I'm excited!  ActiveRecord has been talked up since we learned about models.  It's rare that the Gem is Everything You Wanted...And More!

Before we leave, can we raise a glass to my poor and now thoroughly defunct `database_connector` module?  Because, it was pretty awesome, right?  Let me count the ways...
 
 - it validated data too!  By looking at the data types in the database and calling post-initialize and valid? method hooks!
 - it translated an object into JSON!
 - it used a ForeignKey class to create association methods
 - it used the ForeignKey class to get association choices!
 - it stored the fields you wanted to display vs. the fields that were attributes
 - it performed basic CRUD for you, at the class AND instance level

All in all, except for the complicated SQL calls, it did a lot of what activerecord does...if pretty inefficiently.  I'm going to miss you, [`database_connector` module](https://github.com/Gmfholley/07-13-API-Project/blob/master/database_connector.rb).  You and I were dear, dear friends.