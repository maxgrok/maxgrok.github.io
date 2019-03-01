---
title: "Flatiron BnB: Module One Final Project"
date: "2018-04-09T13:10:13.121Z"
layout: post
draft: false
path: "/posts/thirty-first-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about the Module One Final Project I completed with Jerry Lee: a Flatiron Bnb CLI App."
---

To view the complete directions for the assignment, please read this: 
<a href="https://github.com/learn-co-students/guided-module-one-final-project-dc-web-031218">Guided Module One Final Project</a>

In order to complete the Module One Project, Jerry and I had several remote meetings collaborating on the Module One Final Project. To collaborate, we used PivotalTracker, git, Google Hangouts, and GitHub. <br>

We mapped out the course of the project to do's with PivotalTracker such as making the presentation, making the associations, etc., then checked them off as we went through the project. On GitHub, Jerry named me a collaborator, so I was able to push up code to the repo using 'git push origin master', after 'git clone'ing the repo on my computer. 

First, I built out an XML file for the domain model. We have users, reservations, and listings. (See below)<br>

<img src="/domain.png" alt="DomainModel"><br>

Next, I got the JSON data for NYC, LA, and DC through the <a href="https://stevesie.com/apps/airbnb-api">Stevies Unofficial Airbnb API</a>, then passed it along to Jerry who created the models.  
<br>

The data looks like this: 
<img src="/jsondata.png" alt="jsondata">

I created the associations between all the models and added them to the git repo. 

<img src="/listingassociations.png" alt="ListingAssociations"> <br>

<img src="/reservationassociations.png" alt="ReservationAssociations"> <br>

<img src="/userassociations.png" alt="UserAssociations"> <br>

We created the CLI interface to the application. 

Download the <a href="https://github.com/SaturdayAM/guided-module-one-final-project-dc-web-031218">Module One Final Project GitHub Repo</a>.

To run the application, run 'bundle install' from the command line while within the project folder. 

<img src="/bundleinstall.png" alt=""> <br>

Again, from within the project folder, run 'ruby bin/run.rb'. You should see the following: 
<img src="/CLIinterface.png" alt=""> <br>
    
Follow the directions to query, make reservations, make a user account, and use the application! 

Type 'exit' to exit the program. <br>
To see our Module One Project Presentation go here:<a href="https://www.slideshare.net/MaxGoodman7/module-one-guided-project-flatiron-school" title="Module One Guided Project - Flatiron School" target="_blank"><img src="/flatironbnb.png" alt=""></a> </strong></div>
