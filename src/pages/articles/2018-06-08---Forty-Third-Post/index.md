---
title: "Maps: They Don't Love You Like I Love You"
date: "2018-06-08T06:22:13.121Z"
layout: post
draft: false
path: "/posts/forty-third-post/"
category: "Ventures"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about attitude, GIS maps, and starvation."
---

<quote>"We can do this today...before we finish this cup of coffee!" (<a href="https://twitter.com/twobitidiot/status/1004866201212813312">Garry Tan Tweet</a>)</quote>

When I was outside, it was hard. It wasn't hard in expected ways. I had prepared myself for being cold and alone in a new city. [Hot Tip: Mylar emergency blankets -- about $1/each at a outdoors store, 2oz]

It was hard because I didn't have actionable information. What do I mean?

One day, I met with a case worker and I asked the case worker where to get food and was met with a paper packet. It would be filled with resources, except here's the catch. (It didn't matter which case worker. They had the same packets most of the time.)

Here is how the organization's information is presented in their 
<h2>Initial Listing</h2>

```markdown
Food Pantry of America Inc.
26-02 14th Street
New York, NY 11102
123-123-12345 (Phone Number)
```

This might <strong>seem</strong> like good information to the untrained eye. However, here is some key bits of information missing that can cost your life.

<h3>1) Date Updated</h3>

How old is this information? Is it an organization that regularly partners with the organization from which you got the information packet? Has this case worker ever gone to or visited the location? How long ago? Is the phone number up to date? 

<h3>2) Are they still open?</h3>

There is - unlike restaurants listed on Yelp! - no way of telling from this information, which means I'd need to call them. This leads me to my third point of contention.

<h3>3) Do they answer the phone? </h3>

This is mostly due to lack of resources. In this case, many resources lack the time to be able to answer the phone. Some will have automated services that detail their up to date information, but most will simply have a voicemail. 

<h3>4) Do they listen to and respond to their voicemail?</h3>

Let's say you got this paper packet at a case workers office (sometimes after waiting 2 weeks for an appointment). You start to work down a list of food resources. You're hungry. Now, let's say you go to the location right then and it's 4 pm on a Wednesday. It takes you 5 min assuming it's a nearby location that was recommended (and assuming you qualify for services). They're closed. So, it's not too bad because you've only wasted 5 minutes, but imagine if this was an hour, both ways to get there. Imagine that the doors are locked and it's a church. Imagine they're closed for renovations. Not only did you just waste two hours (you need to get back after all), but you have lost faith in that list that case worker just gave you after trying three more resources, each further away from the next and not organized by location. 

Let's say you get smarter or more likely, start asking around to get access to a phone. You learn that you need the paper packet at the ready and to start calling these locations. Let's say you get skeptical and call them all to see if they even exist. You find 10 of the 25 locations are closed. 10 of the locations have voicemails and no automated system to tell you when their services are. 5 of them have automated systems to direct your call, but you end up in voicemail anyway. Let's say you give up. You've already been to 5 locations. None of them have told you the next bits of information, including your case worker. 

<h3>5) The Basics of Food Information</h3>

Questions: What time is the meal? What kind of food is it? Is it food I need a fridge or freezer to maintain? (Spoiler alert: I don't have a freezer or a fridge I have access to) Is it hot food? Do I need to go to a church service in order to receive food? How long is the service? What time is the service? Do I qualify for the food? Do I need to do an intake before receiving the food? Is there any paperwork for the food? Do I need ID? (Spoiler alert: If you do not have ID, then some places may not let you eat there. However, getting an ID is a whole other process and required for basic participation in US society.)

These are all reasonable questions that are not answered by this sparse bit of information that your case worker has just given you and, of course, you didn't think to ask these questions because you assumed that you were given all the proper information for your needs, plus you're hungry. 

Let's say that you have a phone. Let's say you leave this on their voicemail. They respond...6 days later. So, now you've waited 2 weeks for an appointment with a case worker + 6 days to find out when services are even administered. <h2>That's about 2.8 weeks without food.</h2>

Now, all of these are processes are based on experience and based on the experiences of friends circa 2011. Things may have changed.  

For those more privileged people who expect their services to be delivered by TaskRabbits within an hour, others are still waiting for that callback to announce when their food will potentially be served, if they qualify, if they have ID, in 6 days because they are experiencing a poverty of actionable, accessible information. 

<h2>What was my solution to this problem? </h2>

This was a huge issue for me and my friends in NYC in 2011 onward. So, I dedicated myself to solving it because I could do it right then with a little help from <a href="http://www.batchgeo.com/">BatchGeo</a>. <strong>I could do it that day, right then.</strong>

<strong>My solution was to make an interactive GIS map using BatchGeo API and an .xls file filled with propertly organized information about key, strategic resources for not only food, but healthcare, places to sleep, and education too.</strong> 

<h2>Features</h2>

Here's an example of the features of a map that changed my life and my friend's lives in 2011: 

<h3>1) You cannot lose it. (It's on the Internet)</h3>

<h3>2) You can always access it without any appointment needed. (It's on the Internet)</h3>

<h3>3) Friends only: Hosted on a password protected Tumblr on an obscure address</h3>

