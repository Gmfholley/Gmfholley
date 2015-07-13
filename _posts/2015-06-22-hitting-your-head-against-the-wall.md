---
layout: post
title:  "When You Find Yourself Banging Your Head Against The Same Wall...Stop"
date:   2015-06-22 09:10:41
categories: ruby models database sql week-four sinatra
---

So I worked all weekend on trying to update my Database Theatre Manager project from a Command Line UX to a web UX using Sinatra.

I had two main problems.  Several models had Foreign Keys as instance variables.  How to make sure that: 
  1. the user could only choose Foreign Keys that already existed in the database.  It would be cool if this were in a drop-down field on the web,
  2. the value displayed for the user wasn't the Foreign Key itself, which is usually just a number, but, say, the name of the Foreign Key.  Something that makes sense to a human.

So...I created a ForeignKey class.  It stores the id of the Primary Key, the name of the Class to which it belongs, and an Array called errors*, which stores whether this is a good Primary Key or not.

```ruby
  class ForeignKey
  
    attr_reader :class_name, :field_in_table, :errors
    attr_accessor :id
  
    def initialize(args={})
      @id = args["id"] || args[:id]
      @id = @id.to_i
      @class_name = args["class_name"] || args[:class_name]
      @errors = []
    end

   #...
  end
```

ForeignKey also has a method to check if this is a valid ForeignKey.

```ruby
  # returns boolean if there are no errors
  #
  # returns Boolean
  def valid?
    @errors = []
    if id.blank?
      @errors << {message: "#{class_name} id cannot be blank.", variable: "id"}
    elsif !possible_values.include?(id)
      @errors << {message: "#{class_name} id must be included in the table.", variable: "id"}
    end
    
    if class_name.blank?
      @errors << {message: "Class cannot be blank.", variable: "class"}
    end
    
    @errors.empty?
  end
```

So that's fine and that's all working.  Now my DatabaseConnector modules (for class and instance methods) can get an Array of ForeignKey variables/fields and non-ForeignKey variables/fields.  Plus a list of all possible choices for a ForeignKey so I can populate a drop-down.

```ruby
  # returns an Array of foreign key fields (if any)
  #
  # returns an Array
  def foreign_key_fields
    keys = []
    database_field_names.each do |param|
      if self.send(param).is_a? ForeignKey
        keys << param
      end
    end
    keys
  end
  
  # returns an Array of all non-foreign key fields
  #
  # returns an Array
  def non_foreign_key_fields
    self.database_field_names - self.foreign_key_fields
  end
  
  # returns an Array of the Foreign Key objects for this object
  #
  # returns an Array
  def foreign_keys
    vals = []
    foreign_key_fields.each do |field|
      vals << self.send(field)
    end
    vals
  end
  
  # returns an Array of Arrays, containing all possible choices for the Foreign Keys
  #
  # returns an Array of Arrays
  def foreign_key_choices
    choices = []
    foreign_keys.each do |foreign_key|
      choices << foreign_key.all_from_class
    end
    choices
  end
```

And I can use these Arrays of `foreign_key_fields`, `non_foreign_key_fields`, and `foreign_key_choices` to populate my erb file for *any model*.  Which is the coolest part.

First by cycling through all `non_foreign_key_fields` and just creating a text input html field for each one.

Then by cycling throughthe `foreign_key_fields` and creating a select html element for each one, with an option of each of the `foreign_key_choices` for that field and selecting the choice that matches this object's `foreign_key_id`.

```html
  <form action="/submit/<%=params["something"]%>">

  <!-- Show all non-foreign keys in an input field -->
    <% @m.non_foreign_key_fields.each do |field| %>
      <p><label for = "<%= field %> ">Select your <%= field %>:</label><input type= "text" name = <%= field %> field placeholder= "Type in the <%= field %>" value = "<%= @m.send(field) %>" ></input></p>
    <% end %> 

    <input type= "hidden" name = "id" value = "<%= @m.id %>">
  
    <!--Show all foreign keys in a select field -->
    <% @m.foreign_key_fields.each_with_index do |foreign_key, x| %>
      <p><label for=" <%= foreign_key %>  ">Select your <%= foreign_key %>:</label><select name = <%= foreign_key %>>
        <% @foreign_key_choices[x].each do |choice| %>
          <option value = <%= choice.id %>
            <% if @m.send(foreign_key).id == choice.id %>
              selected
            <% end %>> <%= choice.name %></option>
        <% end %>
      </select></p>
    <% end %>
  
    <input type = "submit">

  </form>
```


So I got this far and told Sumeet...
> I am really struggling with the LocationTime class, though.  It has a Composite Key and it means I can't apply any of the DatabaseConnector modules to it because that module assumes a single Primary Key called id.

And Sumeet looked at my code and said:
> This is not a wrong approach, but it's a different approach.  Having said that, I think there's probably a solution.  You have employed very creative solutions to your model already.

And I said:
> Wait, so how do other people work with composite keys?

And he said:
> They don't.  Yes, you could make this table have a Composite Key.  But it's simpler not to.

*Of course.*  

And I felt close to tears.  Because I have been straining and wringing and contorting myself over this problem for probably 50 hours of coding.

*When you find yourself banging your head against the same wall over and over...stop.*

Maybe this one lesson was more valuable than all the rest.

*_Sumeet gave us the idea to create an array called errors to store our errors in for validation.  Each model should have a valid? class that is called before a database SQL statement is called to make sure the object has good data.  Same idea here._