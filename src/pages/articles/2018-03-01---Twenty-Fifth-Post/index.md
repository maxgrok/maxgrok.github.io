---
title: "JS Deli Counter Lab"
date: "2018-03-02T14:10:13.121Z"
layout: post
draft: false
path: "/posts/twenty-fifth-post/"
category: "Flatiron School"
tags:
  - "JS"
  - "Final Project"
  - "Javascript"
description: "This is a post about the JS Deli Counter Lab in the Flatiron School Community-Based Bootcamp."
---

I'll break this down into different categories of technical components. First, we'll discuss the methods used and what exactly they do in the Javascript Deli Counter Lab, then we'll discuss the functions that are defined as a whole and how those methods fit in. 

# Methods You Need

The .push method in Javascript adds an item to the end of the array. 

The .shift method in Javascript removes the first item of an array and returns that item. 

The .length method returns the length of the array on which the method is operated. 

# Functions Defined

## takeANumber

### Task

Build a function that a new customer will use when entering the deli. The function, takeANumber, should accept the current line of people, katzDeliLine, along with the new person's name as parameters. The function should return their position in line. And don't go being too programmer-y and give them their index. These are normal people. If they are 7th in line, tell them that. Don't get their hopes up by telling them they are number 6 in line.

### Breakdown

Start a function. function takeANumber(){ * your code goes here * }
It accepts two arguments as parameters, which means that they go in the definition of the function, i.e. inside the parentheses. The function should stop and simply return the position in which the person is in line. No one wants to have an inaccurate number in line, so make sure to account for the index factor of arrays (that arrays start at 0). 

We do this by the following: 

function takeANumber(katzDeliLine, name){
	katzDeliLine.push(name); // add the name to the line of the deli array!

return "Welcome, " + name + ". You are number " + katzDeliLine.length + " in line."; // this returns the sentence "Welcome, *insert customer's name*. You are number *insert number they are in line* in line."
}

Now run the tests. They should all be passing for this function. The function simply returns the position in line that the customer is waiting in. 

## nowServing

### Task 
Build a function nowServing. This function should return the first person in line and then remove that individual from the line. If there is nobody in line, it should return "There is nobody waiting to be served!"

### Breakdown 

Define another new function in your js file beneath the first function, takeANumber. This function does not accept two parameters, only one: katzDeliLine. We do this because we need to know who is in line in order to return the first person in line and then remove that individual from the line. 

So, let's start: 

function nowServing(katzDeliLine){
	if (katzDeliLine.length === 0){ // .length method is used to determine if there are people in line and if - in this case - there are not, then return the below string!
		 return "There is nobody waiting to be served!";
	}
	else{
		var shift = katzDeliLine.shift(0); // .shift method is used to remove the first person from line and return that person at the same time
		return shift;
	}
}

Now, your tests should be all passing. Let's go on to the next one!

## currentLine 

### Task

Build a function currentLine that returns the current line. For example, if katzDeliLine is currently ["Ada", "Grace"], currentLine(katzDeliLine) would return "The line is currently: 1. Ada, 2. Grace". If there is nobody in line, it should return "The line is currently empty."

### Breakdown

Let's build another function! This one returns everyone in current line. 

function currentLine(katzDeliLine){
	if (katzDeliLine.length === 0){
		return "The line is currently empty."; // if empty returns this string
	}
	else{
		return "The line is currently: 1. " + katzDeliLine[0] +", 2. " + katzDeliLine[1]; // returns everyone in line (Both Ada and Grace)
	}
}

The function should be passing all the tests! Yay! 

# User Cases

Let's test all the functions by defining the katzDeliLine as a global variable and calling the functions.

var katzDeliLine = ["Ada"]; //katzDeliLine is equal to an array that holds the name of the customers in line ("Ada") in the form of strings.

## Test 1

takeANumber(katzDeliLine, "Grace"); // calling the function

//expected output will be the following string "Welcome, Grace. You are number 2 in line."

## Test 2

nowServing(katzDeliLine);

//expected output will be the following: "Ada"

## Test 3

currentLine(katzDeliLine)

//expected output will be "The line is currently 1. Ada, 2. Grace"

## Tests Passing? 

Hooray! You're all done with the Deli Counter JS Lab in Flatiron School. 