---
title: "Talking to My Duck: Real-World Debugging"
date: "2018-06-08T09:03:13.121Z"
layout: post
draft: false
path: "/posts/forty-second-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Debugging"
description: "This is a post about real world techniques I use to debug my code."
---

<h2>Backstory</h2>

When I was beginning to learn how to code, I was often frustrated by error messages and non-working code or rather code that behaved differently than I wanted it to behave. Flatiron has helped me embrace debugging as an art and shared a few techniques with me that enabled me to move forward effectively, tightening my 'feedback loop' (the process of receiving information about how your code is working or rather not working quickly).

<h2>Equipment Required</h2>

Working Computer with Internet Capability
Internet
Chrome on your computer with DevTools
A Ruby dev environment
A Rubber Ducky (just kidding)

<h2>Short List of Debugging Processes</h2>

```markdown 
1) Talk to Your Rubber Ducky...Or a Human Friend.
2) A Technique Called "Rinse, Wash, Repeat" 
(<--- I made this up. More on that later.)
3) Pair It Out 
4) Read about It on the Interwebs
5) Write down specific questions for a mentor. 

Extra Credit:
If your code has relationships in it, draw a UML or diagram to clarify. 
```

<h2>Details</h2> 
<h2>1) I talk to my duck.</h2>

I have a little cute duck that Flatiron School gave me named 'Oscar' (Yes, I named hir). Oscar is my regular companion in debugging. When I'm too shy to talk to anyone else about my code, I talk to Oscar. Occassionally, Oscar sqweaks, but is always helpful.  

If you don't have a duck, talk to an imaginary friend, alone. Talk to anyone about the problem that you are having, but be sure to articulate exactly and precisely what is happening and how it is different from how you expect it to behave. 
<h2>How to Use Your Words Precisely With Your Duck (or Human) Friend</h2>

This next bit was inspired by <a href="http://www.thegreatcodeadventure.com/junior-dev-survival-guide-communicate-clearly/">this blog post</a> on 'A Guide to Explaining What's Wrong'. In it, Sophie DeBenedetto describes this four step process to articulate exactly what is going wrong. I'm going to elaborate on it, but follow the general structure.  

First, describe exactly what is occuring, not what you want to be occuring. It needs to be a specific, actionable description. Second, describe the context in which the bug is happening. Third, explain how the actual behavior is different from the expected behavior. Fourth, explain how the current behavior differs from teh desired behavior. (<a href="http://www.thegreatcodeadventure.com/junior-dev-survival-guide-communicate-clearly/">Junior Dev Survival Guide: Communicate Clearly by Sophie DeBenedetto</a>)

<h3>What do I mean by specific?</h3> 

I want to know exactly what is happening, what is not happening, and the difference between the two. 

To help get you started, you can list any error messages you may be getting. Look to them for clues. 

Ex. Ruby shell error:

```ruby 
NameError:
uninitialized constant Artist
# ./spec/features/artist_spec.rb:5:in `block (2 levels) in <top (required)>'
```

In this above example, I know that `Artist` is not defined as a Ruby class. This means that it cannot instantiate an Artist that does not exist. It is currently giving me this error, but what I would like it to do is make a new Artist instance. To fix this, I would define an Artist class in the file specifically tested in the `./spec/features/artist_spec.rb` file. This error gives me almost all the information that I need to solve this problem. 

Check the frontend console and backend shell. 
Ex. Javascript console error: 

```javascript
VM115:1 Uncaught ReferenceError: proper is not defined at <anonymous>:1:1
(anonymous) @ VM115:1
```

With the above error, I have a similar problem. `proper` is not defined in the `<anonymous>` or global scope. To get this error, I simply pulled up my console in Chrome and typed `proper` and hit `Enter`. I did not define it at all. I would say that the intended variable `proper` was able to be accessed in the global scope. My intention is to access it in the global scope. In order to do this, I would need to fix the `Uncaught ReferenceError` by entering `let proper = "proper"` into the console, then enter `proper`. It will return `"proper"`, rather than an `Uncaught ReferenceError`. 

If you get an error message that you don't know how to read, then feel free to <a href="http://www.duckduckgo.com/">DuckDuckGo</a> it. You are most likely not alone. <a href="http://www.stackoverflow.com">StackOverflow</a> is your friend as well. 

<h2>Real World Example</h2>

I have been working a lot on DOM manipulation recently, so let's use an example from the Yelp! clone that I built. I was having trouble retrieving the Reviews from the Rails JSON API that I built and displaying them on the web app via DOM manipulation. 

To debug this, I used `console.log()`  to see the JSON objects I was receiving from my `GET` fetch request from the `localhost:3000/api/v1/reviews` and `debugger;` after constructing the json into `new Review`s. 

If I was in Ruby, I would use `require 'pry'` in my Ruby file and run `binding.pry` to stop the code from executing further in IRB in my CLI at a desired line. In this case, since I was testing associations, I used `rails c` in my CLI to enter in a test of my relationships. Did property have many reviews? To check, I entered into my Rails console, then typed `Property.all` to see all my properties. 

```ruby 
2.3.3 :001 > Property.all
  Property Load (0.7ms)  SELECT  "properties".* FROM "properties" LIMIT $1  [["LIMIT", 11]]
 => #<ActiveRecord::Relation [#<Property id: 34, name: "asdf", description: "asdf", address: "asdf", phone_number: "asdf", website: "afasdf", created_at: "2018-06-07 12:54:00", updated_at: "2018-06-07 12:54:00">, #<Property id: 35, name: "Moses", description: "This is an description", address: "Address", phone_number: "123.234.5234", website: "www.com", created_at: "2018-06-07 18:02:54", updated_at: "2018-06-07 18:02:54">]> 
