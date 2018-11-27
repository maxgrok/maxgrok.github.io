---
title: "PoW vs. PoS"
date: "2018-11-09T11:00:13.121Z"
layout: post
draft: false
path: "/posts/sixty-fourth-post/"
category: "Blockchain"
tags:
  - "Bitcoin"
  - "Blockchain"
  - "P2P"
description: "This is a post about Ethereum Proof of Work versus Proof of Stake mining processes."
---

This is a post about the difference between Proof of Work versus Proof of Stake processes. 

## Blockchain Basics: Consensus

Consensus is the state of agreement among each node in the blockchain network. In order to reach consensus, there are two main strategies employed: proof-of-work (PoW) and proof-of-stake (PoS).  

## PoW vs. PoS: The Basics

I recommend watching this quick video: [PoW vs. PoS Video Explainer][https://www.youtube.com/watch?v=ASCGQFZgcT8&feature=youtu.be]

Proof of Work (PoW) is the method by which miners reach consensus by providing proof of solving increasingly complex mathematical problems. [PoW vs. PoS][https://www.ethnews.com/proof-of-work-vs-proof-of-stake-explained]

> Proof of Work (PoW)
>- Particpants only accept valid block when blockhash is less than target number
>- Miners in a network repeatedly hash the block contents and check the output to see if it matches some specific criteria.
>- When the correct block hash is found it is broadcasted throughout the entire network and the miner is awarded.
>- Blocks are mined a deterministic rate (every 15 seconds in the Ethereum Network)

<br>[Consensys Academy Notes][https://github.com/ScottWorks/ConsenSys-Academy-Notes/blob/master/Part%201%20-%20Review%20of%20Blockchain%20Technology.md]

Proof of Stake (PoS) is when the creator of a new block is chosen via various combinations of random selection and wealth or age [Proof of Stake (PoS) - Wikipedia][https://en.wikipedia.org/wiki/Proof-of-stake].

> Proof of Stake (PoS)
>- Currency holders stake some amount of the currency for the chance to validate a block.
>- The block validator is randomly selected by the network but the chance of selection is proportional to the stake.

<br>[Consensys Academy Notes][https://github.com/ScottWorks/ConsenSys-Academy-Notes/blob/master/Part%201%20-%20Review%20of%20Blockchain%20Technology.md]

For more in depth Proof of Work explainer video, watch this video from [Khan Academy][https://www.youtube.com/watch?v=9V1bipPkCTU&feature=youtu.be].

## PoW: Mining

>- In the Proof-of-Work consensus scheme, mining is the process of validating transaction blocks through hashing the block contents. This process makes it incredibly difficult to guess the correct answer but very easy to verify the correct guess has been made.
>- Each time a node wins the block they suggest the next state of the system and broadcast their solution to the network. Other nodes verify that the solution is correct and update their ledgers such that the validator recieves the block reward.
>- The difficulty is adjusted based on how quickly the previous block was mined.
>- Each block contains a list of transactions, the hash of the most recent block, nonce, and block reward.
>- The Ethereum proof-of-work algorithm abides by three main rules:
>>1.  Rejects invalid blocks
>>2.  Requires proof of work to contain a hash less than the target block #
>>3.  Longest chain is always considered to be the most up-to-date/ trusted

<br>[Consensys Academy Notes][https://github.com/ScottWorks/ConsenSys-Academy-Notes/blob/master/Part%201%20-%20Review%20of%20Blockchain%20Technology.md]


## Issues with PoW: 51% attack && The Environment

### 51% attack

This occurs when the network that computes the transactions is controlled by a mining pool that does more then 51% of the mining for block transactions. This goes against decentralization and creates a control over the transactions being processed in the hands of a small number of individuals. 

With this power, the mining pool could collectively invalidate transactions and double spend, which defeats the trustless protocols purpose. 

For more on 51% attacks, read [PoS vs. PoW: 51% attack section][https://www.ethnews.com/proof-of-work-vs-proof-of-stake-explained]. 

### The Environment

It can require tremendous computing power to provide proof of work. This limits participation in mining, as well as creates negative externalities for the environment. 

## Who uses PoW? 

5 cryptocurrencies that use PoW: <br><br>
[Ether][https://www.ethereum.org/ether]<br>
[Bitcoin][https://bitcoin.org/en/]<br>
[BitcoinCash][https://cryptoslate.com/coins/bitcoin-cash/]<br>
[LiteCoin][https://cryptoslate.com/coins/litecoin/]<br>
[Verge][https://cryptoslate.com/coins/verge/]<br>

## Who uses PoS?

5 cryptocurrencies that use PoS:<br><br>
[Dash][https://www.dash.org/]<br>
[PeerCoin][https://peercoin.net/]<br>
[NEO][https://en.wikipedia.org/wiki/NEO_(cryptocurrency)]<br>
[Factom][https://www.factom.com/]<br>
[PIVX][https://pivx.org/]<br>


## Conclusion 

Both Proof of Work (PoW) and Proof of Stake (PoS) are different methods for obtaining the same thing: consensus among nodes in a blockchain. The main difference is that instead of solving complex mathematical problems to validate blocks (PoW), PoS requires that one have a significant stake in the blockchain network chosen randomly to validate a block. 

Thanks so much for reading! Now, you know the difference between proof of work and proof of stake!