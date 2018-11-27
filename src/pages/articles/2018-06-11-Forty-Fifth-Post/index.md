---
title: "Build A Real Time Chat App: Elixir/Phoenix"
date: "2018-06-11T19:10:13.121Z"
layout: post
draft: false
path: "/posts/forty-fifth-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about how to build a real-time chat app with Elixir and Phoenix and Websockets."
---

In this post, unlike the last post, we will be walking through how to build a real-time chat app with Elixir and Phoenix. 

First, let's cover what Elixir is and what Phoenix is. 

<h3>What are Elixir and Phoenix?</h3>

Here's what their respective docs say: 

<strong>Elixir</strong> is a "dynamic, functional language designed for scalable and maintainable applications" (<a href="https://elixir-lang.org/">Elixir-lang.org</a>).

<strong>Phoenix</strong> is a "productive web framework that does not compromise speed and maintainability" (<a href="http://phoenixframework.org/">Phoenixframework.org</a>)

Let's get started building our application. 

<h3>Step 1: Install Elixir and Phoenix</h3>

Go into your CLI and type: 

```markdown 
brew install elixir
```

If you do not have Homebrew installed, follow this <a href="https://brew.sh/">Homebrew</a> tutorial. Requirements: MacOS.

After running the Elixir install, run this: 

`mix archive.install https://github.com/phoenixframework/archives/raw/master/phx_new.ez`

<h3>Step 2: Run a basic Phoenix app</h3>

In your CLI, run `mix phx.new hello`

You should see the following: 

```markdown
* creating hello/config/config.exs
* creating hello/config/dev.exs
* creating hello/config/prod.exs
* creating hello/config/prod.secret.exs
* creating hello/config/test.exs
* creating hello/lib/hello/application.ex
* creating hello/lib/hello.ex
* creating hello/lib/hello_web/channels/user_socket.ex
* creating hello/lib/hello_web/views/error_helpers.ex
* creating hello/lib/hello_web/views/error_view.ex
* creating hello/lib/hello_web/endpoint.ex
* creating hello/lib/hello_web/router.ex
* creating hello/lib/hello_web.ex
* creating hello/mix.exs
* creating hello/README.md
* creating hello/test/support/channel_case.ex
* creating hello/test/support/conn_case.ex
* creating hello/test/test_helper.exs
* creating hello/test/hello_web/views/error_view_test.exs
* creating hello/lib/hello_web/gettext.ex
* creating hello/priv/gettext/en/LC_MESSAGES/errors.po
* creating hello/priv/gettext/errors.pot
* creating hello/lib/hello/repo.ex
* creating hello/priv/repo/seeds.exs
* creating hello/test/support/data_case.ex
* creating hello/lib/hello_web/controllers/page_controller.ex
* creating hello/lib/hello_web/templates/layout/app.html.eex
* creating hello/lib/hello_web/templates/page/index.html.eex
* creating hello/lib/hello_web/views/layout_view.ex
* creating hello/lib/hello_web/views/page_view.ex
* creating hello/test/hello_web/controllers/page_controller_test.exs
* creating hello/test/hello_web/views/layout_view_test.exs
* creating hello/test/hello_web/views/page_view_test.exs
* creating hello/.gitignore
* creating hello/assets/brunch-config.js
* creating hello/assets/css/app.css
* creating hello/assets/css/phoenix.css
* creating hello/assets/js/app.js
* creating hello/assets/js/socket.js
* creating hello/assets/package.json
* creating hello/assets/static/robots.txt
* creating hello/assets/static/images/phoenix.png
* creating hello/assets/static/favicon.ico

Fetch and install dependencies? [Yn] y
* running mix deps.get
* running mix deps.compile
* running cd assets && npm install && node node_modules/brunch/bin/brunch build

We are almost there! The following steps are missing:

    $ cd hello
    $ cd assets && npm install && node node_modules/brunch/bin/brunch build

Then configure your database in config/dev.exs and run:

    $ mix ecto.create

Start your Phoenix app with:

    $ mix phx.server

You can also run your app inside IEx (Interactive Elixir) as:

    $ iex -S mix phx.server

```

