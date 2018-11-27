---
title: "Building atRest w/ Rails"
date: "2018-06-14T10:05:13.121Z"
layout: post
draft: true
path: "/posts/forty-nineth-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about how to build a Rails backend for an house sharing application."
---

I'm leaving a large portion of this app up to you to design and configure. My main goal is to walk through the steps required to setup this application properly, rather than hand hold. 

<h2>Where to begin? </h2>

We need to make a domain model, ActiveRecord associations, create and migrate the database, and test our associations to make sure they work. 

For this we're going to be using Rails 5.2, postgresQL, ActiveRecord (comes with Rails), and our knowledge of foreign keys. 

Here are the stories we need to build relationships for: 

A Host has many locations. 
A Donor has many donations. 
A Donor has many stays through donations. 
A guest has many stays. 
Stays have many reviews. 
Locations has many stays. 

User stories for our application: 
A Host should be able to CRUD* a location (a.k.a. a listing) and stay that belongs to that location, as well as reviews authored by them for particular stays that belong to their location. 
A Donor should be able to CRUD* a donation and a review that belongs to that donation. 
A Guest should be able to CRUD* a stay and a review. 

A User should be able to search through listings according to filters. 
A User should be able to see all the locations in cards displayed on the view (front-end)
A User should be able to login and signup. 

*CRUD stands for 'Create, Read, Update, Delete'

<h2>Building the Backend</h2>

Ok, let's get started. 

<h2>First</h2>, we need to make our domain model for all these relationships/associations. 

Here is the map out of our basic relationships. 

<blockquote class="imgur-embed-pub" lang="en" data-id="a/Y94ApmY"><a href="//imgur.com/Y94ApmY"></a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

<h2>Second</h2>

Let's make our app first with a postgresQL database by running 
`rails new YOURAPPNAME --database=postgresql` 

<h2>Third</h2>

Next, let's generate some models for our database. 

`rails g model *MODELNAMEHERE* component:type component:type`

Where component is the name of the type of data you want, for example, `name` and type is the type of data it is such as `string` or `integer`. 

<h2>Fourth</h2>

Once you have your models, then go into `app/models/` and write out your associations in each file. For example, here is my `app/models/user.rb` file. 

```ruby
class User < ApplicationRecord
    has_many :locations, :foreign_key => 'host_id'
    has_many :stays, :foreign_key => 'guest_id'
    has_many :stays, through: :locations, :foreign_key =>'host_id'
    has_many :reviews, :foreign_key =>"guest_id"
    has_many :donations, :foreign_key=>"donor_id"
end
```

ActiveRecord makes this super simple. For more information on ActiveRecord Associations, visit the Rails Guide <a href="http://guides.rubyonrails.org/association_basics.html">here</a>.

<h2>Fifth</h2>

Go into `rails c` and test your associations. Generate some fake data and see if you have all the methods you expect to have working. 

For example, I'm using some seed data that I manually generated in `app/db/seeds.rb` then run `rails db:seed` when you are done! 

<h2>Sixth</h2>

Make your controllers for your models!

`rails g controller CONTROLLERNAME`





