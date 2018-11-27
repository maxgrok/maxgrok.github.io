---
title: "OO Tic Tac Toe"
date: "2017-01-02T12:46:37.121Z"
layout: post
draft: false
path: "/posts/nineth-post/"
category: "Flatiron School"
tags:
  - "Ruby"
  - "Lab"
description: "This is a post about a Ruby lab for the Flatiron School."
---

In this assignment, I built a two player game of tic tac toe using object orientation. I use a previously completed ruby tic tac toe game, then convert it to object orientation using a class called TicTacToe. 

Here's the code for the Ruby TicTacToe: 
{% highlight ruby %}
require 'pry'

board = [" ", " ", " "," ", " ", " "," ", " ", " "]

WIN_COMBINATIONS = [
	[0,1,2],
	[3,4,5],
	[6,7,8],
	[0,4,8],
	[2,4,6],
	[0,3,6],
	[1,4,7],
	[2,5,8]
]

def position_taken?(board, index)
  !(board[index].nil? || board[index] == " ")
end

def won?(board)
  WIN_COMBINATIONS.detect do |combo|
    position_taken?(board, combo[0]) && board[combo[0]] == board[combo[1]] && board[combo[1]] == board[combo[2]]
  end
end

def full?(board)
  board.all? do |position|
    position == "X" || position == "O"
  end
end

def draw?(board)
    return !won?(board) && full?(board) ? true: false
end

def over?(board)
	if won?(board) 
		return true
	elsif full?(board) && won?(board)
		return true
	elsif full?(board)
  		return true
	elsif draw?(board)
 	    return true
	else
  		return false
    end
end

def winner(board)
  winning_combo = won?(board)
  if winning_combo
    return board[winning_combo[0]]
  end
end


def display_board(board)
  puts " #{board[0]} | #{board[1]} | #{board[2]} "
  puts "-----------"
  puts " #{board[3]} | #{board[4]} | #{board[5]} "
  puts "-----------"
  puts " #{board[6]} | #{board[7]} | #{board[8]} "
end

display_board(board)

def move(board, input, value)
  board[input] = value
end

def input_to_index(input)
	return input.to_i - 1
end


def valid_move?(board, index)
	#if move is valid
	if position_taken?(board,index) == false && index.between?(0,8) == true
		return true
	#if move is invalid
	elsif position_taken?(board, index) == true
		return false
	elsif index.between?(0, 8) == false 
		return false
	end
end

def turn(board) 
	puts "Please enter 1-9:"
	input = gets.chomp
	index = input_to_index(input)
	if valid_move?(board, index) == true && turn_count(board).even? == true
		move(board, index, value = "X")
		puts display_board(board)
	elsif valid_move?(board, index) == true && turn_count(board).odd? == true
		move(board, index, value = "O")
		puts display_board(board)
	elsif valid_move?(board, index) == false
		puts "Please enter 1-9:"
		input = gets.chomp
	end
end
def isEven?(board)
	return turn_count(board) % 2 == 0 ? true : false
end

def isOdd?(board)
	return turn_count(board) % 2 == 1 ? true : false
end

def turn_count(board)
	turns = 0
	board.each do |turn|
		if turn == "X"
			turns += 1
		elsif turn == "O"
			turns += 1
		end
	end
	return turns
end

def current_player(board)
	return turn_count(board).even? == true ? "X" : "O"
end

def play(board)
    while over?(board) == false
    	turn(board)
    end
    if draw?(board)
    	puts "Cats Game!"
    elsif winner(board) == "X" 
    	puts "Congratulations X!"
    elsif winner(board) == "O"
    	puts "Congratulations O!"
    end
end

{% endhighlight %}

Here's the code for the Object-oriented TicTacToe: 
{% highlight ruby %}
require 'pry'

class TicTacToe
	def initialize
		@board = [" "," "," "," "," "," "," "," "," "]
	end

	WIN_COMBINATIONS = [
	[0,1,2],
	[3,4,5],
	[6,7,8],
	[0,4,8],
	[2,4,6],
	[0,3,6],
	[1,4,7],
	[2,5,8]
	]

	def display_board
	  puts " #{@board[0]} | #{@board[1]} | #{@board[2]} "
	  puts "-----------"
	  puts " #{@board[3]} | #{@board[4]} | #{@board[5]} "
	  puts "-----------"
	  puts " #{@board[6]} | #{@board[7]} | #{@board[8]} "
	end

	def input_to_index(user_input)
		user_input.to_i - 1
	end
	
	def move(index, value)
	  @board[index] = value
	end

	# Helper Method
	def position_taken?(index)
	   !(@board[index] == " ")
	end

	#valid_move?
	def valid_move?(index)
		#if move is valid
		if position_taken?(index) == false && index.between?(0,8) == true
			return true
		#if move is invalid
		elsif position_taken?(index) == true
			return false
		elsif index.between?(0, 8) == false 
			return false
		end
	end
 
	#turn_count
	def turn_count
		turns = 0
		@board.each do |turn|
			if turn == "X"
				turns += 1
			elsif turn == "O"
				turns += 1
			end
		end
		return turns
	end
	
	#current_player
	def current_player
		return turn_count.even? == true ? "X" : "O"
	end

	#turn
	def turn
		puts "Please enter 1-9:"
		user_input = gets.chomp
		index = input_to_index(user_input)
		if valid_move?(index) == true && current_player == "X"
				move(index, value = "X")
				puts display_board
		elsif valid_move?(index) == true && current_player == "O"
				move(index, value = "O")
				puts display_board
		elsif valid_move?(index) == false
			puts "Please enter 1-9:"
			input = gets.chomp
		else 
			puts "Please enter 1-9:"
			input = gets.chomp
		end
	end

	#won?
	def won?
	  WIN_COMBINATIONS.detect do |combo|
	    position_taken?(combo[0]) && @board[combo[0]] == @board[combo[1]] && @board[combo[1]] == @board[combo[2]]
	  end
	end

	#full
	def full?
		@board.all? do |index|
			 index == "X" || index == "O"
			end
	end

	#draw
	def draw?
			if won? 
				return false
			elsif full? == false 
				return false 
			else 
				return true
			end
	end

	#over
	def over?
			if won? || draw? == true
				return true
			else
				return false
			end
	end

	#winner
	def winner
		winning_combo = won?
		 if winning_combo
		    return @board[winning_combo[0]]
		 end
	end
	
	#play
	def play
	    while over? == false
	    	turn
	    end

	    if draw?
	    	puts "Cat's Game!"
	    elsif winner == "X" 
	    	puts "Congratulations X!"
	    elsif winner == "O"
	    	puts "Congratulations O!"
	    end
	end

end
{% endhighlight %}

All the Best,

Max