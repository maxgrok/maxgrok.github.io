---
title: "Build a Real Time Chat App: JS/Express/Socket.IO"
date: "2018-06-13T13:00:13.121Z"
layout: post
draft: false
path: "/posts/forty-eighth-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about how to build a real time chat app with JavaScript, Socket.IO, and Express."
---
<h2>Why are you building real time chat apps?</h2>

I'm fascinated by the implementations of websockets in different languages and full-duplex communications. I'm building multiple chat apps to explore and sharing my knowledge as I go. 

The real time chat app that we are going to build with Socket.IO is the quickest implementation of a real time chat app that I have found so far. 

<strong>All you need to know how to do is copy and paste to build this.</strong>  

<h2>What's Covered in this Post:</h2>
<p>What is Socket.IO?</p>
<p>How to Build a Real Time Chat App</p>
<p>How to Deploy Your App with Heroku</p>
<hr>

<h2>What is Socket.IO?</h2>

Socket.IO is a simple JavaScript implementation of websockets to be used in full stack JavaScript web applications. It allows for full-duplex bidirectional server-client communications, just like ActionCable and Phoenix. 

See other posts about Real Time Chat Apps: <a href="http://maxgrok.netlify.com/posts/forty-first-post/">ActionCable</a> implementation & <a href="http://maxgrok.netlify.com/posts/forty-fifth-post/">Elixir/Phoenix</a> implementation. 

<h2>How to Build a Real Time Chat App with Socket.IO</h2>

Pre-requisites: installation of <a href="https://nodejs.org/en/">Node</a>, <a href="https://www.npmjs.com/">npm</a>, git, Macbook, Sublime Text/InsertYourFavoriteTextEditorHere, Internet, basic knowledge of the Terminal

Please go through installating Node before following along with this tutorial. 

<h3>1) Create a directory called anything you want. This will be where your chat app is stored. Let's call ours `chat-app`.</h3>

<h3>1a) Run `git init`, `git add .`, and `git commit -m "first message"</h3>
<h3>2) Create a `package.json` file</h3>

Copy and paste the following into your `chat-app` directory `package.json` file.

```javascript
{
  "name": "socket-chat-example",
  "version": "0.0.1",
  "description": "my first socket.io app",
  "dependencies": {}
}
```

Congratulations! You just made your first `package.json` file. 

<h3>2) Run `npm install --save` in your Terminal</h3>

This step installs all the files necessary for a node app to run. 

<h3>3) Run `npm install --save express@4.15.2`.</h3>

This installs Express for your app. For more on Express, read the <a href="https://expressjs.com/">Express docs here</a>. 

<h3>4) Make an index.js file by running `touch index.js` in your Terminal within your `chat-app` directory</h3>

<h3>5) Copy and paste the following into `index.js`</h3>

```javascript

var app = require('express')();
var http = require('http').Server(app);

app.get('/', function(req, res){
  res.send('<h1>Hello world</h1>');
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});
```

"This translates into the following:

Express initializes app to be a function handler that you can supply to an HTTP server (as seen in line 2).
We define a route handler / that gets called when we hit our website home.
We make the http server listen on port 3000."

<a href="https://socket.io/get-started/chat/">Socket.IO Chat Docs</a>

<h3>6) Run `node index.js` in your Terminal</h3>

This starts the node server to render your javascript app. You should see a message that says `listening on *:3000` in your Terminal. 

<h3>7) Go to your browser at the address `http://localhost:3000`</h3>

You should see "Hello world". This means that your app is running successfully locally!

If you have any errors, please review the steps and make sure you are following them in order and typing them exactly into the Terminal and `index.js` file. 

<h3>8) Edit your `index.js` file</h3>

Copy and paste the following: 

```javascript

app.get('/', function(req, res){
res.sendFile(__dirname + '/index.html');
});
```

This will replace this code in your `index.js` file: 

```javascript

app.get('/', function(req, res){
  res.send('<h1>Hello world</h1>');
});
``` 

Now, your `index.js` file should look like this: 

```JavaScript
var app = require('express')();
var http = require('http').Server(app);

app.get('/', function(req, res){
res.sendFile(__dirname + '/index.html');
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});
    
```

<h3>9) Create an `index.html` file by running `touch index.html` in your Terminal within the app root directory</h3>

<h3>10) Copy and paste the following into your `index.html` file</h3>

