---
layout: post
title: "Changelog for 1.1.1b-20131229 new nightly release."
date: 2013-12-29 18:28
comments: true
categories: News
---

I've just built a <a href="http://update.dsploit.net/nightly">new nightly release</a> and uploaded the signed APK since many of you guys was asking for it, I'm sorry if I didn't make a new release every day, but there were a lot of small changes and fixes I wanted to incorporate in a whole new package.  
This is a changelog with major changes. All of this thanks to **Massimo Dragano** ( tux-mind ) who's actively working on the project.
The new release aims to improve integration with the Metasploit framework, fix many issues, improve spawned processes handling and … fix the LD_LIBRARY_PATH bug/limitation!

<!-- more -->

Have an happy new year guys, and remember to make a donation to the project!

<center>
  <a href='http://www.pledgie.com/campaigns/22257'><img alt='Click here to lend your support to: dSploit and make a donation at www.pledgie.com !' src='http://www.pledgie.com/campaigns/22257.png?skin_name=chrome' border='0' /></a>
</center>

* new upgrade service ( uses notifications )
* tools can now compiled using the android NDK
* **tools is built statically ( solves LD_LIBRARY_PATH bug )** ( fuck yeah! )
* improved the way we use root shells ( **a lot improved** )
* now inspector can be run without the port scanner
* some UI elements modifications
* created a PreferenceActivity for manage options of MSF modules
* Session class allow us to handle MSF opened sessions
* created a very poor shell interface ( for opened MSF sessions )