---
title: "charmCityJS: Webpack, Slack Bots, and more..."
date: "2017-01-05T12:46:37.121Z"
layout: post
draft: false
path: "/posts/tenth-post/"
category: "Flatiron School"
tags:
  - "Javascript"
  - "Meetup"
description: "This is a post about a meetup for Javascript coders in the Baltimore area."
---
<strong>TL;DR  Last night, I had the pleasure of attending the <a href="https://www.meetup.com/charmcityjs/events/228557319/">charmCityJS monthly meetup</a> for the first time. I met nice people and heard three talks related to Javascript. Looking forward to future meetups! </strong> <br><br>

<strong>1. Javascript and Open Source Hardware</strong><br><br>

John Eisenhardt delivered the first talk on Javascript and open source hardware ("charmCityJS Meetup"). I'd heard of <a href="https://processing.org/">Processing</a> and <a href="https://www.arduino.cc/">Arduino</a>'s, even read a tutorial on <a href="https://www.arduino.cc/en/Tutorial/Blink">how to turn on a light</a>("Blink"). Yet I have not used them. He introduced his own open source hardware design component. He encouraged attendees to experiment open source hardware components to develop better Internet-of-Things devices. Through his experimentation, he has noticed that development is not accessible. Though software has improved, it is clear that the IoT is not where it could be. It needs to be more user-friendly for Javascript developers. He sees this as a task for current developers working with open source hardware. <br><br>

I have questions like: What type of software would one need to use to develop? Would it be regular nodeJS or something more specific to the component? What kinds of components are best to start out with? How long would it take to build something like what was presented for an amateur?<br><br>

<strong>2. Making imaginary modules real with Webpack and Babel</strong><br><br>

This talk was delivered by Mark Brocato. I hadn't heard of Babel or Webpack or modules before this talk. <br><br>

Someone that I met at the talk mentioned that Webpack was like Grunt except larger in scope. <br><br>

I had heard of Grunt before, but had attributed it to being like a package manager, when, in fact, it is a taskrunner. I had several questions.<br><br>

What is a taskrunner?<br><br>

A task runner is a way to run automation for activities such as minification for javascript files. This makes one's job easier by saving time. According to the GruntJS site, a taskrunner is used to "automate just about anything with a minimum of effort" (Grunt: The JavaScript Task Runner."). Another task runner is Gulp. According to his Quora answer, Matthias Peter Johansson says that "Gulp does essentially the same thing as Grunt but with a more modern interface (streams)"("What are the differences between Grunt and Gulp.js?"). <br><br>

Why use a taskrunner? <br><br>

To paraphrase the GruntJS site, the less repetitive work you need to do, the easier your javascript developing job becomes ("Grunt: The JavaScript Task Runner."). <br><br>

What is <a href="https://github.com/webpack/webpack">Webpack</a>?<br><br>

According to <a href="https://www.quora.com/What-is-webpack">Juho Vepsäläinen</a>, author of "SurviveJS - Webpack and React", "In short Webpack is a module bundler. It takes in a bunch of assets (ie. source, images, markup, CSS, ...) and turns that into something you can provide to the client"("What is webpack?"). <br><br>

What is <a href="https://babeljs.io/">Babel</a>?<br><br>

Babel, as explained by the speaker last night, transpiles javascript from ES6 to ES5. Why do this? It makes it more easy to read by several different browsers, rather than its updated version. Babel is a popular transpiler for accomplishing this task. It is used by AirBnb, Yahoo!, ZenDesk, SoundCloud, etc.  According to <a href="https://www.quora.com/What-exactly-is-BabelJs-Why-does-it-understand-JSX-React-components">Martin Velchevski</a>[^10].,"you need Babel because browser vendors are slow to adopt new language features, thus browser support for ES6 (at the moment of writing this) is quite poor"("What exactly is BabelJS? Why does it understand JSX React components?").  <br><br>
What is a module? <br><br>

"Modules divide programs into clusters of code that, by some criterion, belong together"(Haverbeke). <br><br>

