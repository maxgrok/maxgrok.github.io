---
title: "GraphQL: Make Your First Query"
date: "2018-06-15T11:39:13.121Z"
layout: post
draft: false
path: "/posts/fiftieth-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about how to make your first graphQL query, what graphQL is, and why it's important."
---

<h2>What is GraphQL?</h2>

graphQL allows clients to make custom queries to your API instead of building multiple APIs to accomodate different fetches. 

<h2>I'm new here. What are fetches?</h2>

Fetch is a way to CRUD data with an API using JavaScript. 

For example, the following is a fetch `GET` request. <br>
(A `GET` request grabs data from an endpoint)

```javascript
fetch('enterURLEndpointhere'){
    then(function(response) {
    return response.json();
  })
  .then(function(myJson) {
    console.log(myJson);
  });
}
```

This grabs data from the API at the endpoint specified, then `console.log`s the JSON response. It might look like this in your `console.log` once you open the response: 

```javascript
{
  "data": {
    "info": "This is the API response"
  }
}
```

For more information on fetches, visit the <a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch">MDN docs</a>. 

<h2>What's an example use for graphQL?</h2>

I'm so glad you asked! 

If you have a query that you want to do with your API and it is not standard REST, then you may want to implement graphQL. 

Let's say we have a movie API. 

It responds this way to a fetch `GET` request at `localhost:3000/api/v1/movies`:

```javascript
    [
{
id: 1,
title: "Indiana Jones",
summary: "Raiders of the Lost Ark",
year: 1981
},
]
```

(We only have one movie in our API right now.)

Let's say we want to see all the actors in this movie, as well as only see the title and year of the movie. 

You can write a graphQL query to specifically target that information. 

So your response would be something like this: 

```javascript
    [
{
id: 1,
title: "Indiana Jones",
year: 1981,
actors: [
    {
        "name":"Harrison Ford"
    }
]
},
]
```

<h2>Why is this important?</h2>

It's important because you can get more specific information and only that specific information back from your queries, which saves time otherwise used for creating custom queries in the JSON data one would receive from the REST Http API. 

<h2>Make your first GraphQL Query</h2>

```markdown

mkdir graphql-query
cd graphql-query
yarn init -y
mkdir src
touch src/index.js
yarn add graphql-yoga
```

Open up your `index.js` file and copy and paste the following: 

```javascript
const { GraphQLServer } = require('graphql-yoga')

const typeDefs = `
type Query {
  info: String!
}
`

// 2
const resolvers = {
  Query: {
    info: () => `This is the API of my first GraphQL query`
  }
}

// 3
const server = new GraphQLServer({
  typeDefs,
  resolvers,
})
server.start(() => console.log(`Server is running on http://localhost:4000`))
```

Run `node src/index.js` from your Terminal. 
You should see this following message: 

`Server is running on http://localhost:4000`

Visit `localhost:4000` and load your GraphQL playground! 

In the right hand box, type the following for your first query: 

```javascript
query {
  info
}
```

You should see the following on the left side of the GraphQL Playground as a response: 

```javascript
{
    "data":{
        "info":"This is the API of my first graphQL query"
    }
}
```

<h2>Congratulations! You made your first GraphQL query!</h2>
<hr>

<em>Source: <a href="https://www.howtographql.com/graphql-js/">How To GraphQL</a>