Now, run `cd hello`.

Then `mix ecto.create` which creates your database. 

Finally, restart the Phoenix server with `mix phx.server`.

By default Phoenix runs on port 4000, so let's go to `localhost:4000` and see our app! 

You should see this: 
`[info] Running HelloWeb.Endpoint with Cowboy using http://0.0.0.0:4000` in your CLI, then go to your browser and type in `localhost:4000`

You should see this screen: 

<blockquote class="imgur-embed-pub" lang="en" data-id="a/Od280Ov"><a href="//imgur.com/Od280Ov"></a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

Which means that your Phoenix app is setup properly! 

<h3>Congratulations! Your basic Phoenix app is running!</h3>

<h2>Building the Chat App</h2>

<h3>Step 1) Creating the View</h3>

Go to `hello/lib/hello_web/templates/page/index.html.eex` file. 
You should see the following: 

```elixir
<div class="jumbotron">
  <h2><%= gettext "Welcome to %{name}!", name: "Phoenix" %></h2>
  <p class="lead">A productive web framework that<br />does not compromise speed and maintainability.</p>
</div>

<div class="row marketing">
  <div class="col-lg-6">
    <h4>Resources</h4>
    <ul>
      <li>
        <a href="http://phoenixframework.org/docs/overview">Guides</a>
      </li>
      <li>
        <a href="https://hexdocs.pm/phoenix">Docs</a>
      </li>
      <li>
        <a href="https://github.com/phoenixframework/phoenix">Source</a>
      </li>
    </ul>
  </div>

  <div class="col-lg-6">
    <h4>Help</h4>
    <ul>
      <li>
        <a href="http://groups.google.com/group/phoenix-talk">Mailing list</a>
      </li>
      <li>
        <a href="http://webchat.freenode.net/?channels=elixir-lang">#elixir-lang on freenode IRC</a>
      </li>
      <li>
        <a href="https://twitter.com/elixirphoenix">@elixirphoenix</a>
      </li>
    </ul>
  </div>
</div>

```

Delete all of it. Copy and paste the following into the same file:  

```elixir
<div id='message-list' class='row'>
</div>

<div class='row form-group'>
  <div class='col-md-3'>
    <input type='text' id='name' class='form-control' placeholder='Name' />
  </div>
  <div class='col-md-9'>
    <input type='text' id='message' class='form-control' placeholder='Message' />
  </div>
</div>
```

<h3>Step 2) Style the View</h3>

Open `hello/assets/css/app.css` and copy and paste the following into this file: 

```css
#message-list {
  border: 1px solid #777;
  height: 400px;
  padding: 10px;
  overflow: scroll;
  margin-bottom: 50px;
}
```

Now, if you run `mix phx.server`, you should see the following: 

<blockquote class="imgur-embed-pub" lang="en" data-id="a/ocl4zSB"><a href="//imgur.com/ocl4zSB"></a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

<h3>Step 3) Setting up a Channel </h3>

Go to file `hello/lib/hello_web/channels/user_socket.ex` and add the following line: 

`channel "lobby", HelloWeb.LobbyChannel`

Then add a new file called `lobby_channel.ex` to the same directory. 

Insert the following inside that file: 
```elixir
defmodule Chatroom.LobbyChannel do
  use Phoenix.Channel

  def join("lobby", _payload, socket) do
    {:ok, socket}
  end

  def handle_in("new_message", payload, socket) do
    broadcast! socket, "new_message", payload
    {:noreply, socket}
  end
 end
```

What does the join method do here? 

It returns {:ok, socket} to allow all connections to the channel. 

The `handle_in` method runs every time a message is sent through the socket and sends that message to all the other open sockets in connection. (paraphrased from <a href="https://sheharyar.me/blog/simple-chat-phoenix-elixir/">Build a Chat App with Phoenix</a>)

<h3>Step 4) Handle connections on the Front-End/Client-side</h3>

Go to file `hello/lib/hello_web/templates/layouts/app.html.eex`. 

Add the following to the bottom of your file nearby the other script tag. 