```

Then entered in `Property.last.reviews` to see if there were any reviews attached to the last property. 

```ruby
 Property Load (1.4ms)  SELECT  "properties".* FROM "properties" ORDER BY "properties"."id" DESC LIMIT $1  [["LIMIT", 1]]
 => #<Property id: 35, name: "Moses", description: "This is an description", address: "ADdress", phone_number: "123.234.5234", website: "www.com", created_at: "2018-06-07 18:02:54", updated_at: "2018-06-07 18:02:54"> 
```

From this information, I could tell that the backend relationships were functioning well. 

<h2>2) Rinse, Wash, Repeat</h2> 

Write down on a piece of paper your expected behavior, results of that action, and a hypothesis of how to fix it, then try the hypothesis while `console.log`ging the results of your new coding. 

Example: I hypothesize that this hypothetical DOM element will appear on the page based on the code that I have written. I test this out by opening `index.html`. If I open `index.html` and it appears, then it is a success and the code runs as hypothesized. If it does not, then I must debug my code. Let's assume it does not. What next? Let's examine `index.html` to see if the element exists. If the element does not exist, then this is why it is not appearing on the page. I need to create an element in `index.html` that corresponds to the id that I am grabbing from the js file by using the `document.getElementById('id')` method where id is equal to the CSS id of the element. So, if I create an element with the following code in `index.js`:

```javascript
let p = document.createElement('p');
p.innerText = "Hello, World!"
p.id = 'id'
```

I can then reload the `index.html` page to see if the element in the DOM. Oh no! Spoiler alert: it won't be. Why? Because we haven't appended it to the DOM. Let's do that, but first, our hypothesis is that if we append it to the body of the `index.html` file that it will appear in the DOM. The action we are taking to fix this lack of appearance is to appended the element to the DOM in the `index.js` file. Let's add the following code last in our `index.js` file: 

```javascript
document.body.appendChild(p);
```

Now, the element appears in the DOM. Hello, World! If this didn't work, we could try it again by coming up with more hypotheses and running more types of tests with new snippets of code. Be sure to `console.log` elements or use `debugger;` to stop code if you add a lot of code just to make sure each step functions exactly as you want it to function. 

<h2>3) Pair It Out </h2>

Find a driver or a navigator. Get to the solution together!
    
A driver in pairing types out the code, while the navigator tells them overall strategy for approaching the problem and coding a solution by describing it to the driver. 

<h3>Exact Pair Programming Role Activities</h3>  

```markdown
Driver:
  -Write the code according to the navigator's specification
  -Listen intently to the navigators instructions
  -Ask questions wherever there is a lack of clarity
  -Offer alternative solutions if you disagree with the navigator
  -Where there is disagreement, defer to the navigator. If their idea fails, get to failure quickly and move on
  -Make sure code is clean
  -Own the computer / keyboard
  -Ignore larger issues and focus on the task at hand
  -Trust the navigator - ultimately the navigator has the final say in what is written
  -You are writing the code 

Navigator:
  -Dictates the code that is to be written - the 'what'
  -Clearly communicates what code to write
  -Explains 'why' they have chosen the particular solution to this problem
  -Check for syntax / type errors as the Driver drives
  -Be the safety net for the driver
  -Make sure that the driver sticks to the small task at hand
  -Outline and note down high level tasks / issues
  -Ongoing code review
  -Pay attention
  -Wait until the task is complete to bring up design / refactoring issues

Both:
  -Actively take part in programming
  -Aim for optimal flow - avoid trying to be 'right'
  -Embrace your role
  -Intervene if your pair is quiet
  -Know when to give up / steal keyboard
  -Communicate, communicate, COMMUNICATE!
  -Sync up frequently to make sure you are on the same page
  -Don't hog the keyboard
  -High-five every time a test passes
  -Follow best practices for TDD
  -Swap roles frequently
```

Source: <em>Jordan Poulton</em>, <a href="https://gist.github.com/jordanpoulton/607a8854673d9f22c696">Pair_Programming_Roles</a><br>

<h2>4) Read About It on the Interwebs</h2>

These sites are your friend: 
<a href="http://www.duckduckgo.com/">DuckDuckGo</a>. <a href="http://www.stackoverflow.com">StackOverflow</a>. <a href="http://www.twitter.com/">Twitter</a>.  

If you are a member of developer groups on <a href="http://www.slack.com">Slack</a>, then Slack is your friend. If you are a member of <a href="http://www.quora.com/">Quora</a>, a Q&A site, then Quora is your friend. 

Even <a href="http://www.reddit.com/">Reddit</a> is sometimes your friend in places like `/r/ruby`. 

Individual Developer Blogs like <a href="https://blog.codinghorror.com/">Coding Horror</a> are your friends and sometimes walk you through debugging your specific problem or a similar problem. 

For video resources: <a href="http://www.youtube.com/">YouTube</a> is great. 

If you are new to Internet research, here is a useful post on how to do <a href="https://www.colorado.edu/history/undergraduates/paper-guidelines/using-internet-research">research</a>. Here is a good <a href="https://www.thoughtco.com/internet-research-tips-1857333">article</a> to determine if your sources are reliable. 

<h2>5) Write down <em>specific</em> questions for a mentor.</h2>

Don't forget to include your code and provide context to your question by using <em>precise language</em>. Mention what you have tried to do to solve the problem first. Try everything above first, then schedule a time to talk and don't forget to write or say a quick 'Thank You'.<br>

<h2>TL:DR;</h2> 

Debugging Tools Mentioned: 

Javascript: 
`Debugger;`
`console.log` in the console

Ruby: 
`pry`/`binding.pry` -- to install, include `gem 'pry'` in your Gemfile 
`rails c` Rails console in CLI


