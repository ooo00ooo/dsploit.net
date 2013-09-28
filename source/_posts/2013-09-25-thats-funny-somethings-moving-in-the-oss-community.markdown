---
layout: post
title: "That's funny, something's moving in the OSS community."
date: 2013-09-25 21:46
comments: true
categories: News 
---

I have to admit it, a few hours ago when I saw the email from github which notified me about the [Androguide](https://github.com/evilsocket/dsploit/pull/291) **huge** pull
request, a smile appeared on my face.  
Just 24 hours ago I announced about dSploit being an abandoned project due to the lack of support from the OSS community and today I received from [Louis Teboul](https://github.com/Androguide) one
of the biggest code patches I've ever seen.  

What he did, whas a complete refactoring, patching, restyling and translating of the project, as he states in his pull request:  

_This pull-request aims at modernizing dSploit in terms of design, tooling and UX._

The following changes were made, in a separate "gradle" branch:

- Integration with the new Gradle-based android build system as well as the Android Studio IDE
- Full refactoring of the user interface, for a more modern, Holo-compliant design (see screenshots below)
- dSploit is now almost fully translatable (the plugins will need their constructors to be refactored to make the plugin selection screens translatable)
- Added partial French translation
- A lot of refactoring and use of syntactic sugar for a cleaner code which is more compliant with the Java conventions, as well as some performance tuning and extra error-checking

<!-- more -->

<ul style="margin:0; padding:0; list-style-type:none;">
<li style="float: left; margin-right:5px">
<a href="https://f.cloud.github.com/assets/2505731/1210894/eaea7536-2600-11e3-8f4f-52f79a2453e1.png" target="_blank">
<img src="https://f.cloud.github.com/assets/2505731/1210894/eaea7536-2600-11e3-8f4f-52f79a2453e1.png" style="height:320px;"/>
</a>
</li>
<li style="float: left; margin-right:5px">
<a href="https://f.cloud.github.com/assets/2505731/1210890/eadf4da0-2600-11e3-87e6-1fb6025c6cdc.png" target="_blank">
<img src="https://f.cloud.github.com/assets/2505731/1210890/eadf4da0-2600-11e3-87e6-1fb6025c6cdc.png" style="height:320px;"/>
</a>
</li>
<li style="float: left; margin-right:5px">
<a href="https://f.cloud.github.com/assets/2505731/1210891/eae0be4c-2600-11e3-89f4-3656bc21be0b.png" target="_blank">
<img src="https://f.cloud.github.com/assets/2505731/1210891/eae0be4c-2600-11e3-89f4-3656bc21be0b.png" style="height:320px;"/>
</a>
</li>
<li style="float: left; margin-right:5px">
<a href="https://f.cloud.github.com/assets/2505731/1210892/eae49558-2600-11e3-8820-018f0c975276.png" target="_blank">
<img src="https://f.cloud.github.com/assets/2505731/1210892/eae49558-2600-11e3-8820-018f0c975276.png" style="height:320px;"/>
</a>
</li>
<li style="float: left; margin-right:5px">
<a href="https://f.cloud.github.com/assets/2505731/1210893/eae92398-2600-11e3-8bef-f902f256569d.png" target="_blank">
<img src="https://f.cloud.github.com/assets/2505731/1210893/eae92398-2600-11e3-8bef-f902f256569d.png" style="height:320px;"/>
</a>
</li>
</ul>
<br style="clear: both;"/>

What can I say? Just **thanks** ... the project will go on, thanks to [Louis Teboul](https://github.com/Androguide) contribution which made me think and gave me new hope ( no, I'm not
exaggerating, I really am **this** passionate about my projects ).