```elixir
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.2.4/jquery.min.js"></script>
<script src="<%= static_path(@conn, "/js/app.js") %>"></script>
```

This adds the jquery library to your application as well as the app.js file that automatically gets generated as part of your Phoenix application. 

Go into `hello/assets/js/app.js` and uncomment the following line: 

```elixir
//import socket from "./socket"
```

When you uncomment it, the line should look like this: 

```elixir
import socket from "./socket"
```

Next, go to `hello/assets/js/socket.js`, and see a file that looks like this: 

```elixir
// NOTE: The contents of this file will only be executed if
// you uncomment its entry in "assets/js/app.js".

// To use Phoenix channels, the first step is to import Socket
// and connect at the socket path in "lib/web/endpoint.ex":
import {Socket} from "phoenix"

let socket = new Socket("/socket", {params: {token: window.userToken}})

// When you connect, you'll often need to authenticate the client.
// For example, imagine you have an authentication plug, `MyAuth`,
// which authenticates the session and assigns a `:current_user`.
// If the current user exists you can assign the user's token in
// the connection for use in the layout.
//
// In your "lib/web/router.ex":
//
//     pipeline :browser do
//       ...
//       plug MyAuth
//       plug :put_user_token
//     end
//
//     defp put_user_token(conn, _) do
//       if current_user = conn.assigns[:current_user] do
//         token = Phoenix.Token.sign(conn, "user socket", current_user.id)
//         assign(conn, :user_token, token)
//       else
//         conn
//       end
//     end
//
// Now you need to pass this token to JavaScript. You can do so
// inside a script tag in "lib/web/templates/layout/app.html.eex":
//
//     <script>window.userToken = "<%= assigns[:user_token] %>";</script>
//
// You will need to verify the user token in the "connect/2" function
// in "lib/web/channels/user_socket.ex":
//
//     def connect(%{"token" => token}, socket) do
//       # max_age: 1209600 is equivalent to two weeks in seconds
//       case Phoenix.Token.verify(socket, "user socket", token, max_age: 1209600) do
//         {:ok, user_id} ->
//           {:ok, assign(socket, :user, user_id)}
//         {:error, reason} ->
//           :error
//       end
//     end
//
// Finally, pass the token on connect as below. Or remove it
// from connect if you don't care about authentication.
// 


socket.connect()

// Now that you are connected, you can join channels with a topic:
let channel = socket.channel("topic:subtopic", {})
channel.join()
  .receive("ok", resp => { console.log("Joined successfully", resp) })
  .receive("error", resp => { console.log("Unable to join", resp) })

export default socket
```

Copy and paste this into that file: 

```elixir
//...
let channel = socket.channel("lobby", {});
let list    = $('#message-list');
let message = $('#message');
let name    = $('#name');

message.on('keypress', event => {
  if (event.keyCode == 13) {
    channel.push('new_message', { name: name.val(), message: message.val() });
    message.val('');
  }
});

channel.on('new_message', payload => {
  list.append(`<b>${payload.name || 'Anonymous'}:</b> ${payload.message}<br>`);
  list.prop({scrollTop: list.prop("scrollHeight")});
});

channel.join()
  .receive("ok", resp => { console.log("Joined successfully", resp) })
  .receive("error", resp => { console.log("Unable to join", resp) })

// ...
```

In the code above, we add an event listener that returns the message on click of keyCode 13 which is equal to the 'Enter' key. It also clears the text field after the message has been `push`ed. 

<h2>Step 5) Deploy it with Heroku!</h2>

1st install the <a href="">Heroku CLI</a>. 
click <a href="https://www."></a>
You will need to specific buildpacks. 2 buildpacks. The elixir buildpack and the phoenix buildpack. 

After you have installed the Heroku CLI, run `heroku create` in your application repo. 

Run the Elixir buildpack here in your CLI: 
`heroku buildpacks:set https://github.com/HashNuke/heroku-buildpack-elixir`

Run Phoenix buildpack here in your CLI: 
`heroku buildpacks:add https://github.com/gjaldon/heroku-buildpack-phoenix-static`

You will also need to comment out the line in your `.gitignore` that specifies `config/*.secret.exs` files and replace those variables with environment variables like so: 

