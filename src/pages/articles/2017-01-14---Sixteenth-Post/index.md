---
title: "Unstuck: Solving the Alphabetizing Problem"
date: "2017-01-14T22:28:13.121Z"
layout: post
draft: false
path: "/posts/sixteenth-post/"
category: "Blog, Itself"
tags:
  - "Ruby"
  - "Blog"
description: "This is a short post to time stamp when my Disqus comments weren't working on my Jekyll & Octopress generated blog."
---
Two days ago, I discovered the solution to the problem on which I was stuck. I will walk through the steps of why it is the solution, after showing you the whole code. 

{% highlight ruby %}
class School

	attr_accessor :roster, :name

	def initialize(name)
		@roster = {} #roster initially an empty hash
		@name = name
	end

	def add_student(student, grade)#takes in variable name and grade
		@roster[grade] = [] if @roster[grade] == nil 
		@roster[grade] << student # adds student and grade to hash @roster
	end

	def grade(grade)
		return @roster[grade] 
	end

	def sort
	 @roster= @roster.sort.to_h
		@roster.sort_by do |item, names|
			names = names.sort_by! do |name|
				 name.downcase	
			end
		end
		return @roster
	end
end
{% endhighlight %}

I was specifically stuck on the def sort method. So, I will go over exactly what I was doing in the def sort method. 

First, I made the instance variable @roster equal to it's sorted hash, which aligned all the keys (symbolizing the grades) in ascending order. 

As a result, the hash looked like this: 
{% highlight ruby %}
{7=>["Blake Johnson", "Jack Bauer"], 9=>["Homer Simpson", "Bart Simpson"], 10=>["Avi Flombaum", "Jeff Baird"]}
{% endhighlight %}

Second, I iterated through this hash using the sort_by! method to make sure it was altering the original array stored as a value within the @roster hash. 

Third, I set the names or values of the @roster hash to equal those arrays sorted by their individual names (such as "blake johnson") in downcase or without upper cases. 

Fourth, I ended this sorting within the @roster iteration, and ended the @roster sorting. 

Fifth, I returned the @roster resulted by the iterations and sorting. 

The result of this is the arrays stored as values within the @roster hash are alphabetized and returned to the @roster hash in their original form. 

Here is the result of calling the sort method: 
{% highlight ruby %}
{7 => ["Blake Johnson", "Jack Bauer"], 9 => ["Bart Simpson", "Homer Simpson"], 10 => ["Avi Flombaum", "Jeff Baird"]}
{% endhighlight %}

There you have it! I solved the problem. 

All the Best,<br>
Max 