```html
<!doctype html>
<html>
  <head>
    <title>Socket.IO chat</title>
    <style>
      * { margin: 0; padding: 0; box-sizing: border-box; }
      body { font: 13px Helvetica, Arial; }
      form { background: #000; padding: 3px; position: fixed; bottom: 0; width: 100%; }
      form input { border: 0; padding: 10px; width: 90%; margin-right: .5%; }
      form button { width: 9%; background: rgb(130, 224, 255); border: none; padding: 10px; }
      #messages { list-style-type: none; margin: 0; padding: 0; }
      #messages li { padding: 5px 10px; }
      #messages li:nth-child(odd) { background: #eee; }
    </style>
  </head>
  <body>
    <ul id="messages"></ul>
    <form action="">
      <input id="m" autocomplete="off" /><button>Send</button>
    </form>
  </body>
</html>
```

<h3>11) Run `node index.js` in your Terminal</h3>

<h3>12) Visit your browser at `http://localhost:3000/'</h3>

You should see a chat box with a send button in your view now! 

<h3>13) Install Socket.IO</h3>

Run `npm install --save socket.io` in your Terminal

This will 'install the module and add the dependency to your `package.json`'.

<h3>14) Edit your `index.js` to add Socket.IO</h3>

Replace all the code in your `index.js` file with the following: 

```javascript
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket){
  console.log('a user connected');
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});
```

This 'initialize(s) a new instance of socket.io by passing the http (the HTTP server) object. Then I listen on the connection event for incoming sockets, and I log it to the console.' <a href="https://socket.io/get-started/chat/">Socket.IO Chat Docs</a>

<h3>15) Copy and paste the following code right before the end of your `</body>` tag in your `index.html` file</h3>

```html
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io();
</script>
```

<h3>16) Run `node index.js` in your Terminal to test out the socket</h3>

You should see (in your Terminal) 'a user connected'. If you refresh the page multiple times, you should see that 'a user connected' text each time you refresh. 

<h3>17) Copy and paste the following into your `index.html`</h3>

```html
<script src="/socket.io/socket.io.js"></script>
<script src="https://code.jquery.com/jquery-1.11.1.js"></script>
<script>
  $(function () {
    var socket = io();
    $('form').submit(function(){
      socket.emit('chat message', $('#m').val());
      $('#m').val('');
      return false;
    });
  });
</script>
```

This should replace the previous code 

```html
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io();
</script>
```

So, now your `index.html` should look like this: 

```html
<!doctype html>
<html>
  <head>
    <title>Socket.IO chat</title>
    <style>
      * { margin: 0; padding: 0; box-sizing: border-box; }
      body { font: 13px Helvetica, Arial; }
      form { background: #000; padding: 3px; position: fixed; bottom: 0; width: 100%; }
      form input { border: 0; padding: 10px; width: 90%; margin-right: .5%; }
      form button { width: 9%; background: rgb(130, 224, 255); border: none; padding: 10px; }
      #messages { list-style-type: none; margin: 0; padding: 0; }
      #messages li { padding: 5px 10px; }
      #messages li:nth-child(odd) { background: #eee; }
    </style>
  </head>
  <body>
    <ul id="messages"></ul>
    <form action="">
      <input id="m" autocomplete="off" /><button>Send</button>
    </form>
    <script src="/socket.io/socket.io.js"></script>
    <script src="https://code.jquery.com/jquery-1.11.1.js"></script>
    <script>
      $(function () {
        var socket = io();
        $('form').submit(function(){
          socket.emit('chat message', $('#m').val());
          $('#m').val('');
          return false;
        });
      });
    </script>
  </body>
</html>
```

<h3>18) Copy and paste the following into your `index.js` file</h3>

```javascript
io.on('connection', function(socket){
  socket.on('chat message', function(msg){
    console.log('message: ' + msg);
  });
});
```

Now, your `index.js` file should look like this: 

```javascript
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket){
  socket.on('chat message', function(msg){
    console.log('message: ' + msg);
  });
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});
    
```

<h3>19) Run `node index.js` in your Terminal & Visit `http://localhost:3000/`</h3>

If you type into your text box on the screen, then click 'Send'. Check your terminal. You should see something like 

```markdown
message: asdf
```

Where your message is 'asdf'. Type in whatever you want and it will show up in the Terminal! Give it a try!