```elixir
#config/prod.secrets.exs
use Mix.Config

# In this file, we keep production configuration that
# you'll likely want to automate and keep away from
# your version control system.
#
# You should document the content of this
# file or create a script for recreating it, since it's
# kept out of version control and might be hard to recover
# or recreate for your teammates (or yourself later on).
config :hello, HelloWeb.Endpoint,
  secret_key_base: System.get_env("secret_key_base")

# Configure your database
config :hello, HelloWeb.Repo,
  adapter: Ecto.Adapters.Postgres,
  username: System.get_env("DATABASE_USERNAME"),
  password: System.get_env("DATABASE_PASSWORD"),
  database: "hello_phoenix_heroku_prod",
  size: 20 
```

Add a Gemfile in your app directory with the following code: 

```css
source 'https://rubygems.org/'
ruby '2.3.1'
gem 'sass'
```
Run `bundle` in your CLI to install the gem. 

Make another file called a `phoenix_static_buildpack.config` in the `hello` directory with the following settings: 

```markdown
# Clean out cache contents from previous deploys
clean_cache=false

# We can change the filename for the compile script with this option
compile="compile"

# We can set the version of Node to use for the app here
node_version=10.4.0

# We can set the version of NPM to use for the app here
npm_version=6.1.0

# We can set the path to phoenix app. E.g. apps/phoenix_app when in umbrella.
phoenix_relative_path=.

# Remove node and node_modules directory to keep slug size down if it is not needed.
remove_node=false

# We can change path that npm dependencies are in relation to phoenix app. E.g. assets for phoenix 1.3 support.
assets_path=.

# We can change phoenix mix namespace tasks. E.g. phx for phoenix 1.3 support.
phoenix_ex=phoenix
```

Run `git add .` and then `git commit -m "adding production requirements"` then run `git push heroku master` and wait. 

Run `heroku ps:scale web=1` to make sure your web process is running. 

If you do not have any errors, check your site and review <a href="https://hexdocs.pm/phoenix/heroku.html">Heroku Phoenix Deployment Docs</a>! 

If you have errors, use StackOverflow to find answers or the #phoenix in the @elixir Slack. Otherwise, ...

<h2>Congratulations! You've Built a Real Time Chat App in Elixir with Phoenix and Deployed It to Heroku!</h2>

<h2>Production Demo</h2>

<iframe style="margin: 0 auto;" src="https://player.vimeo.com/video/274696078" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
<p><a href="https://vimeo.com/274696078">Phoenix/Elixir Real Time Chat App Demo</a> from <a href="https://vimeo.com/user86152978">Max Goodman</a> on <a href="https://vimeo.com">Vimeo</a>.</p>


<h3>Acknowledgements and References</h3>

<a href="https://hexdocs.pm/phoenix/heroku.html">Heroku Phoenix Deployment Docs</a>

<a href="https://www.tuicool.com/articles/QbAVveY">Deploying to Heroku from Phoenix</a>

<a href="https://github.com/phoenixframework/phoenix/issues/1410">Phoenix Issues 1410</a>

<a href="https://github.com/gjaldon/heroku-buildpack-phoenix-static">Heroku Buildpack Instructions</a>

<a href="https://www.elixir-lang.org">Elixir-lang.org</a> - For their definition of Elixir.

<a href="https://hexdocs.pm/phoenix/up_and_running.html">Phoenix Framwork</a> - For their introduction on how to build a basic Phoenix application from scratch. 

<a href="https://sheharyar.me/blog/talk-introduction-to-elixir/">Sheharyar Naseer </a> - For their introduction to Elixir talk, which guided me through the basics of Elixir. 

<a href="https://sheharyar.me/blog/simple-chat-phoenix-elixir/">Sheharyar Naseer</a> - For their tutorial on how to build a simple chat app with Elixir and Phoenix

<a href="`https://work.stevegrossi.com/2016/07/11/building-a-chat-app-with-elixir-and-phoenix-presence/">Steve Grossi </a> - For their tutorial on building a chat app with Elixir and Phoenix. 


