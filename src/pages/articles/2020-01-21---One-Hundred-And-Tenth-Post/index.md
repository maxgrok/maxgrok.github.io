---
title: "How to Deploy to Rinkeby or Mainnet w/ Truffle"
date: "2020-01-21T14:00:13.121Z"
layout: post
draft: false
path: "/posts/one-hundred-and-tenth-post/"
category: "Ethereum"
tags:
  - "Solidity"
  - "Deployment"
  - "Truffle"
description: "This is a post about how to use truffle-hdwallet-provider to deploy Solidity smart contracts to the Rinkeby testnet or Mainnet."
---

Pre-requisites: Truffle project with Solidity smart contracts all ready to be deployed. Infura project ID. Metamask. Rinkeby testnet Ether or mainnet Ether.  

First, within your project directory, use npm to install truffle-hdwallet-provider with `npm install truffle-hdwallet-provider --save-dev` command. 

Second, include truffle-hdwallet-provider in your `truffle-config.js` file in your Truffle project by copying the following code at the top of your `truffle-config.js` file. 

```js
const HDWalletProvider = require('truffle-hdwallet-provider');

```

Third, define your provider, infuraKey, and infuraURL below the HDWalletProvider declaration for both rinkeby and the mainnet. You can choose one or the other or both as options. 

```js
const infuraKey ="234s234dsfkjl..." 
const infuraURL = `https://rinkeby.infura.io/v3/${infuraKey}`;
const infuraMainnetURL = `https://mainnet.infura.io/v3/${infuraKey}`

const mainNet = new HDWalletProvider(yourMnemonicHere, infuraMainnetURL)
const provider = new HDWalletProvider(yourMnemonicHere, infuraURL);
```

Fourth, within the module.exports and within networks declaration, define the rinkeby and/or mainnet network like the following: 

```js
    rinkeby: { 
        provider: () => provider,
        network_id: 4, 
        gas: 5500000
    }, 
    mainnet: {
        provider: () => mainNet,
        network_id: 1, 
        gas: 5500000
    }
```

Fifth, run `truffle migrate --network rinkeby` to deploy to the Rinkeby testnet or `truffle migrate --network mainnet`, if you are deploying to the mainnet. 

Wait for your contracts to compile and migrate and deploy! 

## Congratulations! 

If all went well, you have deployed your contract to the Rinkeby testnet and/or the Ethereum Mainnet!
