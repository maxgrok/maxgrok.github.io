---
title: "How to Publish Your First NPM Package"
date: "2019-04-11T13:44:13.121Z"
layout: post
draft: false
path: "/posts/ninety-second-post/"
category: "NPM"
tags:
  - "NPM"
  - "Node.JS"
  - "NPM package"
description: "This is a post is about how to make a publish a package to NPM registry."
---

Today, we'll be going through how to publish an NPM package. It will be quick and easy! 
We will be presuming you know basic npm and have node and npm and git installed. 

## Follow these steps to build your first NPM package: 

(1) Create a git repository in a new folder by running `git init`. 
(2) Create a git repository on Github using the name of the package you want to create. (Go to Github.com and click 'Create a New Repository' in your user account. Google around for Github help if you have trouble.)
(3) Run `git remote add origin` and then add the https address or ssh address of your github repo. This syncs the git repo with your local repo for all changes. 
(4) Run `npm init` inside the same directory. This creates the `package.json` file for your npm package.
(5) Answer all the publishing questions about the description of the package, name of the package, version of the package (use semantic versioning), license, and author.
(6) Run `git add .` to stage the changes in the directory for commiting. 
(7) Run `git commit -m "adding package.json"` in your command line, still in the same root directory. 
(8) Run `git push origin master` to push the changes already made. 
(9) Write your node module in your own index.js file. 
(10) `git add .` , `git commit -m "changes"`, `git push origin master` to update with your code. 
(10) When you are done with your code, run `npm publish` to publish your package. 
(11) Lastly, add the tag with the same version that you started the repo with in your npm init. i.e. 1.0.0 is the default. Run `git tag 1.0.0` to tag that version. 

To verify that your package was published:
(1) Run `npm info packagenamehere` which will bring you to the package location in a browser. 
(2) Run `npm repo packagenamehere` to go to the repository of the package. 

## Congratulations! You have published your first NPM package! 

Source: <br/>

<a href="https://app.pluralsight.com/library/courses/npm-playbook">NPM Playbook" by PluralSight.</a>

