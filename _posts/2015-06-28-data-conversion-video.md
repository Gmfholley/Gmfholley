---
layout: post
title:  "Refactoring: My Solution for Data Type Conversion in Models"
date:   2015-06-28 09:10:41
categories: ruby sinatra orm video `data_conversion`
---

Now that we're using Sinatra, every value comes back as a string.  So for certain instance variables (but not the ones that should be strings!), I had to convert strings to integers/floats in my initialize methods.

I also had hella long valid? methods in most of my models.  The valid? method is run right before I attempt to save to the database and prevents a save in the case of bad data.  For example, here was the previous valid? function for one of my simplest models:

```ruby
  # returns Boolean if data is valid
  #
  # returns Boolean
  def valid?
    @errors = []
    # check thename exists and is not empty
    if name.to_s.empty?
      @errors << {message: "Name cannot be empty.", variable: "name"}
    end
    
    # checks the point base
    if point_base.to_s.empty?
      @errors << {message: "Point base cannot be empty.", variable: "point_base"}
    elsif point_base.is_a? Integer
      if point_base < 1
        @errors << {message: "Point base must be greater than 0.", variable: "point_base"}
      end
    else
      @errors << {message: "Point base must be a number.", variable: "point_base"}
    end
    
    @errors.empty?
  end
```

Ugly, right?  But I didn't know how to make this cleaner.  Breaking it into smaller methods would just hide the fact that I was doing this in _every_ model. It wasn't DRY (Don't Repeat Yourself).

I asked Sumeet for help, and he suggested some kind of hook to handle all my validation checks.  The same technique was used to convert data into the correct type in initialize methods.

I updated my code.  Here is a video of my solution below.

<iframe width="420" height="315" src="https://www.youtube.com/embed/9LISUPi2l7Y" frameborder="0" allowfullscreen></iframe>