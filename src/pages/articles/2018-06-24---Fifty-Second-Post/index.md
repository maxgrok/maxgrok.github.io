---
title: "Gryd: Redesign and Preview"
date: "2018-06-24T11:20:13.121Z"
layout: post
draft: false
path: "/posts/fifty-second-post/"
category: "Venture"
tags:
  - "Venture"
  - "Gryd"
  - "GIS"
description: "This is a post about Gryd and the effort to reboot and redesign it using OpenStreetMaps and Mapbox."
---
<h2>Introduction</h2>

Now that I've learned JavaScript, I can build maps better, quicker, faster. In an effort to reboot Gryd (<a href="http://www.grydit.com/">Grydit.com</a>), I am redesigning it from the ground up. 

In this post, I'll describe the pros and cons of various stages of development for each version so far built. 

<hr>
<h2>Pre-Gryd: </h2>

![batchgeo](./batchgeo.png "batchgeo")

<a href="https://batchgeo.com/map/672a84f01140f0fb38527e2d1206ada3">pre-Gryd Map</a>

<h3>General Description</h3> 

You can search by any point of data included in the CSV/XLSX file included into the BatchGeo API on the upper right hand corner. The map markers are general Google Maps markers. There is not any directions between points. You can locate yourself on the map though and zoom in and out. It's relatively responsive in it's design. 

<h3>Cons</h3> 

Obscure web address makes it relatively inaccessible. You cannot update the data with the free version. You need to create an entirely separate map. The way that the CSV/XLSX data is imported make it difficult to have multiple types of categories with different markers. Search categories are limited as well to the points of data categories of the columns in the CSV/XLSX data. 
There are no reviews available for each location. It has potentially out of date information, as the POIs haven't been updated in a couple of years. 

Gryd v1: 

![grydv1](./gryditcom.png "Gryd v1")

<a href="http://grydit.com/testindev/index.php?query=Food">Gryd v1</a>

<h3>General Description</h3> 

There are a lot of special search features in this version. You can search for 'breakfast, lunch, dinner', by name, address, phone number, website, etc. It has an accessible web address. 

<h3>Cons</h3> 

It's not terribly responsive in its design. The map markers do not differentiate between different categories. There are no directions between points and you cannot locate yourself on the map to see your location. 
It does use highly reliable maps via Leaflet.JS and OpenStreetMaps. 
There are no reviews available for each location. It has potentially out of date information, as the POIs haven't been updated in a couple of years. 

Gryd v2: 

![grydv2](./grydv2.png "Gryd v2")

Link: Not yet deployed. 

<h3>General Description</h3> 

You can find yourself on this map. You can get directions between points. Styling is upgraded and it is relatively responsive in its design. 
It's made with the latest tech and is a web app, which means it's designed using RESTful architecture. There are custom markers that have good style for the food places. On click, a user is flown to the individual map marker with details on the location. 

<h3>Cons</h3>

There are only three points currently on the map. Reformating all the data from Gryd v1 will take sometime because of the database schema and geoJSON requirements for Mapbox and to get the same data to be available. Search is not yet developed for it. It's a work in progress. There are no review features available just yet for individual locations. 

<hr>

<h2>Conclusion</h2>

Overall, I'm excited to move forward with development and am very optimistic about the outcome of its utility for those who are on the ground in Baltimore looking for places to go. 

Features to be developed in v2: 
- Search
- Reviews
- User Authentication

I look forward to developing these features in the coming months!




