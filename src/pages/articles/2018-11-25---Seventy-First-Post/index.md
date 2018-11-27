---
title: "Incorporating Materialize UI into Rails 5.2.1"
date: "2018-11-25T17:39:13.121Z"
layout: post
draft: false
path: "/posts/seventy-first-post/"
category: "Materialize UI"
tags:
  - "Rails"
  - "Materialize"
description: "This is a post about how to integrate Materialize UI into your Rails 5.2.1 app."
---

Navigate to your gemfile and add `gem 'materialize-sass'` in the general scope of the Gemfile. 

Run `bundle install` from the terminal within your project directory. This will install the Materialize-UI gem, which includes the javascript and scss files needed to incorporate this into your app.  

Edit: Additional Steps Required: 
Add `@import "materialize";` to your `app/assets/stylesheets/application.scss` file. 
Add `//= materialize` at the end of your `app/assets/javascripts/application.coffee` file. 
Add `//= materialize-sprockets` at the end of your `app/assets/javascripts/application.coffee` file.

Run `rails assets:precompile`

Restart/start running your project with `rails s` to ensure the changes are made. 

Enjoy your new Materialized project! 
