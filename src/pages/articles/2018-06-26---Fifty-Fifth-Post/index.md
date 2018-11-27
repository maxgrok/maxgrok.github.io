---
title: "Integrating React into Rails 5.2"
date: "2018-06-26T14:22:13.121Z"
layout: post
draft: false
path: "/posts/fifty-fifth-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about how to integrate React into a Rails 5.2 project."
---

Here is how to integrate React into Rails 5.2 project. 

1) Add `webpacker` and `react-rails` gems to your Gemfile. 

2) Run installers

``` bundle install
$ rails webpacker:install       # OR (on rails version < 5.0) rake webpacker:install
$ rails webpacker:install:react # OR (on rails version < 5.0) rake webpacker:install:react
$ rails generate react:install
```

3) Add JavaScript pack between the head tag in `application.html.erb`

`<%= javascript_pack_tag 'application' %>`

4) Generate first component

`rails g react:component HelloWorld greeting:string`

5) Add your component to your view

`<%= react_component("HelloWorld", { greeting: "Hello" }) %>`

6) Run `rails g react:install`

You can now load your component in your Rails application. 

You should see 'Greeting: Hello!' once you run your `rails s` and view your page. 

Resource: React-Rails gem documentation <a href="https://github.com/reactjs/react-rails">here</a>.