In Flatiron, I'm covering object-oriented Ruby. At first, I thought of modules as similar to classes. I searched for the similarities and differences between Ruby Classes and Javascript Modules. Find them  <a href="http://stackoverflow.com/questions/151505/difference-between-a-class-and-a-module#9778021">here</a>("Difference between a class and a module"). The main takeaway from that link is that classes concern objects, modules concern functions. As <a href="http://stackoverflow.com/questions/151505/difference-between-a-class-and-a-module#9778021">scottru</a> points out, modules are about providing methods you can use across classes; think of them like "libraries" in Rails ("Difference between a class and a module"). <br><br>

What is a library in Rails? <br><br>

I haven't covered Rails yet. I completed two courses on it through Codecademy. We did not go over libraries. We went over saving data, associations, and authentication ("Learn Ruby on Rails", "Ruby on Rails: Authentication"). <br><br>

I searched for what a library in Rails actually is. I'm going to assume that a library in Ruby is the same as a library in Rails. According to the <a href="https://www.ruby-lang.org/en/libraries/">Ruby-lang site</a>, libraries release as gems ("Libraries"). I know how to install gems via the bundler; I do not know what they actually are, except that they are external code. <br><br>

I searched for what a computing library is. "In computer science, a library is a collection of non-volatile resources used by computer programs, often to develop software. These may include configuration data, documentation, help data, message templates, pre-written code and subroutines, classes, values or type specifications. In IBM's OS/360 and its successors they are referred to as partitioned data sets.[...] A library is also a collection of implementations of behavior, written in terms of a language, that has a well-defined interface by which the behavior is invoked." ("Library").<br><br>

