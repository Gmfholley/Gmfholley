---
layout: post
title:  "Rock-Paper-Scissors(-Lizard-Spock)"
date:   2015-06-05 09:10:41
categories: ruby first-week game
---

#Assignment
It is still the first week of Code School.  Homework is:

 - Create a Game of paper, rock scissors
 - Create a Player
 - Create a GameDriver to play the game
 
Fun! Stretches!

 - Make the Game paper, rock, scissors, lizard, spock
     - Giggle at the idea that paper "disproves" Spock
 - Make a ComputerPlayer who can play the game.  Game should not be able to tell the difference.
 - Create a Tournament of games
 - Play a Game of tic-tac-toe (using the same GameDriver!)
 
#Design

My thoughts as I initially designed this were:

 - Since Game may not always be Rock-Paper-Scissors, I need to make sure that my current Game class can be duck-typed for a game as different as tic-tac-toe.
 - Game should have the rules of the game - (`possible_moves`, `number_of_players`, `players`)
 - My ComputerPlayer class will inherit from my Player class, but it will overwrite the `get_move` method to sample from the Array of possible_moves, instead of asking the Player for a move.
 - I need to be able to play more than one game.

#Game

Game has two instance variables - `players` stores an Array of the player object.  `needed_players` is the number of players needed for a game.

```ruby
  # prints the rules at the beginning of the game
  # asks the user to initialize the players
  #
  # returns self
   def initialize()
     @players = []
     @needed_players = 2
     #set_needed_players(args[:needed_players])
   end
```
 
The rules of the game are stored as methods in Game.

```ruby
   # Hash of the plays - put in the user's play, and you will see what it beats
   def winning_play
     {paper: [:rock, :spock], rock: [:lizard, :scissors], scissors: [:paper, :lizard], lizard: [:spock, :paper], spock: [:rock, :scissors], scratch: [:scratch]}
   end
   
   # Array of the plays each player can use
   def possible_plays
     [:paper, :rock, :scissors, :spock, :lizard]
   end
   
   # String of the rules of the game
   def rules
     "Choose rock, paper, scissors, lizard, or spock."
   end
```
With the game class, you can `add_player_to_players` by passing in a Player object.  You can also check if there are `enough_human_players?` yet, so that your GameDriver can pass in ComputerPlayers if needed.


The Game class is also responsible for returning the results of a game or games.  You can get the score for every player (`get_score`), get the `highest_player_score` or `players_with_highest_score`.  

Finally, Game has a method calls `play_a_game`, which asks each player for a move, plays the game with those moves, and saves the player's score, returning the winner(s).

```ruby
   # plays a single game and gets the winners nad saves the score
   #
   # returns array of winning players
   def play_a_game
     get_each_players_move
     winners = get_games_winners
     save_winners(winners) unless winners.nil?
     winners
   end
```

Since I store the `winning_play` as a hash, checking to see who wins is just a simple matter of looking up the results of the hash vs. the other player's move, which is calculated in a utility method called `winners_between_two_players`.

```ruby
   # returns an array of the winner(s) of a two-player game (allowing for a tie)
   #
   # player, against_player are Player objects
   #
   # returns an Array
   def winners_between_two_players(player, against_player)
     #if player's winning move = against_player's move, player wins
     if winning_play[player.move].include?(against_player.move)
        return [player]
     # if against_player.move is the winning play, against_player is the winner
     elsif winning_play[against_player.move].include?(player.move)
        return [against_player]
     # otherwise, they tied (ie - both won)  
     else    
        return [player, against_player]
     end
   end
```

But I did add a layer of complexity to my game by allowing any group of players to play paper-rock-scissors at the same time.  The way that works is that you play each player against each other player.  Whoever has the highest score in that round of player vs. player wins. 

```ruby
   # returns Hash of plqyers and their scores against all other players
   # 
   # returns Hash
   def all_player_tally
     tally = Hash.new(0)
     players.each do |player|
        players.each do |against_player|
           winners_between_two_players(player, against_player).each do |winner|
             tally[winner] += 1
           end
         end
      end
      tally
   end 
```

#Player
The Player class stores the name, score, and current move.

```ruby
   def initialize(name)
       @name = name
       @score = 0
       @move = ""
   end
```

Player has an `increment_score` method to increase the score.  The score is otherwise not writeable.

The move is changed by asking the user to `set_valid_move`.  Since Player will be used in multiple games, the Array of valid moves is passed to it.

Player asks the user to return a valid move in a separate method called `get_valid_move` which will loop until the user returns a valid move.

```ruby
   # gets a valid move from the user
   #
   # valid_move - Array of all valid moves
   #
   # returns String of valid move
   def get_valid_move(valid_move)
     puts "Moves: #{valid_move.join("\t")}"
     try_move = get_user_input("#{name}, choose your move.").to_sym
     while !valid_move.include?(try_move)
       try_move = get_user_input("Not a valid move.  Try again.").to_sym
     end
     try_move
   end
```

##ComputerPlayer

ComputerPlayer inherits from Player in every respect, except the `get_valid_move` method samples from the `valid_move` parameter that was passed to it.

```ruby
class ComputerPlayer < Player
  
  # selects an item from the valid_move array at random
  #
  # returns String of valid move
  def get_valid_move(valid_move)
    my_move = valid_move.sample
    puts "My AI chooses #{my_move}"
    my_move
  end
  
end
```

#GameDriver
My GameDriver class has two parameters, a game and a `best_of` set of games for tournaments.

You can `play_game` or `play_best_of_game_set`.  A single game call `play_a_game` from game and will then `publish_winners` and `display_score`.

The GameDriver is also responsible for making sure the rules of the game are followed.  It will `get_user_players` and if the user does not create enough players for the game, it will `add_computer_players_if_not_enough_humans`.

#Links
[Here](https://gist.github.com/Gmfholley/ab195a42aeaa156dc77b) is my complete code with app.rb driver file.
