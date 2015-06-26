---
layout: post
title:  'First Day - CheckSplitter'
date:   2015-06-01 09:10:41
categories: ruby classes sample-code
---

#Assignment

Our first day of Code School!  Sumeet is throwing us right in.

The assignment is to create a class called CheckSplitter.  It should take as inputs the amount of a bill, an optional tip, and the number in the party.  It should return how much each person should pay.

#My code
CheckSplitter takes three parameters:

  - `size_of_party` --> Integer, or if not an integer, will be set to 1
  - `bill_amount`   --> Float of the bill - or if not a float, will be set to 0
  - `tip_percent`   --> Integer of the tip - defaults to 18

```ruby
  def initialize (args)
   `set_size_party`(args[:size_of_party])
   `set_bill_amount`(args[:bill_amount])
   args[:`tip_percent`].nil? ? `set_tip_percent` : `set_tip_percent`(args[:`tip_percent`])
  end
```

The parameters are passed in an optional Hash so that if I change the number or name of parameters later, I can do that just by changing my initialization method.

The `set_size_party`, `set_bill_amount`, and `set_tip_percent` are utility methods to set default values or correct for incorrectly inputted values.  

For example, `size_of_party` is set to 1 if a user passes a value that is a string or 0, so that the calculation of `each_persons_split` is not infinity.

My goal is this: the code should not break.  It may not return a value that is meaningful, but it shouldn't break.

The user will probably only use the `calculate_per_person_share` method.  `num_persons`, if not provided, defaults to the `size_of_party` but can be set to another value (for example, to accommodate a party who treats a birthday girl).  

`calculate_per_person_share` calls a utility method, `calculate_total`, that has calculated the final bill + tip.  `calculate_per_person_share` returns a Float rounded to two decimals.  

The `calculate_per_person` method is below.

```ruby
  #Calculates each person's share
  #
  #num_persons - Integer representing how many people split the check
  #
  #returns Float, rounded to two decimals
  def calculate_per_person_share (num_persons = @size_of_party)
   (calculate_total / num_persons).round(2)
  end
```

Note on Ruby's rounding method: Ruby removes trailing 0 decimals on a float.  But it signifies a float by providing one trailing 0 after a decimal.  

So for example...

```ruby
  total = 30.00
  total.round(2)
  => $30.0

  total = 33.33333333333
  total.round(2)
  => 33.33  
```

#Links
[Here](https://gist.github.com/Gmfholley/35d28cd3cb656275b4b3) is my complete code with app.rb driver file.

If you want to play, I've also posted it to [repl.it.](http://repl.it/t59)