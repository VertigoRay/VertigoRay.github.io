---
layout: post
title: Bond with Adaptive Load Balancing on Ubuntu Server
date: 2017-07-11 06:13
author: VertigoRay
comments: true
categories: [Linux]
---
I was wanting to setup my server with bonded network interface cards (NICs). Since it took me a while to get the bond working, I thought I do some notes to self here; added benefit of sharing with you all.

<h1>Configuration</h1>

This is my <code>/etc/network/interfaces</code> file:

[gist https://gist.github.com/VertigoRay/6b325a0247f94c4b4bba4cacced6dd6f /]

You'll notice that my NICs aren't <code>eth0</code>, <code>eth1</code>, <code>eth2</code>, and <code>eth3</code>. Nope, that would be way too easy. In order to get the names of my NICs, I used: <code>ip link show</code>.

<h1>Decisions</h1>

<img class="size-medium wp-image-282 alignright" style="margin-top: 0.857143rem; margin-bottom: 0.857143rem; margin-left: 1.71429rem;" src="https://vertigion.com/wp-content/uploads/2017/07/adaptive-load-balancing1-300x279.png" alt="Adaptive Load Balancing" width="300" height="279" />I chose to use <code>allow-hotplug</code> on the NICs instead of <code>auto</code>. While booting with <code>auto</code> set, I was getting a significant delay: <em>a start job is running for raise network interfaces (5 mins 1 sec)</em>. This is because <code>auto</code> causes the system to wait for DHCP relay, even if it's set to <code>manual</code>.

Additionally, I chose to have my main NIC boot instantly while the other three NICs would wait five seconds (<code>pre-up sleep 5</code>). This is one method of ensuring that my main NIC was the one that the bond spoofed the mac address of. Another method would have been to specify the <code>hwaddress</code> in the bond; such as:

<pre><code>auto bond0
iface bond0 inet manual
hwaddress fe:80:12:04:6d:6f
</code></pre>

I hope this helps others out there in the ether!
