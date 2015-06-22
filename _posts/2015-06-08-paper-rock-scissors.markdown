---
layout: post
title:  "Rock-Paper-Scissors Refactored"
date:   2015-06-08 09:10:41
categories: ruby first-week game
---

So that Rock-Paper-Scissors game was great, right?  Well, it could be better. :)

I am learning about this class that we write things and we write them and we write them again.  That's how Sumeet @ Omaha Code School is teaching us.  The Hard Way.

#Assignment
Things to improve.

 - Puts/gets (user input or user messages) should only be in the GameDriver.
 
We want Classes to store the business logic.  We want the Driver to handle how the information is recovered for the Classes.

I have a gets/puts statement in my Player class to get a valid move.  Changing it will mean my Game will probably be responsible for helping my ComputerPlayer make a move.

 - Save the results of the game to a file (optional.)
 
 - Allow for a tournament with brackets, not just a best of game set.

 - Add tests to each class and each class's public methods.

Testing should not be done on the command line. Like the other code we write, it should be automated.  We use a gem called minitest to run our tests for us.  The important command is `assert_equal`, which takes two arguments, an expected and an actual value.

If you've seen tests in my previous projects, I learned about them today and went back and added tests later.

#Changes to the Player class

The Player Class no longer has `get_valid_move` or `set_valid_move` method and is not passed any information about moves from the Game.  Instead, it has a method called `is_computer?` which is defined as false for Player and true for ComputerPlayer.

```ruby
   # indicates whether Player is a computer
   #
   # returns boolean (false)
   def is_computer?
     false
   end
```


#Setting the moves
The Game class now sets the move.  Because the GameDriver class is actually the human interface, the player (object) and the move (string) are passed to it as parameters.  

The `set_computer_move?` will set the computer's move, if it is a computer player, or it returns false.  The `set_player_move`? sets the move if the move is valid or returns false if it is not.

I kept the check for the validity of a user's move in the Game class, so that it would be easier to re-use the GameDriver.  Many games might not be able to store all possible moves in an Array.

```ruby
   # sets the player's move if it is valid
   #
   # player - Player object
   # move - String
   #
   # returns boolean if it successfully set the move
   def set_player_move?(player, move)
     if possible_plays.include?(move)
        player.move = move
        true
      else
        false
      end
   end
  
   # if the player is a computer, sets the move
   #
   # player - Player object
   #
   # returns true if able to do so, sets false if not
   def set_computer_moves?(player)
     if player.is_computer?
       move = possible_plays.sample
       player.move = move
       true
     else
       false
     end
   end
```

#TournamentRound Class

The TournamentRound class takes an Array of objects in seeded order.  It stores that Array as :players, TournamentRound's single instance variable.
   
```ruby
   class TournamentRound
     attr_reader :players
  
     # initializes an array of players that are seeded in the order they arrive
     #
     # players - Array
     #
     def initialize(players)
       @players = players
     end
```

TournamentRound's `get_brackets` method returns an Array of Arrays, in which the highest seeded player is paired with the lowest seeded player, on down until there are no more pairs of players left.  If the number of players is odd, `get_brackets` will not return the median player in the `get_brackets` Array.
  
```ruby 
     # returns an Array of Arrays of the brackets, paired off in order of seeding
      #
      # returns an Array
      def get_brackets
        brackets = []
        (1..num_brackets).each do |x|
          brackets.push([players[x-1], players[-x]])
        end
        brackets
      end
```


#Changes to the GameDriver
The `get_player_moves` method was switched to the GameDriver class.  `set_users_move` asks a user over and over again for a move, passing it the `set_player_move?` method in Game until the Game returns a true, indicating the move was valid.

```ruby
  # set user's move
  #
  # player - Player object
  #
  # returns nothing
  def set_users_move(player)
    move = get_users_move(player.name).to_sym
    while !game.set_player_move?(player, move)
      move = get_users_move(player.name).to_sym
    end
  end
```


A `save_to_file` method was created that will save a string to the file.

```ruby
  # saves the string to file
  #
  # save_string - String
  #
  # returns nothing
  def save_to_file(save_string)
   # puts dir.pwd
    output = File.open( file_name,"a" )
    output << save_string
    output.close
  end
```

#Playing the Game
Now that I have tournaments, ComputerPlayers, and multi-player games, I had a whole lot of fun playing nonsense games.

I created a game of 70 ComputerPlayers and put them in a tournament against each other...until there was one.

Creating the ComputerPlayers.

```ruby
  puts "\nNow playing a game with 70 people."

  #creating the players
  all_70_players = []
  (1..70).each do |c|
    a = ComputerPlayer.new(c.to_s)
    all_70_players.push(a)
  end
```

Then I created an Array to store the players, and as they lose a game, they are deleted.  A new TournamentRound is played until there is only one in the Array that stores the players.

```ruby
  # now plays a tournament with 70 people
  # delete from all_players until there is only one
  all_players = all_70_players
  round = 1
  while all_players.length > 1
    puts "\nPlaying round #{round} in the tournament!"
    new_tournament = TournamentRound.new(all_players)
    brackets = new_tournament.get_brackets
    
    #play each bracket
    brackets.each_with_index do |players_for_game, index|
      puts "Bracket:\t#{index + 1}"
      winners = players_for_game
  
       #Now play the game until you get one winner
       # loop until you get a winner for the bracket
       # play_game may take a few games if there is a tie
       while winners.length > 1
         new_game = PaperRockScissorsGame.new()
         g_driver = GameDriver.new(game: new_game)
         g_driver.set_up_these_players_plus_any_more_required(players_for_game)
         winners = g_driver.play_game
       end
      
      #remove loser from all_players
      players_for_game.delete(winners[0])
      all_players.delete(players_for_game[0])
    
    end
    round += 1
  end
```

In case you're wondering, 43 won. :)  So that was a lot of fun.

#Links
[Here](https://gist.github.com/Gmfholley/be6bdd32fc5354e6adce) is my complete code with app.rb driver file.