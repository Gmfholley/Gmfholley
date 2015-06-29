---
layout: post
title:  "What Every Junior Developer Should Know"
date:   2015-06-12 09:10:41
categories: ruby second-week feeling-very-very-junior
---

One of the [former Omaha Code School students](https://railsmama.wordpress.com/2015/06/13/what-every-junior-rails-developer-should-know/) posted this on on our messaging service Slack today.

<img width = 50% height = 50% src = "https://railsmama.files.wordpress.com/2015/06/rails_skills_diagram1.jpeg">

Rails Mama's post is full of encouragement and hope for the future.  But I'm in week two.  It feels like a long road.  I understand just about one quintile of these words even.

So my response...

```ruby

require 'chronic'  # handles date/time

class BranchParser
  
  attr_reader :understanding
  
  def initialize
    @understanding = []
  end
  
  def parse_branches (branches)
    branches.each do |branch|
      if has_branches?(branch)
        parse_branches (branch)
      else
        understanding << branch.parse
      end
    end
  end
  
  def has_branches?(branch)
    #some test for branches
  end

end

me = BranchParser.new

begin
  me.parse_branches("Ruby On Rails Competencies")
rescue StudentOverloadException
  sleep(Chronic.parse("three months from now"))
  retry
end

  
```

Geek humor. :)