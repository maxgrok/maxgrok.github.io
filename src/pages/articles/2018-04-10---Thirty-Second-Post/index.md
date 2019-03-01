---
title: "The Final Countdown: Impromptu Assignment"
date: "2018-04-10T11:30:13.121Z"
layout: post
draft: false
path: "/posts/thirty-second-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about how to build a simple countdown Rails app."
---

## I Volunteer!

I volunteered to create a Rails app that does countdown to the next lecture. 

Excited for the task, I scrambled to create something quickly. I turned to the Rails App Composer for help. It integrates many boilerplate templates for a basic web app, fast. I found the perfect one: <a href="https://github.com/RailsApps/rails-bootstrap">Rails-Bootstrap</a>. It incorporates basic Bootstrap 4 and uses Rails 5.1. For more information, see the Github link. 

I needed a countdown plugin. Fast. So, I went to Github and typed in 'countdown' and got loads of results. I narrowed it down to find something in Ruby, but didn't find much usable code. So, I searched for 'countdown rails' and found a few gems such as 'countdown'. 

After fooling around with 'countdown', I discovered that the .js file was empty except for 'alert("test")' and this was not helpful. It also had minimal documentation. 

I tried another gem, <a href="https://github.com/mauriciopasquier/jquery-countdown-rails">'jquery-countdown-rails'</a>. This did not work as easily as I'd like it to. After fooling around with it in the web app, I decided there must be better options. 

This is when I found <a href="https://github.com/hilios/jQuery.countdown">jQuery.countdown</a>. I followed the documentation <a href="http://hilios.github.io/jQuery.countdown/">here</a>, and it worked perfectly. Within minutes, I had a working countdown.

Now, I just had to get the parameters on the time working properly. 
I had a bit of trouble because I discovered military time was used
and had to adjust for the target time. 

## The Future & Heroku Deployment
I edited Bundler version. Edited Gemfile from 'sqlite3' to 'pg' and edited the 'database.yml' file. To deploy, I used 'git push heroku master'. 

Now, I was able to deploy to Heroku without throwing me an error, however the javascript did not deploy properly and is not visible. 

The result is that it works locally, but not in production right now. 

## Looking Back

All in all, it took about an hour or so to create the web app. I'm pretty satisfied with it. In the future, I'd like to add styling of the countdown that resembles a old school ticker clock and maybe scrap the calendar data for start times of lectures to auto-regenerate the countdown depending on lecture automatically. However, I'm quite satisfied with how it stands now. 





