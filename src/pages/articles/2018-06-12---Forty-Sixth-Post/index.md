---
title: "Three Types of DOMs Explained"
date: "2018-06-12T08:10:13.121Z"
layout: post
draft: false
path: "/posts/forty-sixth-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about the difference between the virtual DOM, shadow DOM, and the real DOM."
---

I'm just starting to learn React and learning about the virtual DOM. I tried Google-ing around for best answers to the question of what exactly is the difference between the virtual DOM, the real DOM, and the shadow DOM. I couldn't really find too much in one place. 

So, I decided to do a dive into the exact differences between the virtual DOM, shadow DOM, and the real DOM myself. Let's start with the basics. 

<h2>1) The Real DOM</h2>

<strong>DOM is short for Document Object Model</strong>. "The Document Object Model (DOM) is a cross-platform and language-independent application programming interface that treats an HTML, XHTML, or XML document as a tree structure wherein each node is an object representing a part of the document. The objects can be manipulated programmatically and any visible changes occurring as a result may then be reflected in the display of the document."

(<a href="https://en.wikipedia.org/wiki/Document_Object_Model">Document Object Model - Wikipedia</a>)

Most web browsers use something similar to the DOM and organizes each document into a tree of nodes, "the DOM tree" (<a href="https://en.wikipedia.org/wiki/Document_Object_Model">Document Object Model - Wikipedia</a>). 

For Javascript, which is what we will be focusing on in this writing, it represents the document that is loaded when the page is loaded, providing an "object-oriented representation of an HTML document, that acts as an interface between JavaScript and the document itself and allows the creation of dynamic web pages"(<a href="https://en.wikipedia.org/wiki/Document_Object_Model">Document Object Model - Wikipedia</a>). JavaScript can CRUD (Create, Read, Update, Delete) any object on the page loaded in the DOM, as well as react to all the changes in the page loaded such as state changes. 

An example of the DOM tree is below: 

<blockquote lang="en" data-id="a/NxMx5hF"><a href="//imgur.com/NxMx5hF"></a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script> 

<a href="https://www.w3.org/TR/WD-DOM/introduction.html">W3C "What is the Document Object Model?"</a>

<h2>A Brief History Lesson on the DOM</h2>

The DOM was standardized by the World Wide Web Consortium with it's last recommendation dating back to 2004 (<a href="https://en.wikipedia.org/wiki/Document_Object_Model">Document Object Model - Wikipedia</a>). The <a href="https://en.wikipedia.org/wiki/WHATWG">WHATWG</a> has made the standard a living document and superceded the W3C standard recommended in 2004.

<h2>Problems with the DOM</h2>

It is really slow. The virtual DOM is a "really clever workaround to the DOM being slow."(<a href="https://learn.co/tracks/web-development-immersive-2-0-module-four/react/what-is-react/virtual-dom">Learn Co. Curriculum - Virtual DOM</a>) Due to increasingly dynamic web pages, we need to edit the DOM a lot, so this is a problem. (<a href="https://reactkungfu.com/2015/10/the-difference-between-virtual-dom-and-dom/">Difference between the Virtual DOM and the Real DOM</a>)

<h2>2) The Virtual DOM</h2>

The "Virtual DOM is a technique employed by several front-end libraries and frameworks, most notably React. In a nutshell, virtual DOM builds a virtual representation of what our document should look like." (<a href="https://learn.co/tracks/web-development-immersive-2-0-module-four/react/what-is-react/virtual-dom">Learn Co. Curriculum - Virtual DOM</a>)

It provides performance gains for sites by not touching and changing the DOM super frequently, and "when we do, we do it with surgical precision." (<a href="https://learn.co/tracks/web-development-immersive-2-0-module-four/react/what-is-react/virtual-dom">Learn Co. Curriculum - Virtual DOM</a>). 

It might be easier to think of the virtual DOM as an abstraction of the real DOM, "a local and simplified copy of the HTML(real) DOM"(<a href="https://reactkungfu.com/2015/10/the-difference-between-virtual-dom-and-dom/">Difference between the Virtual DOM and the Real DOM</a>). <strong> It allows React to do its computations within this local and simplified copy of the real DOM without the DOM operations (slow and browser-specific -- <a href="https://reactkungfu.com/2015/10/the-difference-between-virtual-dom-and-dom/">Difference between the Virtual DOM and the real DOM</a>). 

We've mentioned React, but what is React? How does it use the virtual DOM? 

<h2>What is React?</h2>

React "is a library for building composable user interfaces. It encourages the creation of reusable UI components which present data that changes over time." (<a href="https://reactjs.org/blog/2013/06/05/why-react.html">React Docs</a>). 

<h2>How is React different from just manually manipulating the real DOM?</h2>

"In a traditional JavaScript application, you need to look at what data changed and imperatively make changes to the DOM to keep it up-to-date. Even AngularJS, which provides a declarative interface via directives and data binding requires a linking function to manually update DOM nodes.

When your <strong>component</strong> is first initialized, the render method is called, generating a lightweight representation of your view. From that representation, a string of markup is produced, and injected into the document. When your data changes, the render method is called again. In order to perform updates as efficiently as possible, we diff the return value from the previous call to render with the new one, and generate a minimal set of changes to be applied to the DOM.

The data returned from render is neither a string nor a DOM node — it’s a lightweight description of what the DOM should look like."

(<a href="https://reactjs.org/blog/2013/06/05/why-react.html">React Docs</a>).

React breaks down building UIs into specific <strong> components</strong>.In other words, individual chunks of your application front-end can be represented by dedicated chunks of code that can change over time using a virtual DOM. In other words, "[r]eact components are small, reusable pieces of code that return a React element to be rendered to the page."

(<a href="https://reactjs.org/docs/glossary.html">React Docs - Glossary</a>). 

