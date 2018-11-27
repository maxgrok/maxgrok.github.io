---
title: "If It Quacks Like a Duck: Duck Typing"
date: "2018-06-07T13:30:13.121Z"
layout: post
draft: false
path: "/posts/fortieth-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about duck typing and an example of duck typing."
---
<h2>Messages && OOP Design</h2>

One of the key lessons I learned by reading half of Sandi Metz's Object-Oriented Programming in Ruby book is that <quote>"messages are at the design center of your application"</quote> (p.82, Metz). 

The messages that get sent between classes define how the classes operate and what they ulimately do. A good way to think about how to design a class is to think about what kinds of messages you want it to receive or send.  

<h2>What is Duck Typing?</h2>

According to <a href="https://stackoverflow.com/questions/4205130/what-is-duck-typing#4205163">StackOverflow</a>, duck typing <quote>"is a term used in dynamic languages that do not have strong typing. The idea is that you don't need a type in order to invoke an existing method on an object - if a method is defined on it, you can invoke it."</quote>

In other words, the messages that you can send and receive -- the way an object behaves -- define an object more than what it is called. 

<h2>What are types?</h2>

Ruby provides a limited number of specific categories of variable, known as 'types', used to describe data (p.82), such as strings, numbers, etc. These types give way to expectations about how that data will behave, i.e. you can concatenate a string, add numbers together, and push objects into arrays. 

On a larger view, in Ruby, these types of expectations extend to objects' behavior based on it's public interface. This leads us to our next question. 

<h2>What is a public interface?</h2>

According to Wikipedia, a public interface <quote>"is the logical point at which independent software entities interact."</quote> (<a href="https://en.wikipedia.org/wiki/Public_interface">Public Interface</a>). In practical terms, for Ruby, its the methods which you can use to send and receive messages between objects that are accessible, i.e. not private methods in a class. 

<h2>Quack!</h2>
<h3>An example of a duck typing</h3>

```ruby 
'A string'.respond_to?(:to str)
=> true
Exception.new.respond_to?(:to_str)
=> false
4.respond_to?(:to_str)
=> false
```
This is the simplest example of duck typing, according to <a href="http://rubylearning.com/satishtalim/duck_typing.html">rubylearning.com</a>. 
If an object is a string, then treat it like a string. If the object is not a string, it will not be treated as a string. 

<h2>References</h2>

Metz, Sandi. Practical Object-Oriented Design in Ruby: an Agile Primer. Addison-Wesley, 2016.

“Public Interface.” Wikipedia, Wikimedia Foundation, 23 Sept. 2017, en.wikipedia.org/wiki/Public_interface.

Talim, Satish, and Erwin Aligam. “RubyLearning.com.” Ruby Exceptions, rubylearning.com/satishtalim/duck_typing.html.

“What Is Duck Typing?” Stack Overflow, stackoverflow.com/questions/4205130/what-is-duck-typing.

<h2>Further questions to consider</h2> 

What kind of implications does duck typing have for object-oriented design?<br> How does it affect relationships between objects?<br> What exactly would I use duck typing for in a Rails web app? <br>How would I incorporate this into my code? 





