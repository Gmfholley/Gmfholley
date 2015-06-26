---
layout: post
title:  "Dinner Club"
date:   2015-06-03 09:10:41
categories: ruby classes sample-code
---
#Assignment

We're at mid week of our first week at Omaha Code School.  The assignment has gone through a few iterations and re-factoring.

We should create a DinnerClub class, which keeps track of members, who pays each of the club's outings and how much each person has paid since they began.

The DinnerClub uses the CheckSplitter class to calculate tip.

DinnerClub and CheckSplitter should each have tests.

# Dinner Club
At first, the DinnerClub's only instance variable was a Hash that stored the member's names as keys and their balance as values.

Sumeet assigns "stretches" as the days go on, though.  One of his first stretches was that the people who attend an event might not be the people who pay.

I decided I needed an Event class. An Event captures attendees (Array), payees (Array), bill (Float), tip (Integer), location (String), date (Date).  The Array of Events is DinnerClub's only instance variable.

To get information on the members, I loop through the @events Array.

When a dinner club is initialized, the array of Events is initialized to an empty Array.  You do not need to pass any arguments into the Dinner Club.

```ruby
  def initialize()
    @events = []
  end
```

You can add events to the club, either using the arguments needed for an Event object, or passing an Event object itself.



```ruby
  def add_event(args)
    this_event = get_event_object(args)
    save_event(this_event)
    events
  end
```


`get_event_object` will either create the event object if it is not already passed as args or send it back if it is already an event object.

`save_event` saves the event into the events Array.
These two methods are utility methods.  I only mention them so that the user knows that they have flexibility about how they pass parameters to add_event.

The user can call the following public methods to get information about members:

  - `get_members_balance` (name)     --> takes a string of "name" and returns a float of their balance
  - `get_member_list`                --> returns an Array of all members from all events
  - `get_each_members_balance`       --> returns a Hash of all members and their balance 
 
These three methods all loop through the array @events to get the information requested.  `get_each_members_balance` calls `get_member_list` and `get_members_balance` to construct its Hash.

Behind the scenes, DinnerClub is calling a helper class, CheckSplitter, to split the check among the number of payees.

## Event

The event class keeps track of each of the dinner club's events.

  - attendees     --> Array of names of attendees
  - bill_amount   --> Float of the bill
  - tip_percent   --> Integer of the tip (if already in decimal form, will be converted by CheckSplitter)
  - payees        --> Array of names of those who pay - defaults to the same as attendees if not provided
  - location      --> String of the location  - defaults to "not provided" if not provided
  - date          --> Date object - defaults to today if not provided

```ruby
def initialize(args)
   @attendees = args[:attendees]
   @bill_amount = args[:bill_amount]
   @tip_percent = args[:tip_percent]
   if args[:payees].nil?
      @payees = args[:attendees]
   else
     @payees = args[:payees]
   end
   
   set_location(args[:location])
   set_date(args[:date])
 end
```
 
Event's methods are mainly to set default values for the arguments.  I considered calling CheckSplitter directly from Events.  But I decided to let DinnerClub handle it because then DinnerClub is responsible for knowing about both CheckSplitter and Events.  There's less chance that DinnerClub breaks because I change the Events class or CheckSplitter later.

### CheckSplitter
I marked this code up already.  Find an explanation [here.](./checksplitter.html)

#Links
[Here](https://gist.github.com/Gmfholley/35d28cd3cb656275b4b3) is my complete code with app.rb driver file.

If you want to play, I've also posted it to [repl.it.](http://repl.it/t59/3)