---
author: evilsocket
comments: true
date: 2013-03-22 00:09:54+00:00
layout: post
slug: dsploit-internals-and-arp-cache-poisoning
title: dSploit Internals and ARP Cache Poisoning
wordpress_id: 93
categories:
- Networking &amp; Internals
tags:
- arp
- arp cache
- arp cache poisoning
- arp poisoning
- arp spoof
- arp spoofing
- attack
- dsploit
- internals
- man in the middle
- mitm
- spoof
- spoofing
---

Here it is the second post about dSploit internals, we we'll discover how dSploit actually can intercept and manipulate traffic which was not originally supposed to receive, thanks to what we will refer as ARP cache poisoning.

The content of this article is taken from "Understanding Man-in-the-Middle Attacks – ARP Cache Poisoning" by windowsecurity.com.

<!-- more -->


### Introduction


One of the most prevalent network attacks used against individuals and large organizations alike are man-in-the-middle (**MITM**) attacks. Considered an active eavesdropping attack, MITM works by establishing connections to victim machines and relaying messages between them. In cases like these, one victim believes it is communicating directly with another victim, when in reality the communication flows through the host performing the attack. The end result is that the attacking host can not only intercept sensitive data, but can also inject and manipulate a data stream to gain further control of its victims.


### ARP Cache Poisoning


One of the oldest forms of modern MITM attack, ARP cache poisoning (sometimes also known as ARP Poison Routing) allows an attacker on the same subnet as its victims to eavesdrop on all network traffic between the victims. I’ve deliberately chosen this as the first attack to examine because it is one of the simplest to execute but is considered one of the most effective once implemented by attackers.


### Normal ARP Communication


The **ARP** protocol was designed out of necessity to facilitate the translation of addresses between the second and third layers of the **OSI model**. The second layer, or data-link layer, uses MAC addresses so that hardware devices can communicate to each other directly on a small scale. The third layer, or network layer, uses IP addresses (most commonly) to create large scalable networks that can communicate across the globe. The data link layer deals directly with devices connected together where as the network layer deals with devices that are directly connected AND indirectly connected. Each layer has its own addressing scheme, and they must work together in order to make network communication happen. For this very reason, ARP was created with **RFC 826**, "_An Ethernet Address Resolution Protocol_".

![Normal ARP behaviour](http://www.dsploit.net/wp-content/uploads/2013/03/arp-poisoning-00.jpg)

The nitty gritty of ARP operation is centered around two packets, an ARP request and an ARP reply. The purpose of the request and reply are to locate the hardware MAC address associated with a given IP address so that traffic can reach its destination on a network. The request packet is sent to every device on the network segment and says “Hey, my IP address is XX.XX.XX.XX, and my MAC address is XX:XX:XX:XX:XX:XX. I need to send something to whoever has the IP address XX.XX.XX.XX, but I don’t know what their hardware address is. Will whoever has this IP address please respond back with their MAC address?” The response would come in the ARP reply packet and effectively provide this answer, “Hey transmitting device. I am who you are looking for with the IP address of XX.XX.XX.XX. My MAC address is XX:XX:XX:XX:XX:XX.” Once this is completed the transmitting device will update its ARP cache table and the devices are able to communicate with one another.


### Poisoning the Cache


ARP cache poisoning takes advantage of the insecure nature of the ARP protocol. Unlike protocols such as DNS that can be configured to only accept secured dynamic updates, devices using ARP will accept updates at any time. This means that any device can send an ARP reply packet to another host and force that host to update its ARP cache with the new value. Sending an ARP reply when no request has been generated is called sending a gratuitous ARP. When malicious intent is present the result of a few well placed gratuitous ARP packets used in this manner can result in hosts who think they are communicating with one host, but in reality are communicating with a listening attacker.

![ARP behaviour during a dSploit MITM attack.](http://www.dsploit.net/wp-content/uploads/2013/03/arp-poisoning-01.jpg)


