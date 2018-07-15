---
layout: post
title: Salt Stack - salt-osx-grains
date: 2013-08-22 21:40
author: VertigoRay
comments: true
tags: [Apple, Salt Stack, Uncategorized]
---
<p>During my <a href="http://go.vertigion.com/AdventuresWithSaltStack">adventures with Salt Stack</a>, I found that the <a href="http://docs.saltstack.com/topics/targeting/grains.html" target="_blank">grains</a> lacked a couple of key bits on information for OS X:</p>
<ul><li><a href="http://bit.ly/189M2So" target="_blank">Apple Model Number</a></li>
<li><a href="http://bit.ly/15Pz902" target="_blank">Apple Serial Number</a></li>
</ul><p>Additionally, I decided that it would be useful to store the computer&rsquo;s <em>Company Asset Number</em> in <a href="http://bit.ly/17OBJRL" target="_blank">nvram</a>, and make that available in grains.<!-- more --></p>
<p>To solve this, I made some customized grains and <a href="https://github.com/VertigoRay/salt-osx-grains" target="_blank">made them available on GitHub</a>.</p>
<p>If you want to know how to use the customized grains, <a href="https://github.com/VertigoRay/salt-osx-grains/wiki" target="_blank">check out the wiki</a>.</p>
<p>If you have issues with the custom grains, please <a href="https://github.com/VertigoRay/salt-osx-grains/issues" target="_blank">use the issue tracker</a>.</p>
<p>General questions and comments can be made here and I’ll get to them as I can.</p>
<p>Tested on: 10.8.4</p>
