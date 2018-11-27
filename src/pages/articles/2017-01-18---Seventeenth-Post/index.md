---
title: "Stuck & Unstuck: OO-Counting-Sentences"
date: "2017-01-18T14:40:13.121Z"
layout: post
draft: false
path: "/posts/seventeenth-post/"
category: "Blog, Itself"
tags:
  - "Ruby"
  - "Blog"
description: "This is a short post to time stamp when my Disqus comments weren't working on my Jekyll & Octopress generated blog."
---
I was stuck on the last counting sentences lab. The task of the last lab question is to count all the sentences in a given string. However, I didn't know that there was a .squeeze method or to use regex with the solution. 

Here's what I was working with before, while I was stuck: 
{% highlight ruby %}
def count_sentences
	count = 0
	array = self.split(" ")
	array.each do |item|
	      if item == "."
	        count += 1 
	        puts count
	      elsif item == "?" 
	        count +=1
	        puts count
	      elsif item == "!" 
	        count += 1
	         puts count
	      end
	end
end
{% endhighlight %}

It managed to count the sentences and return 0 when the string was empty, however it could not handle complex sentences such as "Well, there is a sentence!! This is another? And another? Woo...".<br>

The solution I used combines regex with the .squeeze method to eliminate duplicate characters while detecting punctuation. 

{% highlight ruby %}
def count_sentences
    string = self.squeeze(".")
    string = string.squeeze("!")
    string.split(/[$\.|?|!]/).count
 end
{% endhighlight %}

I discovered the .squeeze method through the Ask a Question feature of the community. Another member had used it for their solution. So, I used it to remove duplicates of periods and exclamation points in the sentence. <br><br>
I then used regex to determine where to split the string. I discovered that I could use the | to say "or" and then counted how many times the string was split. This count was the number of sentences in the complex example. Therefore, it solved the problem. 
