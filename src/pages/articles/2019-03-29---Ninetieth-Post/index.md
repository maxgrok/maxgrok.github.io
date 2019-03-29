---
title: "What's the difference between UDP and TCP?"
date: "2019-03-29T10:00:13.121Z"
layout: post
draft: false
path: "/posts/ninetieth-post/"
category: "Networking"
tags:
  - "Networking"
  - "TCP"
  - "UDP"
description: "This is a post about the difference between UDP and TCP and use cases for them both."
---

<em>Warning: This post presumes a level of beginners knowledge of networking concepts such as IP addresses and some basic familiarity with setting up a network.</em>

## Introduction 

As I have grown as a full stack developer, I have decided to learn about networkign and the infrastructure that makes up the basic abilities of users on the Internet. I'll start this exploration by exploring the differences between UDP and TCP IP protocols. 

## Definition 

An network protocol "defines rules and conventions for communication between network devices" (<a href="https://www.lifewire.com/definition-of-protocol-network-817949">Source</a>). The Internet Protocol family contains a set of related network protocols (<a href="https://www.lifewire.com/definition-of-protocol-network-817949">Source</a>). 

The most common type of protocols for the Internet are TCP and UDP. 
TCP stands for transmission control protocol, whereas UDP stands for user datagram protocol.  

## Similarities and Differences: TCP vs. UDP

Both rely on IP protocols. However, each is used in different scenarios and with different frequencies. TCP (i.e. TCP/IP) is used when reliability is prioritized over speed of packets sent. It is the most widely used protocol on the Internet. TCP/IP numbers the packets sent and then checks them for errors, so that packets are not lost. This is important when sending email for example.

On the other hand, UDP (UDP/IP) is faster than TCP and does not include the error catching capabilities of TCP/IP. So, it is more commonly used for live broadcasting or gaming; situations where error catching and reliability are not an issue. 

## Conclusion

- TCP :
    + most commonly used protocol on the Internet
    + two way communication
    + serious about reliability
        * orders packets by numbering them
        * packets are error-checked
- UDP:
    + doesn't do error checking done in TCP
    + packets are just sent to the recipient
    + used when speed is more desirable than reliability
        * live broadcasting
        * gaming

Now, you know the differences between UDP and TCP! 

