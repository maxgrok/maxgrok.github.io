---
title: "What are structs in Solidity?"
date: "2018-11-24T21:15:13.121Z"
layout: post
draft: false
path: "/posts/sixty-nineth-post/"
category: "Solidity"
tags:
  - "Smart Contracts"
  - "Blockchain"
  - "P2P"
  - "Solidity"
description: "This is a post about what structs in Solidity are."
---

`Struct`s "provide a way of defining new types".

`Struct`s have fields, as well as methods. They are similar to objects, except that objects do not have methods, while `struct`s do. 

Let's look at a very simple struct Code Source:[Solidity Docs][http://solidity.readthedocs.io/en/develop/types.html#structs]

```
struct Funder {
        address addr;
        uint amount;
    }
```

This above code example defines a `struct` of "Funder" to have both 
an address named "addr" and a unit integer named "amount". This is part of a `struct` in an example contract found in a sample crowdfunding contract for the funder. 

`Struct`s cannot contain members of their own type. In other words, a `struct` cannot contain a `struct`. This is because the size of the `struct` must be finite, while nesting `struct`s does not lead to them being finite. 