A gem could be described as a released library. Gems consist of combination of code, documentation, and a gemspec ("Structure of a Gem". It consists of a lib directory (contains the code), test directory (contains tests), bin directory (for executable files), README (documentation), and rakefile ("Structure of a Gem"). <br><br>

<strong>What the talk was about:</strong><br><br>

Creating imaginary modules with webpack and babel was a talk about creating clusters of code that, by some criterion, belong together using the module builder, Webpack, and transliterating it using Babel for ES5 compatibility with ES6. It was called imaginary modules because it is not currently possible to use the functionality described with the ExtJS framework with React, so adaptations implemented provided functionality for its use.  <br><br>

The way that React - I haven't studied React beyond the beginning of a tutorial - is includes libraries with JSX is not compatible with ExtJS components. In order to use ExtJS components, the speaker created workarounds using Webpack and Babel. This is why the talk is entitled "Creating Imaginary Modules with Webpack and Babel". <br><br>

The speaker went over specific code that would allow for this functionality with the current version of ES6. <br><br>

I have questions like the following: What is JSX? What does ExtJS actually do? Why use React over Angular? What is ES6? Why is it important? What does a production workflow look like? Is there a difference between using Git for production and using it to have simple version control? What does a typical professional deployment look like? <br><br>

While I don't yet understand the code presented, I'm excited to continue learning and pursue those answers in the future when I reach the React section of my curriculum. <br><br>

<strong>3. Slack Bots for Fun and Profit </strong><br><br>

In this talk, Cole Furfaro-Strode went over how he built slack bots. Slack is an IRC client that has become really popular lately. Bots are automatic interactors with human chatters. Slack bots are bots within a Slack channel. He emphasized that building Slack bots is an interaction first design process. Think about what would a bot say in response to the user. Create a decision tree, if necessary, to articulate this. Keep in mind the purpose of the bot. Aim for them to be humble, helpful, appropriately funny, and warm to the user. Avoid snark and being cutesy. They are difficult to pull off and get old quickly.  <br><br>

In code, he also emphasized that interactions come first for the user or anyone else who will need to read the code. This is why he created skellington, which simplifies the process of making a Slack bot from several hundred lines of code to 15. <br><br>

I have questions like the following: What does a typical interaction look like? What does a decision tree for a bot look like? How do you know if your bot is hhafw? Does skellington work on a large enough scale that it is commercially applicable?<br><br>

<strong>In Conclusion</strong><br><br>

I'm happy to have attended the talk. I am curious about making my own open source hardware, coding modules using webpack and babel, and making Slack bots now.  In the future, I'll be happy I attended this talk, especially as I cover React. I am glad to have been exposed to new ideas and new questions. <br><br>

<a href="http://www.baltimorenode.org/">Baltimore Node</a> is hosting a Microcontroller Monday talk soon. I may attend and fool around with an Arduino. <br><br>

I learned that the charmCityJS group has a slack channel, then I joined it today. There are over 250 participants! Excited to meet more javascript developers!<br><br>

Thanks for the stimulation! Looking forward to future meetups!<br><br>

<p style ="text-align:center">Works Cited</p>
"Arduino - Blink." Arduino - Blink. N.p., n.d. Web. 05 Jan. 2017. <a href="https://www.arduino.cc/en/Tutorial/Blink">https://www.arduino.cc/en/Tutorial/Blink</a>.<br>
"CharmCityJs." Meetup. N.p., n.d. Web. 05 Jan. 2017. <a href="https://www.meetup.com/charmcityjs/">https://www.meetup.com/charmcityjs/</a>.<br>
"CharmCityJs - Monthly Meetup." Meetup. N.p., n.d. Web. 06 Jan. 2017. <a href="https://www.meetup.com/charmcityjs/events/228557319/">https://www.meetup.com/charmcityjs/events/228557319/</a>.<br>
"Grunt: The JavaScript Task Runner." Grunt Blog. N.p., n.d. Web. 05 Jan. 2017. <a href="http://gruntjs.com/">http://gruntjs.com/</a>.<br>
Haverbeke, Marijn. "Chapter 10 - Modules." Modules :: Eloquent JavaScript. No Starch Press, 14 Dec. 2014. Web. 05 Jan. 2017. <a href="http://eloquentjavascript.net/10_modules.html">http://eloquentjavascript.net/10_modules.html</a><br>
Johansson, Mattias Petter. "What Are the Differences between Grunt and Gulp.js?" Quora. Quora, 4 May 2014. Web. 5 Jan. 2017.<a href="https://www.quora.com/What-are-the-differences-between-Grunt-and-Gulp-js">https://www.quora.com/What-are-the-differences-between-Grunt-and-Gulp-js</a>.<br>
"Learn Ruby on Rails." Codecademy. Codecademy, n.d. Web. 05 Jan. 2017. <a href="https://www.codecademy.com/learn/learn-rails">https://www.codecademy.com/learn/learn-rails</a>.<br>
Moore, Josh. "Difference between a Class and a Module." Ruby - Difference between a Class and a Module - Stack Overflow. StackExchange, 30 Sept. 2008. Web. 05 Jan. 2017. <a href="http://stackoverflow.com/questions/151505/difference-between-a-class-and-a-module">http://stackoverflow.com/questions/151505/difference-between-a-class-and-a-module</a>.<br> 
"Ruby." Libraries. Ruby-lang, n.d. Web. 05 Jan. 2017. <a href="https://www.ruby-lang.org/en/libraries/">https://www.ruby-lang.org/en/libraries/</a>.<br>
"Ruby on Rails: Authentication." Codecademy. Codecademy, n.d. Web. 05 Jan. 2017. <a href="https://www.codecademy.com/learn/rails-auth">https://www.codecademy.com/learn/rails-auth</a>.<br>
Velchevski, Martin. "What Exactly Is BabelJs? Why Does It Understand JSX/React Components?" Quora. Quora, 2 Dec. 2015. Web. 05 Jan. 2017. <a href="https://www.quora.com/What-exactly-is-BabelJs-Why-does-it-understand-JSX-React-components">https://www.quora.com/What-exactly-is-BabelJs-Why-does-it-understand-JSX-React-components</a>.<br>
Vepsäläinen, Juho. "What Is Webpack?" Quora. Quora, 15 June 2015. Web. 05 Jan. 2017. <a href="https://www.quora.com/What-is-webpack">https://www.quora.com/What-is-webpack</a>.<br>
"What Is a Gem? - RubyGems Guides." What Is a Gem? - RubyGems Guides. RubyGems, n.d. Web. 05 Jan. 2017. <a href="http://guides.rubygems.org/what-is-a-gem/">http://guides.rubygems.org/what-is-a-gem/</a>.<br>