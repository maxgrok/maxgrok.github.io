---
title: "Using Postman to Make Github API POST Request"
date: "2018-04-09T12:10:13.121Z"
layout: post
draft: false
path: "/posts/thirtieth-post/"
category: "Flatiron School"
tags:
  - "Flatiron School"
  - "Immersive"
  - "Coding School"
description: "This is a post about how to use Postman to make a POST Github API request."
---
During this post, we will cover how to submit a POST request through Postman to the Github API in order to submit a new issue on a Github repo. <br>

<img src="/postman.png" alt="PostmanLogo" /> <br>
First, download Postman <a href="https://www.getpostman.com/">here</a> and open it. <br>

Second, select request from menu and then name your request anything your heart desires and save it in a folder. <br>
<img src="/selectrequest.png" alt="SelectRequest"> <br>
<img src="/nameyourrequest.png" alt="NameYourRequest" /><br>

<img src="/POSTrequest.png" alt="PostmanRequestSelect" /><br>

Third, select "POST" from the menu bar.  <br>

Fourth, select "Headers" from the menu underneath. <br>
Fifth, enter in "token ENTERYOURCODEHERE" in the Value container. <br>
<img src="/tokenauth.png" alt="TokenAuthorization" /><br>

Sixth, select "Raw" from Body menu bar. <br>
Seventh, enter in your issue as a hash. <br>
<img src="/yourissuehash.png" alt="yourIssueHash" /><br>

Lastly, get your response data and check Github to see if the Issue was posted!
If it was, then<em> your POST request was a success! Congratulations!</em> <br>

Below is the example, data for a request that I made to the Github API to post an issue on my blog, which can be viewed <a href="https://www.github.com/maxgrok/maxgrok.github.io/issues">Maxgrok Github Issues</a>
<hr>
    {
    "url": "https://api.github.com/repos/maxgrok/maxgrok.github.io/issues/3",
    "repository_url": "https://api.github.com/repos/maxgrok/maxgrok.github.io",
    "labels_url": "https://api.github.com/repos/maxgrok/maxgrok.github.io/issues/3/labels{/name}",
    "comments_url": "https://api.github.com/repos/maxgrok/maxgrok.github.io/issues/3/comments",
    "events_url": "https://api.github.com/repos/maxgrok/maxgrok.github.io/issues/3/events",
    "html_url": "https://github.com/maxgrok/maxgrok.github.io/issues/3",
    "id": 312596781,
    "number": 3,
    "title": "Issue Test",
    "user": {
        "login": "maxgrok",
        "id": 16481962,
        "avatar_url": "https://avatars2.githubusercontent.com/u/16481962?v=4",
        "gravatar_id": "",
        "url": "https://api.github.com/users/maxgrok",
        "html_url": "https://github.com/maxgrok",
        "followers_url": "https://api.github.com/users/maxgrok/followers",
        "following_url": "https://api.github.com/users/maxgrok/following{/other_user}",
        "gists_url": "https://api.github.com/users/maxgrok/gists{/gist_id}",
        "starred_url": "https://api.github.com/users/maxgrok/starred{/owner}{/repo}",
        "subscriptions_url": "https://api.github.com/users/maxgrok/subscriptions",
        "organizations_url": "https://api.github.com/users/maxgrok/orgs",
        "repos_url": "https://api.github.com/users/maxgrok/repos",
        "events_url": "https://api.github.com/users/maxgrok/events{/privacy}",
        "received_events_url": "https://api.github.com/users/maxgrok/received_events",
        "type": "User",
        "site_admin": false
    },
    "labels": [],
    "state": "open",
    "locked": false,
    "assignee": null,
    "assignees": [],
    "milestone": null,
    "comments": 0,
    "created_at": "2018-04-09T16:20:31Z",
    "updated_at": "2018-04-09T16:20:31Z",
    "closed_at": null,
    "author_association": "OWNER",
    "body": "This is an issue!",
    "closed_by": null
}
