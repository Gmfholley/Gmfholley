---
layout: post
title:  "Why I Love Args"
date:   2015-06-20 09:10:41
categories: ruby sql sinatra hashes
---

Before I started the class, Omaha Code School sent us a list of problems as prep work.  The basics taught us how to create variables, employ operands, use loops, and the very basics of classes.  

Because I've coded in VBA extensively and some in Java and C#, most of this was familiar terrain for me.  But the real differences were:

  - As a dynamically typed language, I did not have to state what any variable was and I could change its type at any time!
    - Arrays of anything!  Or multiple somethings!  It's like a collection, except better!
    - The flip-side of which is that nothing is compiled.  :( I miss the debugger.
  - Syntax!!!  
    - Good-bye semi-colons at the ends of sentences!  
    - Good-bye parentheses around conditionals!  
    - Everything except Classes and Modules in lower case!
      - `always_use_snake_case`
      - noCamelCaseAnyMore.
    - Hello, legibility!
  - Hashes?  Omg, this is amazing.


I fell _in love_ with hashes.  How useful!  What a fantastic look-up table.  What a great way around the problem of multi-dimensional arrays!  Huzzah!  

I started using them for everything I could.  And Sandi Metz's [Practical Object Oriented Design in Ruby](http://www.poodr.com/) showed me why they might be important in the initialize method.

>In the following example, `Gear`'s initialize method takes three arguments: `chainring`, `cog`, and `wheel`.  It provides no defaults; each of these arguments is required.  In lines 11-14, when a new instance of `Gear` is created, the three arguments must be passed and they must be passed _in the correct order._

```ruby
  class Gear
    attr_reader :chainring, :cog, :wheel
  
    def initialize(chainring, cog, wheel)
      @chainring = chainring
      @cog = cog
      @wheel = wheel
    end
    #....
  end
```

>Senders of new depend on the order of the arguments as they are specified...If that order changes, all the senders will be forced to change.  Unfortunately, it's quite common to tinker with initialization arguments.  Especially early on...

And I immediately thought, of course!  Sandi shows how to use args and pass the arguments as a Hash, _in any order and missing any or all of the variables._

```ruby
  class Gear
    attr_reader :chainring, :cog, :wheel
    
    def initialize(args)
      @chainring = args[chainring]
      @cog = args[cog]
      @wheel = args[wheel]
    end

  end

  gear = Gear.new(cogs: 4, wheel: Wheel.new(26, 1.5), chainring: 52)
```

Or any other combination we could think of!!

I used args from the start.  It was so flexible and functional that I found it met needs in unexpected ways.  For example, when we started using the sqlite3 gem, how does the gem return the fields and names of a database to us?

```ruby
  
  > results = CONNECTION.execute("SELECT * FROM locations WHERE id = 2;")
  => {"id" => 7, "name" = "Burger King"}

```

Woo hoo hoo!  And look at how awesome that is to place right into the new method and create an instance of the object!

```ruby

  `burger_king` = Location.new(results)
  => #<Location:7898790382jfl;a
  @id = 7
  @name = "Burger King">

```

This is amazing!  It's as though sqlite was planned with me in mind!

Guess what?  Sinatra does the same thing!  So if you have your html file

```html
<form action="/submit/location">
  <input type="hidden" name=my_location["id"] value=@id>
  <input type="text" name=my_location["name"] default="Type in your location here">
  <input type="submit" value="Update your location.">
</form>
```

How does that come back to the router?

```ruby

*From:* /Users/.../Code/...this_program.rb @line 15 self.GET "/submit/location" 

  14: get "/submit/location" do
=>15:   binding.pry
  16:  # some code here...we'll see what sinatra returns in params first
  17: end


[1] pry(#<Sinatra::Application>)> params
=> {"my_location"=>{"id"=>"7", "name"=>"Burger King"}}
```

Omg omg omg, another hash!  And you can send *that* hash right into your initialize method too!  (Although we'll still have to somehow convert that id to an integer.)

We're also still building our database connector module.  I know it's not `active_record` (which we will get to soon, Sumeet tells us), but I want it to have some functionality.  And for that, I need to be able to cycle through all of an object's parameters so that I can insert into the database automatically.  The SQL call to insert requires the column names to start with:

```SQL
  INSERT INTO `table_name` (column1, column2, ... column n) VALUES (value1, value2, ... valuen);
```

But how do I get the names of the columns? 

Well, I discovered this really cool little method:

```ruby
 > `some_location.instance_variables`
 => [:id, :name]
```

But what you might notice is that this is an instance method.  Usually, when you're inserting into a database, you want to be able to create a new object, so you want a Class method.  But if for example, you're trying to allow a user to create a new location, you need to know the instance variables that the user needs to fill in, so you can create fields for the user.  

Well...look what happens when you use args but with no real data!

```ruby
> args = {}
=> {}
> n = Location.new(args)
=> #<Location: #4839jk;ji98-8
@id = nil,
@name = nil>
> `n.instance_variables`
=> [:id, :name]
```

How sweet is that?  Now you can use this Array to create input fields in html or create a loop in the command-line's driver and loop through all this object's parameters so that your user can enter data for every parameter.

*hugs self* _I love args! :)_