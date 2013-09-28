---
author: evilsocket
comments: true
date: 2013-03-20 20:53:52+00:00
layout: page
slug: faq
title: FAQ
wordpress_id: 30
---




### **What is a rooted device ? How do i root my device ?**


Rooting a device is a procedure that will unlock administrative privileges on it, allowing you to run utilities which requires higher privileges
than the usual.

It's very device specific, there's no "universal rooting guide", therefore you have to google something like "how to root PUT-YOUR-DEVICE-MODEL-HERE".

However, if you don't know what rooting is, probably you won't need dSploit because it's intended for a tech/geek user who knows how to perform such procedures
without bricking the device itself.

**What is busy box ? How do i fully install it ?**

BusyBox is a free software which offers almost every command line utility usually available on a Unix platform, to install it on your ( previously rooted ) device,
you can use the [BusyBox Istaller](https://play.google.com/store/apps/details?id=com.jrummy.busybox.installer) available on the Play Store
which is a pretty straightforward procedure.

During the installation process make sure you install at least the 1.20 version of busybox.

**Why every functionality is disabled when i turn off wifi ?**

90% of dSploit modules work only on a standard TCP/IP layer, therefore they wouldn't work anyway on 3G/4G/whatever.

Other modules, such as the port scanner and so on, would generate a lot of network traffic to remote endpoints, and it could
be considered a service abuse from your phone provider.

**I keep getting the "Full BusyBox installation required, killall binary not found ( maybe you have an old busybox version )." message! WTF?**

Probably you have an old installation of BusyBox ( < version 1.20 ) or your installation is corrupted, please update it to a newer version.






**I keep getting the "It seems like your ROM has the LD_LIBRARY_PATH bug, i'm sorry but it's not compatible with dSploit." message! WTF?**

dSploit needs it's own native libraries to run the tools it needs, those libraries are bundled with the application itself and get installed on first launch.
Some Android ROMS ( we are building a complete list of those ) [have a "bug"](https://github.com/evilsocket/dsploit/issues/35) in the way the system linker works, preventing dSploit to load those libraries at runtime, therefore
causing this message.

In this case, if you can, please upgrade your ROM to a newer one.

**I keep getting the "Error during files installation!" message! WTF?**

You don't have enough space left on your device, please make sure you ave around 50MB free before installing dSploit.

**The application is really slow and MITM features don't work/crash!**

This is probably a **SU / SuperUser** issue ( which is way too slow ), try replacing it with **SuperSU** by flashing the **CWM-SuperSU** zip package in recovery mode,
this is the best way to ensure your old su installation gets overwritten by SuperSU. Many users have reported substantial performance improvement when switching to SuperSU as well as
problems related to MITM modules being solved.

Besides make sure you have the latest version of SuperSU and BusyBox installed.

**I don't see my other computers on the same network, what's happening ?**

There are two possible issues, either your router/gateway has some sort of firewall and/or protection, or your ROM is
not compatible with dSploit ( see previous FAQ ).

**I've found a bug/there's a new feature i'd like to see implemented, how can i reach the dev team ?**

You can open a [new issue](https://github.com/evilsocket/dsploit/issues) on GitHub, but first **please** make sure there's not
the same issue of yours already opened.

**I can't get the app work in portrait mode!**

The app is made to work only in landscape mode and will stay landscape even if you rotate your device, if you have an application such as Rotation Control to force every app to rotate, probably you are going to see dSploit crash.

This is something i want to be like this, every interface is designed to work in landscape, so do not submit issues related to rotation.

**I keep getting super user toast notifications, what's happening ?**

If the app keeps asking you for root privileges every 2-3 seconds, this is not a dSploit bug, but a bug of the application which handles the authorizations as [documented here](https://github.com/evilsocket/dsploit/issues/2), so please do not submit bugs about that and start using something really functional like **[SuperSU](https://play.google.com/store/apps/details?id=eu.chainfire.supersu)** from chainfire.


