---
title: "ElasticSearch: Up and Running in under 20 minutes"
date: "2018-06-26T09:10:13.121Z"
layout: post
draft: false
path: "/posts/fifty-fourth-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about how to get ElasticSearch up and running, as well as implement a basic version of full-text search."
---

This is a quick post about getting implementations of ElasticSearch up and running in under 20 minutes, assuming you are using OS X. 

<h2>1) Install ElasticSearch.</h2>

Make sure you have Java 8 installed. Check your Java version by running `java -version`. Install Java 8 from <a href="https://java.com/en/download/">this download</a>. 

To install ElasticSearch, run the following: 
`brew install elasticsearch`

If you do not have Homebrew installed, go ahead and install it <a href="https://brew.sh/">here</a>.

After this, go ahead and run `elasticsearch` in the console.

<h2>2) Run a command</h2>

`rails new searchapp --skip --skip-bundle --template https://raw.github.com/elastic/elasticsearch-rails/master/elasticsearch-rails/lib/rails/templates/01-basic.rb` for a basic setup demo

<h2>3) Run a long command</h2>

`rails new searchapp --skip --skip-bundle --template https://raw.github.com/elastic/elasticsearch-rails/master/elasticsearch-rails/lib/rails/templates/02-pretty.rb` in the same folder as the other project to see Bootstrap styles added, result highlighting etc. 

<h2>4) Run another long command </h2>

`rails new searchapp --skip --skip-bundle --template https://raw.github.com/elastic/elasticsearch-rails/master/elasticsearch-rails/lib/rails/templates/03-expert.rb` in the same folder to see a use case with a couple of hundred NYTimes articles. 

In order to run the last one, you need to be running a Redis server concurrently with the rails server and elasticsearch. 

<h2>Resources</h2>

See Redis quickstart <a href="https://redis.io/topics/quickstart">here</a>.
See ElasticSearch-Model gem github <a href="https://github.com/elastic/elasticsearch-rails/tree/master/elasticsearch-model">here</a>.
See ElasticSearch-Rails gem github <a href="https://github.com/elastic/elasticsearch-rails/tree/master/elasticsearch-rails#rails-application-templates">here</a>. 


