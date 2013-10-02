---
layout: post
title: "A new team member ... MetaSploit coming to v1.1.0b!"
date: 2013-10-02 16:43
comments: true
categories: News
---

I'm happy to annouce that [Massimo Dragano](https://github.com/tux-mind) aka tux-mind decided to merge his modifications
of dSploit with the master branch, joining the list of the offial contributors and [team members](/the-team/) of the project.

I don't have words to describe his work on dSploit, so I'll use what he wrote me in the [pull request](https://github.com/evilsocket/dsploit/pull/304) on GitHub: 

    hi evilsocket,
    i finally got msfrpc working properly.
    there are a lot of cool stuff to carry on... exploit options, sessions, shells handlers and so on.
    if you add me to the repo collaborators i'll be glad to help you to get dSploit always better ;)

    why i do this?
    sincerely i hate java, i always used C, and i love it.
    but the prospective that i can leave meterpreter backdoors in every nearby unsecured PC from my phone, it's awesome!
    infect on the fly for explore them later, easily from my home. wonderful!

    i hope that my work will improve dSploit a lot :)

    bye!

    PS:
    the gentoo armv7a system image with msf inside can be downloaded here:
    http://androtransfer.com/?developer=tux_mind

<!-- more -->

What he did, was implementing a RPC interface to a MetaSploit installation running on a Gentoo image on the device itself, allowing
the future user of dSploit to use the main features of MetaSploit on their handled devices ... stay tuned for the 1.1.0b!!!