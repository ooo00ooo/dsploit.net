---
author: evilsocket
comments: true
date: 2013-03-21 22:10:01+00:00
layout: post
slug: how-dsploit-network-discovery-works
title: How dSploit network discovery works
wordpress_id: 82
categories:
- Networking &amp; Internals
tags:
- alive ip
- android
- android sdk
- arp
- dsploit
- dsploit howto
- dsploit internals
- host discovery
- icmp
- ip discovery
- netbios
- netbios query
- networking
- nmap
- query
- sdk
- syn packet
- syn scan
- unicast
- unicast query
---

I'm going to start this section of this blog explaining how every module of dSploit works at low level, both to give users an idea on what they are actually doing and to produce ( hopefully ) some interesting material about network security and generally speaking networking basic principles.

Hence let's start from the beginnig, how dSploit discovers alive hosts on the network :)

<!-- more -->

First of all, let me point out that there are plenty of techniques to accomplish this task, many of them tested for years in dozens of other tools ( and operating systems of course, just think about your "Network" link in the Windows explorer, which discovers alive computers in the same domain of yours ), but not all of them are easily reproducible on an Android device and, most important, not all of them are 100% reliable when your network is composed by computers with different OS.

For this article, let's focus on the three main methods i've tested during dSploit developement:



	
  1. **ICMP/ARP** ping

	
  2. **Syn scan**

	
  3. **NetBIOS** scan




### ICMP/ARP ping


This was the first method dSploit used to discover computers on your network, basically the algorithm is the following:



	
  * Precompute every possible address of the network

	
  * Loop each one and send an ICMP or ARP packet.

	
  * Wait for a reply until a certain timeout.


Every alive host would then answer to the packet ( hopefully before the timeout ) respectively with an ICMP reply or an ARP reply ( this one would contain the mac address of the computer too ) telling us it's alive and kicking.

This would be a good approach if only ICMP and ARP were not two of the most filtered procotols by software and hardware firewalls ... in fact this first attempt was almost totally a failure since many users reported it wasn't working on their networks.


### Syn Scan


This was the second attempt, "well", i said to myself, "i have native tools such as nmap inside dSploit, i have root privileges ... let's pretend I'm running on a normal computer" ... so i came out with syn scanning.

As "Google" says:

    
    The TCP SYN scan uses common methods of port-identification that allow nmap to gather information about open ports without completing the TCP handshake process. When an open port is identified, the TCP handshake is reset before it can be completed. This technique is often referred to as "half open" scanning.


Obviously in this step i didn't give a **** about open ports, but this could be a good method to identify our network neighbours, so it all became:



	
  * Precompute every possible address of the network

	
  * Loop each one and try to syn scan it.

	
  * Parse nmap output to see if the host is alive or not.


Even in this case, only 60% of the users reported this as working, just like the ARP/ICMP case nmap generated traffic gets filtered by firewalls or, most of the cases, dSploit simply couldn't receive an appropriate reply in the given timeout ( low wifi signal, very trafficated networks, God knows what ).


### NetBIOS Scan


And the winner is .... ok ok, let's take a step back :D

One of the many evenings of dSploit developing i was surfing the Play Store searching for some network utility to reverse to find out alternative host discovery methods ... and i came accross [Fing](https://play.google.com/store/apps/details?id=com.overlook.android.fing) .

I suddenly got excited by its discovery feature which worked so well ( and user reported to be working almost 100% of the times ) so i started to decompile and study it ... and then came the light!

The trick was so simple to implement yet so hard to figure out that i was astonished by the ability of the Fing programmer and by its smartness.

The application basically sends the following UDP packet to every possible ip of the network:

    
    0x82 0x28 0x0  0x0  0x0 
    0x1  0x0  0x0  0x0  0x0 
    0x0  0x0  0x20 0x43 0x4B 
    0x41 0x41 0x41 0x41 0x41 
    0x41 0x41 0x41 0x41 0x41 
    0x41 0x41 0x41 0x41 0x41 
    0x41 0x41 0x41 0x41 0x41 
    0x41 0x41 0x41 0x41 0x41 
    0x41 0x41 0x41 0x41 0x41 
    0x0  0x0  0x21 0x0  0x1


This is a **NetBIOS Unicast Query** packet ... in human language, is a request a computer sends to another computer to find out what its netbios name is, if it has networks shares, and so on ( remember the Network thingy in the Windows explorer ? :D )

After sending this - and this is the main concept of this approach - there's absolutely no timeout to wait, the app just needs to [check the file](http://www.emoticode.net/c/arp-lookup-inside-your-system-cache.html) **/proc/net/arp** for changes ... once the packet is sent, this file is suddenly updated with a new empty record like:

    
    192.168.1.xxx     0x1         0x2         00:00:00:00:00:00     *        wlan0


As you might notice, the fourth column contains an empty mac address, which is going to stay empty unless the ip address is found to be alive.
In this case, this line would become:

    
    192.168.1.xxx     0x1         0x2         xx:xx:xx:xx:xx:xx     *        wlan0


With a valid mac address ... and that's not all, if the computer has a netbios service running, we would get a reply to our query with the computer domain name!
So the algorithm became:



	
  * Precompute every possible address of the network

	
  * Loop each one and send the unicast query

	
  * Once we've done, just keep checking the /proc/net/arp file for new valid entries.


Doing this, i had no timeout to worry about and i could keep checking for new hosts even after the first set of packets was sent, because every time a new host became alive, dSploit found a new entry in the ARP file ( and maybe the NetBIOS reply with a fancy domain name to show! )

This whole concept is implemented in the [NetworkDiscover](http://www.emoticode.net/android-sdk/android-sdk-using-netbios-packets-to-discover-network-computers.html) class ... it could be a little messy to read and understand, but i swear it's a really simple concept compared to the first two, and it works in 99% of the cases ( dear 1% WTF you have on your network ?!?!? O.o )

I hope this post will be useful and interesting, since i'd like not only to share my code and my application, but even a little bit of my knowledge to new users ... as usual, i'm sorry for my english :D
