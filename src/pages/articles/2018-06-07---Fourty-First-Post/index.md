---
title: "Build A Real-Time Chat App: ActionCable/Rails"
date: "2018-06-11T12:40:13.121Z"
layout: post
draft: false
path: "/posts/forty-first-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about what websockets are and how to build a real-time chat app using websockets, specifically ActionCable, that works on your local machine."
---

In this blog post, I am going to teach you what websockets are and how to build a real-time chat web app with ActionCable in Rails 5. 

<h2>A little bit about why</h2>

I first heard of websockets when I was Googling around about real-time web applications becuase I was curious about real-time notifications and updates as features for web apps and how they were implemented. I initially learned what they were and how they came to be for my talk for <a href="http://maxgrok.netlify.com/posts/thirty-eighth-post/">Flatiron Presents: Websockets && ActionCable</a>. 

Since then, I've been reading up on it and became interested in implementing my own chat app. So, I've read a few tutorials, but this is the <a href="https://www.learnenough.com/action-cable-tutorial">best</a> in my opinion. 

Before we get started building, let's explore a few terms. 

<h2>What are Websockets? What is ActionCable? </h2>

The main distinction between the HTTP protocol and Websockets is the same as the difference between "half-duplex" and "full-duplex". 

<blockquote class="imgur-embed-pub" lang="en" data-id="a/EtgZCuV"><a href="//imgur.com/EtgZCuV"></a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

"Half-duplex" refers to the ability to communicate with the server one request at a time, whereas 'full-duplex' refers to the ability to communicate more than one request at a time with a bi-directional connection setup between the server and client that remains in constant communication. 

<blockquote class="imgur-embed-pub" lang="en" data-id="a/lpg6xIx"><a href="//imgur.com/lpg6xIx"></a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

Websockets are 'full-duplex', meaning that one client can send a message at the same time as another client and both messages will be rendered in real-time. 

ActionCable is simply Rails' implementation of Websockets protocol that was released by the HyPy group from <a href="https://tools.ietf.org/html/rfc6455">Google, Inc.</a> in 2011. 

For more information, see my other post on Websockets && ActionCable or these resources (<a href="https://blog.heroku.com/real_time_rails_implementing_websockets_in_rails_5_with_action_cable">Real-Time Rails</a>, <a href="http://edgeguides.rubyonrails.org/action_cable_overview.html">ActionCable Rails Guides</a>, <a href="https://hectorperezarenas.com/2015/12/26/rails-5-tutorial-how-to-create-a-chat-with-action-cable/">Rails 5 Tutorial</a>, <a href="https://youtu.be/n0WUjGkDFS0">DHH ActionCable Demo</a>).

<h2>How long will it take to build this chat app? </h2>

I'd allow about half a day to get familiar with the tutorial and build it if you have some familiarity with MVC and Rails. It took me about that much time to build. 

<h2>What was a challenge about building this chat app?</h2>

One of the challenges with building this app was reading the error messages coming from the `heroku logs` on the server. I had to debug those error messages for the first time and they show up in a different syntax, as well as use the CLI to debug deployment issues. 

For example: 
```markdown
2018-06-08T20:24:15.745182+00:00 app[web.1]: I, [2018-06-08T20:24:15.745070 #4]  INFO -- : [0a978a8a-103a-4e3c-8f0d-e4d584e37f29] Started POST "/messages" for 65.207.79.74 at 2018-06-08 20:24:15 +0000
```

Instead of:

```markdown
Started GET "/cable" for ::1 at 2018-06-11 11:55:44 -0400
Started GET "/cable/" [WebSocket] for ::1 at 2018-06-11 11:55:44 -0400
Successfully upgraded to WebSocket (REQUEST_METHOD: GET, HTTP_CONNECTION: Upgrade, HTTP_UPGRADE: websocket)
  User Load (0.5ms)  SELECT  "users".* FROM "users" WHERE "users"."id" = ? LIMIT ?  [["id", 1], ["LIMIT", 1]]
Registered connection (Z2lkOi8vY2hhdC1hcHAvVXNlci8x)
RoomChannel is streaming from room_channel
RoomChannel is transmitting the subscription confirmation
RoomChannel is streaming from room_channel_user_1
```

Otherwise, the tutorial is fairly straightforward to follow so long as you are familiar with MVC organizations for web apps. Even if you are not, Hartl does a great job of making it accessible and highlights key changes that occur at every step. 

<h2>See What We're Building First</h2>

It is under current development. In the meantime, see the app working in production here on <a href="https://nameless-springs-56756.herokuapp.com">Heroku</a>. 

You can sign up as any user with any password (atleast 6 characters) or use 'bob' (pwd:asdfasdf) or "alice" (pwd: wonderland). 

<h2>Let's Get Started!</h2>

<h3>Step 1) Download the base app <a href="http://www.github.com/mhartl/action_cable_chat_app.git">ActionCable Base Chat App</a>. 

Fork it and then clone the fork on your local repo. 

To clone it, use this command in your CLI: 
`git clone https://github.com/<username>/action_cable_chat_app.git`

<h3>Step 2) `cd` into your local repo</h3>

`cd action_cable_chat_app/`

<h3>Step 3) Run the necessaries</h3>

Run the following commands: 
`bundle install`    
`rails db:migrate`
`rails db:seed`

Then: 
`rails test` (all tests should be green)

<h3>Step 4) Go to the `app/controllers/messages_controller.rb` file</h3>

Go to `def create` and add the following just below the definition of the action: 

`message = current_user.messages.build(message_params)`
 
I chose to skip most of the javascript in the tutorial to the "Upgrading to ActionCable" section. Section 4. The purpose of the Javascript portion of the tutorial is to teach one why exactly websockets are an upgrade. Let's assume we feel the pain of polling and move forward. 

