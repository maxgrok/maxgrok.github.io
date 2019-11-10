---
title: "How to Deploy Your Smart Contract to Production"
date: "2019-10-27T09:29:13.121Z"
layout: post
draft: true
path: "/posts/one-hundred-and-eighth-post/"
category: "Ethereum"
tags:
  - "Solidity"
  - "Buddy"
  - "Mainnet"
description: "This is a post about how to deploy your Solidity smart contract to the mainnet via Infura and Buddy CI and Github."
---
In this post, I will teach you how to deploy your Solidity smart contract to the mainnet via Infura with BuddyCI and Github. 

Prior requirements: 
  - knowledge of javascript, git, solidity, CLI
  - have a <a href="https://www.github.com/">github account, <a href="www.infura.io">infura</a> account, and <a href="https://buddy.works/">buddy CI </a> account. 
  - smart contracts already written, audited, and ready for deployment
      - here's a sample of a <a href="https://github.com/maxgrok/SimpleStorage/">smart contract</a> that you can deploy. 

## Select Github Repo

![buddy-ci(1)](./buddy-ci(1).png)<br/>

![buddy-ci(2)](./buddy-ci(2).png)<br/>

## Add a Pipeline to Buddy CI
![buddy-ci(3)](./buddy-ci(3).png)<br/>

Execute it "On Push". 

## Edit your truffle-config.js file

Run `npm install truffle-hdwallet-provider`. 

Copy and paste the following into your truffle-config.js file, replacing the <project_id> with your Infura project id. 

```javascript
const path = require("path");
const HDWalletProvider = require("truffle-hdwallet-provider");

const infuraURL = "https://mainnet.infura.io/v3/<project_id>";
const infuraRinkebyURL = "https://rinkeby.infura.io/v3/<project_id>";
const mnemonic = process.env.PRIV_SEED;

module.exports = {
  // See <http://truffleframework.com/docs/advanced/configuration>
  // to customize your Truffle configuration!
  contracts_build_directory: path.join(__dirname, "client/src/contracts"),
  networks: {
    develop: {
      host: "127.0.0.1",
      port: 7545,
      network_id: "*"
    },
    "rinkeby":{
      provider: ()=> new HDWalletProvider(mnemonic, infuraRinkebyURL),
      network_id: 4
    },
    "mainnet":{
      provider: () => new HDWalletProvider(mnemonic, infuraURL),
      network_id: 1
    }
  }
};

```

Get your mnemonic seed phrase from your Metamask account by selecting Settings and Security then enter your password to gain access to your seed phrase and add it as an environment variable in Buddy CI pipeline called "PRIV_SEED". 

If you do not have Rinkeby test ether in your account, then now is a good time to get some here at the <a href="https://faucet.rinkeby.io/">Rinkeby Faucet</a> by following the instructions there. 

## Add the install truffle-hdwallet-provder script

Add `npm install truffle-hdwallet-provider` to your environment under the `npm i -g truffle` script. 

## Rinkeby or Mainnet

Decide if you want to deploy your smart contract to the testnet (Rinkeby in this case) or mainnet (warning: costs real ETH). 

Depending on what you decide, you want to configure your pipeline action to run the following: 
### Mainnet Command

`truffle migrate --network mainnet`

### Rinkeby Command

`truffle migrate --network rinkeby`

## Make a Github Push to Deploy to Production

run `git init` within your project directory to start a git 
run `git add .` to add the changes in your truffle-config.js file to your staging area. 
run `git commit -m 'changing truffle-config.js to include mainnet and rinkeby'`
run `git remote add origin <your github repo address here>`
run `git push origin master`

This will push all the files and history up to your github repo, which will automaticaly trigger the Buddy CI to run. 

## Check the logs

Check the logs on your Buddy CI pipeline by logging into your account and selecting your project, if you don't already have it open in another window. 

## Success! 

![buddy-ci(success)](./buddy-ci(success).png)

Hopefully, you have succeeded in deploying your contract to the mainnet or rinkeby. It's your choice. Depending on what you choose, you will see some variation of the above and it will take a variable amount of time to complete the mining of the transaction/contract on the network (ethereum mainnet takes approximately ~12 seconds per block). 

## Extra Credit

Explore Buddy CI and see how to send yourself a notification email on production deploy or to setup an approval requirement for admins to execute deploy. 




