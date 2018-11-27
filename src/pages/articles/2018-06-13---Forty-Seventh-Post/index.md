---
title: "Build A Real Time Chat App: React/GraphQL"
date: "2018-06-18T10:40:13.121Z"
layout: post
draft: false
path: "/posts/forty-seventh-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about how to build a real time chat app with React and GraphQL."
---

In this tutorial, I'm going to run through how to build a real time chat app using React and GraphQL.  

Here is a demo of the final product: <a href="http://whispering-caverns-55862.herokuapp.com/">whispering-caverns-55862.herokuapp.com/</a>

No time to waste! Let's get started. 

1) Open to your terminal. 

2) Run `create-react-app graphql-chat`. This will scaffold a new react project for you. 

3) Run `cd graphql-chat` in your terminal to enter the project folder we just created. 

4) Update your dependencies in `packages.json` within your project folder to include the following under `dependencies`: 

```javascript
"apollo-client-preset": "^1.0.6",
  "apollo-link-ws": "^1.0.4",
  "graphql": "^0.12.3",
  "graphql-tag": "^2.6.1",
  "react": "^16.2.0",
  "react-apollo": "^2.0.4",
  "react-dom": "^16.2.0",
  "react-scripts": "1.0.17",
  "subscriptions-transport-ws": "^0.9.4"
```

5) Now, run `npm install`. 

6) Add your styles to the `public/index.html` file in the `head` section: 

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/7.0.0/normalize.min.css" />
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/skeleton/2.0.4/skeleton.min.css" />
```

7) Install graphcool. `npm install -g graphcool-framework`

8) Start a new graphcool server. `graphcool-framework init server`

9) Go to the `types.graphql` file in the `server` folder. 

10) Replace all the content with the following: 

```javascript
type Chat @model {
  id: ID! @isUnique
  from: String!
  content: String!
  createdAt: DateTime!
}
```

11) `cd server` and run `graphcool deploy` (Note: please signup for Graph.cool account for this to work)

12) open up `console.graph.cool` to see your `schema`. 

13) Go into your console and check out the GraphQL playground Endpoint API address. Copy and paste this into your browser to go to the GraphQL playground for your database! OR run `graphcool-framework playground` in your console to open up your GraphQL playground. 

14) Run the following two operations in your graphQL playground to test our schema. 

Make sure to run FETCH_CHATS first, then the mutation. 


```javascript
  query FETCH_CHATS{
      allChats{
        from,
        content
      }
    }

    mutation CREATE_CHAT {
      createChat(content: "test", from: "test") {
        content,
        from
      }
    }
```

You should see something like this on the right hand side of your graphQL playground: 

```javascript
{
  "data": {
    "createChat": {
      "content": "test",
      "from": "test"
    }
  }
}
```

15) Update your `src/hello.js` file to include all the dependencies.

```javascript
 import { ApolloProvider } from 'react-apollo';
    import { ApolloClient } from 'apollo-client';
    import { HttpLink } from 'apollo-link-http';
    import { InMemoryCache } from 'apollo-cache-inmemory';
    import { ApolloLink, split } from 'apollo-client-preset'
    import { WebSocketLink } from 'apollo-link-ws'
    import { getMainDefinition } from 'apollo-utilities'
```

16) Right after the imports, place the following to configure the websockets link. You can do this by copy and pasting the following into the `src/hello.js` file. 

```javascript
const wsLink = new WebSocketLink({

  uri: '[Subscriptions API URI]',
  options: {
    reconnect: true
  }
})
```

Please make sure to substitute your own Subscriptions API http address for the placeholder `Subscriptions API URI`.

17) Add the following to configure our HTTP connection. Make sure to add it right after the websockets configuration. 

`const httpLink = new HttpLink({ uri: '[SIMPLE API URI]' })`

Please make sure to include your actual SIMPLE API URI (the web address for the Simple API included in your console). 

18) Create your Apollo client by copy and pasting the following after the previous code in `src/hello.js`.

```javascript
const client = new ApolloClient({

  link,
  cache: new InMemoryCache()
})
```

19) Reorganize your file structure. All your `.js` files should be under `src/`.

20) run `npm start` from your Terminal, which will open the browser. You should see a popup with a message requesting your name. Enter a name, then see the test data that was initially inputted by mutation in the graphQL database! 

21) In our `App.js` file, insert the following for the Chat mutation. 

```javascript
    import { graphql, compose } from 'react-apollo';
    // App component ...

    const CREATE_CHAT_MUTATION = gql`
      mutation CreateChatMutation($content: String!, $from: String!) {
        createChat(content: $content, from: $from) {
          id
          createdAt
          from
          content
        }
      }
    `;

    export default compose(
      graphql(ALL_CHATS_QUERY, { name: 'allChatsQuery' }),
      graphql(CREATE_CHAT_MUTATION, { name: 'createChatMutation' })
    )(App);
```

22) Add the following to the `render()` method within `App.js`. 

```javascript
 const allChats = this.props.allChatsQuery.allChats || [];
       return (
          <div className="">
            <div className="container">
              <h2>Chats</h2>
              {allChats.map(message => (
                <Chatbox key={message.id} message={message} />
              ))}

              {/* Message content input */}
              <input
                value={this.state.content}
                onChange={e => this.setState({ content: e.target.value })}
                type="text"
                placeholder="Start typing"
                onKeyPress={this._createChat}
              />
            </div>
          </div>
           );
       }
    }```

Now when you run `npm start`, you will see a chat box that says "Start typing" and be able to enter in new messages, however, you will only be able to see the new messages on reload! 

This is a problem. Let's fix it by <strong>setting up real time subscriptions</strong>. 

23) Add the following method to your `App` class to setup the subscription. 

```javascript
_subscribeToNewChats = () => {
      this.props.allChatsQuery.subscribeToMore({
          document: gql`
            subscription {
              Chat(filter: { mutation_in: [CREATED] }) {
                node {
                  id
                  from
                  content
                  createdAt
                }
              }
            }
          `,
          updateQuery: (previous, { subscriptionData }) => {
            const newChatLinks = [
              ...previous.allChats,
              subscriptionData.data.Chat.node
            ];
            const result = {
              ...previous,
              allChats: newChatLinks
            };
            return result;
          }
        });
      };
```

24) Add the following to the `componentsDidMount` method within the `App` class. 

`this._subscribeToNewChats();`

This starts the subscription. 

25) Run `npm start`. You should see a real time chat app that works!

<h2>Congratulations! You're Done!</h2>

<h1>Further implementation</h1>

Let's deploy this to Heroku! 

1) Run `heroku create` (assuming you have Heroku CLI installed already)
2) Delete the `yarn.lock` file in your root directory. 
3) `git push heroku master` in your CLI
4) Run `heroku open` and it will open your web app! 

<h1>Congratulations! You deployed your chat app to Heroku!</h1>

See a demo of what you'll have created here: 
<a href="http://whispering-caverns-55862.herokuapp.com/">whispering-caverns-55862.herokuapp.com/</a>

Sources: 

<a href="https://scotch.io/tutorials/how-to-build-a-realtime-chat-app-with-react-and-graphql#creating-new-messages">How to Build a Real Time Chat App with React and GraphQL</a>

<a href="https://blog.heroku.com/deploying-react-with-zero-configuration">Deploying with Zero Configuration with React in Heroku</a>