This means that instead of doing this: 

```javascript
lib.runApp(function(pageSet, allRows){
   // simulate updating model with server results, after a scroll
   pageSet.forEach(function(row){
       writeRow(row);
   });
});
``` 

We can do this: 

```javascript
lib.runApp(function(pageSet, allRows){
   // simulate updating model with server results, after a scroll
   _app.state.rows = allRows;
   _app.setState(_app.state);
});
```

Code snippet courtesy of <a href="https://objectpartners.com/2015/11/19/comparing-react-js-performance-vs-native-dom/">"Comparing React.js Performance vs. native(real) DOM"</a>

The virtual DOM "allows to [the real DOM to] collect several changes to be applied at once, so not every single change causes a re-render, but instead re-rendering only happens once after a set of changes was applied to the DOM."
<a href="https://www.laravel-vuejs.com/learn-the-differences-between-shadow-dom-and-virtual-dom/">Learn the differences between the shadow DOM and the virtual DOM</a>.

Ok, great. So now you know what the real/native/HTML DOM is as well as what the virtual DOM is in React. This leads us to our next question. 

<h2>3) The Shadow DOM</h2>

"Shadow DOM

Shadow dom is mostly about encapsulation of the implementation. A single custom element can implement more-or-less complex logic combined with more-or-less complex DOM. An entire web application of arbitrary complexity can be added to a page by an import and <body><my-app></my-app> but also simpler reusable and composable components can be implemented as custom elements where the internal representation is hidden in the shadow DOM like <date-picker></date-picker>.

Style encapsulation Shadow DOM is also about preventing styles being applied accidentally to elements the designer didn't intend to, for example because the CSS or components library you are using changed a selector that now applies to other elements that use the same CSS class names. Styles added to components are scoped to that component and bleeding out or in of styles is prevented.

Shadow DOM and performance

Even though shadow DOM is not about performance in the first place it also has performance implications. Because styles are scoped, the browser can make assumptions about some changes to affect only a limited area of the page (the shadow DOM of a custom element) which can limit re-rendering to the area of such a component, instead of re-rendering the entire page.

This is the reason the >>>, /deep/, and ::shadow CSS combinators, which allowed to apply styles across shadow DOM boundaries, were deprecated and are subject to be removed soon from Chrome (other browsers never had them AFAIK). The mere existence of these combinators prevents the kind of optimization mentioned in the previous paragraph"

(<a href="https://stackoverflow.com/questions/36012239/is-shadow-dom-fast-like-virtual-dom-in-react-js#36906251">"StackOverflow: Is shadow DOM fast like virtual DOM in React.js?"</a>).


"Shadow DOM is a tool that helps us to overcome DOM encapsulation on the native level. It’s not only about CSS, it is about elements as well." <a href="https://develoger.com/shadow-dom-virtual-dom-889bf78ce701">Shadow DOM != Virtual DOM</a>.

"An important aspect of web components is encapsulation — being able to keep the markup structure, style, and behavior hidden and separate from other code on the page so that different parts do not clash, and the code can be kept nice and clean. The Shadow DOM API is a key part of this, providing a way to attach a hidden separate DOM to an element. This article covers the basics of Shadow DOM."

(<a href="https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM"> MDN - Using shadow DOM</a>)

<h2>Where can you use the shadow DOM?</h2>

Here is the latest compatibility information: 

<blockquote lang="en" data-id="a/EscINUl"><a href="//imgur.com/EscINUl"></a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script> 

<a href="https://caniuse.com/#feat=shadowdomv1">Shadow DOM v1</a>

<h2>Summary</h2>

<strong>DOM is short for Document Object Model, which represents the way the document is loaded in an object-oriented fashion. <br><br>Virtual DOM is a local copy of the DOM that can be edited in batches of changes and provides relief from the real DOM. <br><br>Shadow DOM is about encapsulation, not performance, and is only really compatible with certain browsers right now.</strong>

<h2>Acknowledgements and References: </h2>

Thank you to Learn.co and the Flatiron School who continuously encourage me to deepen my learning and play. 

<p style="font-size: 1em"><a href="https://www.laravel-vuejs.com/learn-the-differences-between-shadow-dom-and-virtual-dom/">Learn the differences between the shadow DOM and the virtual DOM</a>,<a href="https://www.w3.org/TR/shadow-dom/">Shadow DOM w3c Docs</a>,<a href="https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM">Using Shadow DOM - MDN docs</a>,<a href="https://reactjs.org/blog/2013/06/05/why-react.html">Why React?</a>,<a href="https://reactjs.org/docs/glossary.html">React - Glossary</a>,<a href="https://stackoverflow.com/questions/36012239/is-shadow-dom-fast-like-virtual-dom-in-react-js#36906251">"StackOverflow: Is shadow DOM fast like virtual DOM in React.js?"</a>,<a href="https://www.laravel-vuejs.com/learn-the-differences-between-shadow-dom-and-virtual-dom/">Learn the difference between the shadow DOM and the virtual DOM</a>,<a href="https://en.wikipedia.org/wiki/Document_Object_Model">Document Object Model - Wikipedia</a>,<a href="https://learn.co/tracks/web-development-immersive-2-0-module-four/react/what-is-react/virtual-do">Virtual DOM - Learn.co</a>,<a href="https://reactkungfu.com/2015/10/the-difference-between-virtual-dom-and-dom/">Difference between the Virtual DOM and the Real DOM</a>,<a href="https://objectpartners.com/2015/11/19/comparing-react-js-performance-vs-native-dom/">"Comparing React.js Performance vs. native(real) DOM"</a>,<a href="https://www.w3.org/TR/WD-DOM/introduction.html">W3C "What is the Document Object Model?"</a></p>