<h3>4) Searchable by address, phone number, time of meal served, name of organization, day of services</h3>

<h3>5) Interactive Map - enables you to see what is close by what</h3>

<h3>6) Clickable address and phone number </h3>

a) If you clicked on the address, it would redirect you to Google Maps for directions<br><br>b) If you clicked on the phone number and you were on a mobile phone, it would call for you.

<h3>7) Search by type of service (healthcare, shelter/sleep, food, education)</h3>

<h3>8) Displays Your Location</h3>

(with your permission on mobile/desktop (useful for if you don't know the address of where you are, so you can see resources nearby you)

<h3>9) Qualifications and Requirements.</h3>

With each resource, there was a list of requirements and qualifications. If you needed to bring ID, I listed that you needed to bring ID. If you needed to be under 24 years old, then I listed that.

All the things that you needed to know right up front. 

So, when you clicked on a map marker, you could see a pop up of information in this format: 

<h3>Solution Listing</h3>

```markdown
Type of Meal: Hot Meal
Time of Meal: 9am - 10am
Days Served: Monday - Friday

Address:
26-02 14th Street
New York, NY 11102

Phone Number: 123-123-12345 (Phone Number)
Name of Organization: Food Pantry of America Inc.
Type of Resource: Food
```

This format puts the information that you need to access the resource as priority number one. It's listed first what time the meal is, how often it's served, and where it is located. It's organized in a way that serves to provide the most important information first. 

<strong>Qualifying Tid Bits:</strong> I discovered BatchGeo after trying to read the Leaflet.JS docs without any knowledge of javascript and cobble something together to get a map to display on a page without success. I believe I did a DuckDuckGo search for "GIS Mapping Software" and besides ArcGIS, found the user-friendly BatchGeo.   

<h2>Backstory</h2>

I made this map while I was living in the basement of a church with no money. 

<h2>How long did this map take to make?</h2>

I spent hours entering in resources manually from paper packets into BatchGeo's format in an Excel spreadsheet to make this map. 

No one gained anything except that it saved us all time and headaches when trying to get fed, get healthcare access, and get to sleep somewhere inside. We used it to get access to the basics and build a daily schedule. We used it to not starve. 

<h2>Acknowledgements</h2>

I owe my deepest gratitude to my Professors (Smith and Silon) at the University of Rochester who may never know their true impact or read this blog post. Without them and what they taught me about the Strength of Weak Ties (<a href="https://sociology.stanford.edu/sites/default/files/publications/the_strength_of_weak_ties_and_exch_w-gans.pdf">Granovetter</a>) and Creative Destruction (<a href="http://www.econlib.org/library/Enc/CreativeDestruction.html">Schumpeter</a>) and the Social Networking Mapping exercises we did in Social Networking Theory & Entrepreneurship, I would not have come up with this idea, believed I could do it, and quite likely would have starved. 

I also owe Professor Scott Klemmer for everything he taught me through <a href="http://www.coursera.com/">Coursera</a> about Human-Computer Interaction, including but not limited to rapid prototyping.<br>I also owe an old acquantaince for forming the best, most comprehensive packet of information at the time. Without it, I could not have made the map as accurate as it was at the time.

I made this map with the tremendous help of the folks at BatchGeo (circa 2011) who made an publicly accessible API that took an Excel spreadsheet as input and turned it into a beautiful, searchable map. I also need to extend gratitude to the basement of the church where I lived. Lastly, thank you to the administrators, case workers, and various other staff at these resources. It is truly a gift that you exist and what you are doing is great, but could be better.

<strong>Thank you to you all for reading this post! </strong>

<h2>Wrap Up</h2>

Without all these unique bits of knowledge and tools, I would not have made it to where I am today.  

