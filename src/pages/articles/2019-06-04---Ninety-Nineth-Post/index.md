---
title: "Testing a Sidekiq Worker"
date: "2019-06-04T9:30:13.121Z"
layout: post
draft: true
path: "/posts/ninety-nineth-post/"
category: "Sidekiq"
tags:
  - "Rspec-sidekiq"
  - "Sidekiq"
  - "Rails"
description: "This is a post about how to test a Sidekiq worker with Rails and rspec-sidekiq."
---

## Introduction 
 
Sidekiq runs background jobs for Rails apps. Officially, Sidekiq is "simple, efficient background processing for Ruby"(<a href="https://github.com/mperham/sidekiq">Sidekiq</a>).

In a Rails app, I was working on I was tasked with building a sidekiq worker that sent an in-app notification and an email in the future to users for a To Do list. 

So, I'm going to help others who may Google for how to test a Sidekiq worker, especially at a specific time.  

## Configure Your Rails App 

<a href="https://github.com/philostler/rspec-sidekiq">`rspec-sidekiq`</a>

<a href="https://github.com/mperham/sidekiq/wiki/Testing">Sidekiq Testing</a>

in `rails_helper.rb`, include: 
```ruby

```

## Writing Your Tests 

## Example Test

```ruby
```

## Running Your Tests

`rspec path/to/file`

`rails c` 
`require 'sidekiq/testing'`
--> true

<br/>

## Further Reading

<a href="https://github.com/mperham/sidekiq">Sidekiq</a><br/>

<a href="https://github.com/mperham/sidekiq/wiki/Testing">Sidekiq Testing</a>

<a href="https://github.com/philostler/rspec-sidekiq">rspec-sidekiq</a>