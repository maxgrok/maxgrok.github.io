---
title: "How to Fix the OpenSSL issue in RVM in Mojave"
date: "2019-05-06T14:10:13.121Z"
layout: post
draft: false
path: "/posts/ninety-sixth-post/"
category: "RVM"
tags:
  - "RVM"
  - "OpenSSL"
  - "Mojave"
description: "This is a short post about how to fix the OpenSSL issue with installing Ruby versions."
---
My environment: 

RVM version 1.29.7
Ruby version - any would reproduce this error. 

Over the weekend, I kept getting this error: 
`ERROR:  While executing gem ... (Gem::Exception) Unable to require openssl, install OpenSSL and rebuild ruby (preferred) or use non-HTTPS sources`

I got this error even after installing `brew install openssl`.

At first, I went to the error url that was linked in the rest of the [error message](https://rvm.io/rvm/autolibs). However, I just got information about autolibs, not how to fix the OpenSSL issue. 

I kept Googling and found several options. 

I'll go over the ones that didn't work for me. 

This [StackOverflow post](https://stackoverflow.com/questions/15511943/troubles-with-rvm-and-openssl) suggested the following: 
```
rvm pkg install openssl
$ rvm remove rubyversion
$ rvm install rubyversionhere --with-openssl-dir=$HOME/.rvm/usr
$ gem install bundler
```

However, this did not work for me. I still got the OpenSSL error. 

What worked for me was the following command and running it to install each version of Ruby. 

``` 
rvm install rubyversionhere --with-openssl-dir=`brew --prefix openssl`
```

I already have Homebrew installed and also already ran `brew install openssl@1.1`, which is the latest stable version of OpenSSL available. 

Hopefully, this saved you some time finding the answer to this obscure error! 