<h3>Step 5) Create a new branch</h3>

Enter `git checkout -b action-cable` into the CLI. This tells git that we are working on a new branch and we are now committing changes in that branch to be merged with `master` later. 


<h3>Step 6) Create the Rooms Channel</h3>

Run `rails generate channel Room`. 

If you want to get back to a blank slate for the app chat room, then run this : `rails db:migrate:reset && rails db:seed`

This command resets the database and reintegrates the seeds for the database. 

Go to `app/channels/room_channel.rb` file in your text editor. I use Sublime. 
You should see something like this: 

```ruby
# Be sure to restart your server when you modify this file.
# Action Cable runs in a loop that does not support auto reloading.
class RoomChannel < ApplicationCable::Channel
  def subscribed
    # stream_from "some_channel"
  end

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end
end
```

We want to subscribe to the Room channel that we just generated. 

So, we want to add this: `stream_from "room_channel"` to the `#subscribed` action. 

Our RoomChannel should look like this now: 

```ruby
# Be sure to restart your server when you modify this file.
# Action Cable runs in a loop that does not support auto reloading.
class RoomChannel < ApplicationCable::Channel
  def subscribed
    stream_from "room_channel"
  end

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end
end
```


<h3>Step 7) Edit the Messages Controller</h3>

Edit your MessagesController #create to look like this: 

```ruby 
def create
message = current_user.messages.build(message_params)
if message.save
  ActionCable.server.broadcast 'room_channel',
                               content:  message.content,
                               username: message.user.username
end
```

This allows ActionCable to send the content of the messages that a user enters as well as a username in the `room_channel`. 

<h3>Step 8) Editing Room.coffee</h3>

Go to `app/assets/javascripts/channels/room.coffee`

Here is what your file should look like before we edit it: 
```javascript
App.room = App.cable.subscriptions.create "RoomChannel",
connected: ->
# Called when the subscription is ready for use on the server

disconnected: ->
# Called when the subscription has been terminated by the server

received: (data) ->
```

To test that we received the data object, we will update the `received: (data) -> ` function to add an alert `alert data.content` like this: 

```javascript
App.room = App.cable.subscriptions.create "RoomChannel",
connected: ->
# Called when the subscription is ready for use on the server

disconnected: ->
# Called when the subscription has been terminated by the server

received: (data) ->
    alert data.content
```

To get this `alert` to work, we need to do one more step. 

<h3>Step 9) Mounting the ActionCable Server in Your Routes</h3>

Go to `config/routes.rb`. It should look like this: 
```ruby
Rails.application.routes.draw do
  root 'messages#index'
  resources :users
  resources :messages
  get    '/login',   to: 'sessions#new'
  post   '/login',   to: 'sessions#create'
  delete '/logout',  to: 'sessions#destroy'
end
```

Let's mount our ActionCable server in our routes: 

```ruby 
Rails.application.routes.draw do
  root 'messages#index'
  resources :users
  resources :messages
  get    '/login',   to: 'sessions#new'
  post   '/login',   to: 'sessions#create'
  delete '/logout',  to: 'sessions#destroy'

  mount ActionCable.server, at: '/cable'
end
```

This allows the application to know about our ActionCable server so that it can transfer information between your local system and the main Rails server. 

<h3>Step 9a) Using a Cloud IDE? Add this to your `config/environments/development.rb` file</h3>

```ruby
config.action_cable.allowed_request_origins = [
    'insertyourURLhere' ]
```

<h3>Step 10) REJOICE! </h3>

You have now built an ActionCable chat app that works on your local machine! 

To learn how to deploy it to production and add extended features such as login protection and SSL in production, follow 4.2 - 7 of the <a href="https://www.learnenough.com/action-cable-tutorial">Hartl tutorial</a> and follow <a href="https://www.railstutorial.org/book/sign_up#sec-professional_grade_deployment">Hartl's Professional Grade Deployment</a> guidelines. 

<h2>What did you specifically did you learn while building this chat app?</h2>

The main key takeway from this tutorial is that there are three main steps to setting up a Websocket. 

1) Setting up the channel. 
2) Making the coffeescript file for the rooms channel to function. 
3) Making edits to the rooms controller #create action to get the ActionCable to function properly.

Or in the words of Hartl:  
<blockquote>
"There are only three main steps needed to convert the base app to a working Action Cable chat app:

Make a channel to handle WebSocket connections on the server side (local server in development, Heroku in production).

Make a CoffeeScript program (room.coffee) for the chat room on the client side (web browser).

Update the Messages controller create action to broadcast changes to the channel instead of redirecting or rendering."</blockquote> 

<a href="https://www.learnenough.com/action-cable-tutorial">4 Upgrading to Action Cable by Michael Hartl</a>

<h2>I want to see your code! Where is your code repo?</h2>

<a href="http://www.github.com/maxgrok/action_cable_chat_app.git">ActionCable Chat App</a>

<h2>Is there screenflow of this app working in production?</h2>

It is under current development. In the meantime, see the app working in production here on <a href="https://nameless-springs-56756.herokuapp.com">Heroku</a>.

Update: here is the screenflow of the app! 

<iframe style="margin:0 auto;" src="https://player.vimeo.com/video/274697809" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
<p><a href="https://vimeo.com/274697809">ActionCable Websockets Real Time Chat App Demo</a> from <a href="https://vimeo.com/user86152978">Max Goodman</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

<h2>Questions or comments?</h2>

Feel free to reach out with any questions or comments <a href ="email:max.goodman@flatironschool.com">max.goodman@flatironschool.com</a> or find me on Twitter <a href="http://www.twitter.com/maxxgrok">here</a> to DM me about your own implementation of ActionCable Websockets. 

