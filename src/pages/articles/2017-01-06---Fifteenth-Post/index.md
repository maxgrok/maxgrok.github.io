---
title: "Stuck: Alphabetizing an Array within a Hash"
date: "2017-01-06T17:46:37.121Z"
layout: post
draft: false
path: "/posts/fifteenth-post/"
category: "Blog, Itself"
tags:
  - "Ruby"
  - "Blog"
description: "This is a short post to time stamp when my Disqus comments weren't working on my Jekyll & Octopress generated blog."
---
I'm currently stuck on a lab. In this lab, I need to iterate through a hash that is serving as a domain model for a school. In the hash, the key is the number of the grade that the students in the values are in. The students are stored in an array. The array the students are stored in needs to be sorted alphabetically; the grades need to be in ascending order. 

I don't understand how to get access to the array where students are stored or how to alphabetize them once I have accessed those values. 

I am currently passing all the other tests for the lab, except for this last one. 

I currently get this error: 

{% highlight ruby %}

School
  ::new
    has an empty roster when initialized
  #add_student
    is able to add a student
    is able to add multiple students to a class (grade)
    is able to add students to different grades
  #grade
    is able to retreive students from a grade
  #sort
    is able to sort the students (FAILED - 1)

Failures:

  1) School #sort is able to sort the students
     Failure/Error: expect(@school.sort).to eq({7 => ["Blake Johnson", "Jack Bauer"], 9 => ["Bart Simpson", "Homer Simpson"], 10 => ["Avi Flombaum", "Jeff Baird"]})
     
       expected: {7=>["Blake Johnson", "Jack Bauer"], 9=>["Bart Simpson", "Homer Simpson"], 10=>["Avi Flombaum", "Jeff Baird"]}
            got: {7=>["Blake Johnson", "Jack Bauer"], 9=>["Homer Simpson", "Bart Simpson"], 10=>["Avi Flombaum", "Jeff Baird"]}
     
       (compared using ==)
     
       Diff:
       @@ -1,4 +1,4 @@
        10 => ["Avi Flombaum", "Jeff Baird"],
        7 => ["Blake Johnson", "Jack Bauer"],
       -9 => ["Bart Simpson", "Homer Simpson"],
       +9 => ["Homer Simpson", "Bart Simpson"],
       
     # ./spec/student_spec.rb:58:in `block (3 levels) in <top (required)>'

Finished in 0.01888 seconds (files took 0.12698 seconds to load)
6 examples, 1 failure

Failed examples:

rspec ./spec/student_spec.rb:49 # School #sort is able to sort the students

{% endhighlight %}

The students are not alphabetized. 

I asked a few people at the Baltimore Node for help. They recommended that I take out all the students and sort them individually as I iterate through the hash, then place them back where they were. They also recommended that if that didn't work, take out all the students, then sort them back in the order they were in, then return them into the Hash. 

I'm confused about how to actually implement this though. 
I've tried this: 
{% highlight ruby %}
def sort
	array = []	
	@roster.each do |pairs|
		pairs.each do |student|
			array.push(student)
		end
	end
	return array
end
{% endhighlight %}

However, this does not work. It does not store the students in an array. It outputs the following results from the spec tests: 
{% highlight ruby %}
expected: {7=>["Blake Johnson", "Jack Bauer"], 9=>["Bart Simpson", "Homer Simpson"], 10=>["Avi Flombaum", "Jeff Baird"]}
got: [9, ["Homer Simpson", "Bart Simpson"], 10, ["Avi Flombaum", "Jeff Baird"], 7, ["Blake Johnson", "Jack Bauer"]]
     
       (compared using ==)
     # ./spec/student_spec.rb:58:in `block (3 levels) in <top (required)>'

Finished in 0.01681 seconds (files took 0.12729 seconds to load)
6 examples, 1 failure

Failed examples:

rspec ./spec/student_spec.rb:49 # School #sort is able to sort the students
{% endhighlight %}

I changed the code to convert the result of the iterations into a hash and sort them by adding ```end.sort.to_h```. I looked up how to alphabetize elements in an array on <a href="https://stackoverflow.com/questions/17799871/how-do-i-alphabetize-an-array-ignoring-case">Stackexchange</a>  ("How do I alphabetize an array ignoring case?").<br> I found this:
{% highlight ruby %}
wordlist.sort_by(&:downcase)
{% endhighlight %}

Now, I refactored the code to look like this: 
{% highlight ruby %}
def sort
		array = []	
		@roster.each do |pairs|
			pairs.sort_by(&:downcase)
			@roster[@grade] = pairs
		end.sort.to_h
	end
{% endhighlight %}

However, this doesn't work either. I get a different error. 

{% highlight ruby %}
School
  ::new
    has an empty roster when initialized
  #add_student
    is able to add a student
    is able to add multiple students to a class (grade)
    is able to add students to different grades
  #grade
    is able to retreive students from a grade
  #sort
    is able to sort the students (FAILED - 1)

Failures:

  1) School #sort is able to sort the students
     Failure/Error: pairs.sort_by(&:downcase)
     
     NoMethodError:
       undefined method `downcase' for 9:Fixnum
     # ./lib/school.rb:23:in `each'
     # ./lib/school.rb:23:in `sort_by'
     # ./lib/school.rb:23:in `block in sort'
     # ./lib/school.rb:22:in `each'
     # ./lib/school.rb:22:in `sort'
     # ./spec/student_spec.rb:58:in `block (3 levels) in <top (required)>'

Finished in 0.00349 seconds (files took 0.13756 seconds to load)
6 examples, 1 failure

Failed examples:

rspec ./spec/student_spec.rb:49 # School #sort is able to sort the students
{% endhighlight %}

So, I am somehow not accessing only the students array where the students are stored. I am converting it into an array where the keys are also stored. I don't know how to access the students array only for each iteration. 

I'm still working on this. 

