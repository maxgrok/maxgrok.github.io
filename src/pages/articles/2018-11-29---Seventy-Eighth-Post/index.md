---
title: "Build Your Own Ethereum Block Display Site"
date: "2018-11-30T04:30:13.121Z"
layout: post
draft: false
path: "/posts/seventy-eighth-post/"
category: " Blockchain"
tags:
  - "Blockchain"
  - "Ethereum"
  - ""
description: "This is a post about how to build a ethers.io API empowered site to explore the Ethereum blockchain."
---

## Pre-requisites: 
git
nvm
node.js
MetaMask
Basic knowledge of blockchain

---------------------

Install ethers-cli

`npm install -g ethers-cli`
`mkdir explorer`
`cd explorer`
`touch index.html`

```html
    <html>
        <head>
            <title>Block Explorer</title>
        </head>
        <body>
            Hello World!
            <script type="text/javascript" src="https://cdn.ethers.io/scripts/ethers-app-v0.2.min.js"></script>
        </body>
    </html>
```
To get the deploy to work with the 0.5v of ethers-cli, you need to deploy this: 

`ethers-deploy serve --rpc http://localhost:8080`

Go to your browser and navigate to `localhost:8080/`.

Then navigate to the localhost:8080. Make sure you have MetaMask running as well. Also, enable insecure dApps to run otherwise your dApp will not work! 

You should see your 'Hello World!' displayed on screen!

Now, let's add some Javascript code in a separate script tag to the HTML document to get the latest 10 blocks validated on the Ethereum blockchain. 

```html
<script>
            ethers.onready = function() {
                updateBlocks();
            }

            function updateBlocks() {
                var lastBlockNumber = ethers.blockchain.getBlockNumber();
                lastBlockNumber.then(function(number) {
                    console.log('The last block number: ' + number);
                    for(var i=0; i<10; i++) {
                        ethers.blockchain.getBlock(number-i).then(function(block) {
                            printBlock(block);
                        });
                    }
                });
            }

            function printBlock(block) {
                var table = document.getElementById('blocks');
                var row = table.insertRow(-1);
                var cell1 = row.insertCell(0);
                var cell2 = row.insertCell(1);
                var cell3 = row.insertCell(2);
                cell1.innerHTML = block.number;
                cell2.innerHTML = block.hash;
                cell3.innerHTML = block.timestamp;
            }
        </script>     
```

Let's go ahead and remove the `hello world!` from our application and replace it with the following code to display the latest 10 blocks!

```html
<table id="blocks" width="100%">
            <tr>
                <th>Number</th>
                <th>Hash</th>
                <th>Timestamp</th>
            </tr>
        </table>
```

Now, let's deploy our app on the localhost!

Go to your command line and type `ether-build serve`

Go to your `localhost:8080` and you should see all the last 10 latest blocks validated by the Ethereum blockchain! 

## Congratulations! You've built your first blockchain site interacting with the ethers API. 

## Bonus Points

Google around and find out how to install and add your files to `ipfs` for a decentralized site!



