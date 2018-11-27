---
title: "How to Build a Basic JSON API"
date: "2018-05-30T09:14:13.121Z"
layout: post
draft: false
path: "/posts/thirty-sixth-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post that walks through building most of a Rails JSON API from scratch."
---

<h2>Learning update!</h2>
<div class="container">
    <p>During Module 3, we have been focusing on DOM manipulation, promises (ex. fetch), async, and building Rails JSON APIs from scratch. </p>
    <p>In the Module 3 project, I am making a review site with a backend and frontend, then connecting the two via fetch requests. </p>
    <p>So, I am going to walk through how to make most of the backend JSON API for this project with Rails!</p>
</div> 

<h2>Here is the overarching details for the total project: </h2>

<h3>Specs: </h3>
<div class="container"><p>- Must be a Single Page Application (SPA)</p></div>

<h3>Domain: </h3>
<div class="container">
<ul>
<li> A property has many reviews</li>
<li> A property has a name, description, phone number, address, website</li>
<li>Each review belongs to a property </li>
<li>Each review has a title and content</li>
</div>

<h3>User stories:</h3>
<div class="container">
    <ul>
    <li>A user may create, read, update, and delete properties </li>
    <li>A user may create, read, update, and delete reviews of properties</li>
    <li>A user can view only 50 properties at a time and can click a button to view more properties</li>
    <li>Stretch Goal: A user may search through properties using a filter that actively updates based on typing into a search box.</li>
    <li>Stretch Goal: All properties are organized into cards that display 4x4 in a grid pattern on the page with photos using Semantic-UI</li>
    </ul>
</div>
<h1>Let's start!</h1>
<div class="container">

1) Enter your CLI and run `rails new yelp-api --database=postgresql --api -T` to generate the application in the directory of your choice. 

2) `cd` into that directory

3) check your gemfile and uncomment the `gem rack-cors` gem and add the `gem active_model_serializers` gem, also include `gem 'faker'` (for later) then run `bundle install` again. When done, continue to the next step.  

4) in `config/initializers/cors.rb`, uncomment the and edit the following to look like this: 

```ruby
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
   origins '*'
    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end 
```

5) Next, let's tackle routes. Head to the `config/routes.rb` file and namespace your routes for inclusion of 'api' and the version ('v1') like this: 
```ruby 
namespace :api do 
    namespace :v1 do 
        resources :properties
        resources :reviews
    end
end 
```

6) Let's make our controllers. Run `rails g controller api/v1/Properties ` and `rails g controller api/v1/Reviews` in your CLI. 

7) Now, let's head to the controllers in `app/controllers/api/v1/`. 

You should see something like this in `app/controllers/api/v1/properties_controller.rb`

```ruby
 class Api::V1::PropertiesController < ApplicationController
end 
```  

Let's add some instructions for the controller in between the class declaration and the end. Like this: 

```ruby
 before_action :find_property, only: [:update]
  def index
    @property = Property.all
    render json: @property
  end

  def update
    @property.update(property_params)
    if @property.save
      render json: @property, status: :accepted
    else
      render json: { errors: @property.errors.full_messages }, status: :unprocessible_entity
    end
  end

  private

  def property_params
    params.permit(:name, :description, :phone_number, :website, :address)
  end

  def find_property
    @property = Property.find(params[:id])
  end 
```

8) Do the same thing for reviews. Like this: 

```ruby
 before_action :find_review, only: [:update]
  def index
    @review = Review.all
    render json: @review
  end

  def update
    @review.update(review_params)
    if @review.save
      render json: @review, status: :accepted
    else
      render json: { errors: @review.errors.full_messages }, status: :unprocessible_entity
    end
  end

  private

  def review_params
    params.permit(:title, :content)
  end

  def find_review
    @review = Review.find(params[:id])
  end 
```

9) Let's create our models by running `rails g model Property name description address phone_number website` and `rails g model Review title content` in the CLI. 

10) Let's run `rails db:create && rails db:migrate` to update and create our database in Postgres. Important: If you are not running the GUI Postgres, then the database will not run in your `rails s` command. You will get an error. So, please be sure to download Postgres first. 

11) Test out your database using `rails c` and then try `Property.create(name: "McDonalds", ...)` then run `Property.all` and it should appear! Do the same thing to test out reviews. 

If you run `rails s`, then go to `localhost:3000/api/v1/properties` you will not see anything if you didn't do `Property.create(insert params here)`! Let's fix that with some seed data. 

12) Let's use the faker gem we included in our gem file to create data for the backend database. Go to `db/seeds.rb` and type in the following: 
```ruby
 beachhouse = Property.create(name: Faker::Name.unique.name, description: Faker::Company.unique.bs, address: Faker::Address.unique.street_address,phone_number: Faker::PhoneNumber.unique.cell_phone,website: Faker::Internet.unique.url)
review = Review.create(title: "Five Guys Was Awesome", content: "Best french fries ever!") 
```

13) run `rake db:seed` to migrate the data to the database. 

14) Now run `rails s` and navigate to your endpoint(`localhost:3000/api/v1/properties` or `localhost:3000/api/v1/reviews`). You can also check your routes using `rails routes` to see which routes work. You should see something like this for properties: 
```ruby 
[
    {
    id: 1,
    name: "Five Guys",
    description: "Good burger joint",
    address: "10001 Liberty Rd., Baltimore, MD, 21210",
    phone_number: "410-510-2390",
    website: "https://www.fiveguys.com/",
    created_at: "2018-05-29T19:00:32.364Z",
    updated_at: "2018-05-29T19:00:32.364Z"
    },
    {
    id: 2,
    name: "Alaina Bradtke",
    description: "target cutting-edge technologies",
    address: "268 Nikolaus Brooks",
    phone_number: "696.501.1132",
    website: "http://halvorson.name/fiona_kaulke",
    created_at: "2018-05-29T19:11:44.965Z",
    updated_at: "2018-05-29T19:11:44.965Z"
    }
    ] 
```

This is great! That's our JSON data that we get by sending a GET request to our API! It's working! 

Hint: If you want to see something prettier, feel free to download the JSONView extension for Chrome or something similar for your own browser. This will help you view JSON data easier and prettier! 

15) If you want to continue building out the project, you will need to build the relationship working between reviews and properties, as well as make specific configurations for the PostSerializer. 

That's it! Now, you have most of the backend JSON API for a review site! You can make fetch requests to it in the JS in the front-end, while the rails server is running. 

<h1>Congratulations! You're done! </h1>
</div>