<h3>20) Copy and paste the following into `index.js`</h3>

```javascript
io.on('connection', function(socket){
  socket.on('chat message', function(msg){
    io.emit('chat message', msg);
  });
});
```

So, your `index.js` file should look like this: 

```javascript
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket){
  socket.on('chat message', function(msg){
    io.emit('chat message', msg);
  });
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});
    
```

<h3>21) Copy and paste the following into `index.html`</h3>

```html
<script>
  $(function () {
    var socket = io();
    $('form').submit(function(){
      socket.emit('chat message', $('#m').val());
      $('#m').val('');
      return false;
    });
    socket.on('chat message', function(msg){
      $('#messages').append($('<li>').text(msg));
    });
  });
</script>
```

So your `index.html` page should look like this now: 
```html
<!doctype html>
<html>
  <head>
    <title>Socket.IO chat</title>
    <style>
      * { margin: 0; padding: 0; box-sizing: border-box; }
      body { font: 13px Helvetica, Arial; }
      form { background: #000; padding: 3px; position: fixed; bottom: 0; width: 100%; }
      form input { border: 0; padding: 10px; width: 90%; margin-right: .5%; }
      form button { width: 9%; background: rgb(130, 224, 255); border: none; padding: 10px; }
      #messages { list-style-type: none; margin: 0; padding: 0; }
      #messages li { padding: 5px 10px; }
      #messages li:nth-child(odd) { background: #eee; }
    </style>
  </head>
  <body>
    <ul id="messages"></ul>
    <form action="">
      <input id="m" autocomplete="off" /><button>Send</button>
    </form>
    <script src="/socket.io/socket.io.js"></script>
    <script src="https://code.jquery.com/jquery-1.11.1.js"></script>
    <script>
  $(function () {
    var socket = io();
    $('form').submit(function(){
      socket.emit('chat message', $('#m').val());
      $('#m').val('');
      return false;
    });
    socket.on('chat message', function(msg){
      $('#messages').append($('<li>').text(msg));
    });
  });
</script>
  </body>
</html>
```
<h3>22) Run `git add .` and `git commit -m "finished real time chat app` in your Terminal</h3>

<h2>Congratulations!</h2>
<h2>You just built a Real Time Chat App with Socket.IO and Express in JavaScript that runs locally!</h2>

<p>Find the code on <a href="http://www.github.com/maxgrok/node-real-time-chat-app.git">GitHub</a></p>

<h2>Deploying Your Real Time App to Heroku</h2>

Pre-requisites: install Heroku CLI + same pre-reqs as before

<h3>1) Run `heroku create` in your Terminal inside your `chat-app` directory</h3>

You should see something like 
```markdown
Creating app... done, ⬢ damp-everglades-14640
https://{your-app-name-here}.herokuapp.com/ | https://git.heroku.com/{your-app-name-here}.git
```

Run `git remote -v` to check that you have a remote Heroku branch. 

<h3>2) Edit app to set the port dynamically in your `index.js` file

    Copy and paste: 

```javascript
http.listen(process.env.PORT || 3000, function(){
  console.log("Express server listening on port %d in %s mode", this.address().port, app.settings.env);
});
```

(Adapted from <a href="https://stackoverflow.com/questions/14322989/first-heroku-deploy-failed-error-code-h10">StackOverflow - Deploy Error H10 for Heroku</a>)

<h3>3) Edit the `package.json` file to include a "start" script</h3>

```javascript
"scripts": {
    "start": "node your-script.js"
}
```

<h3>4) Run `git add .` && `git commit -m "finished deployment config"` and `git push heroku master` to deploy</h3>

<h2>Congratulations! You're done! You've deployed!</h2>

Check out your app at your heroku location. ( http://{your-app-name}.herokuapp.com/) 

<h2>Real Time Chat App</h2>

<iframe width="640" height="564" src="https://player.vimeo.com/video/274922723" frameborder="0" allowFullScreen mozallowfullscreen webkitAllowFullScreen></iframe>

If you have any errors, try to debug them by running `heroku logs` in your Terminal or seeing any errors in your `console.log` or `debugger` in JavaScript or running it locally with `npm start` to see any errors. If you need to, feel free to reach out to me personally for help, <a href="http://www.twitter.com/maxxgrok">@maxxgrok</a>.

<h2>Thanks for reading this post!</h2>


