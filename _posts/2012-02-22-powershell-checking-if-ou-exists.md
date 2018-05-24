---
layout: post
title: PowerShell - Checking if OU exists
date: 2012-02-22 16:54
author: VertigoRay
comments: true
categories: [Active Directory, AD, LDAP, OU, posh, powershell, Uncategorized]
---
<p>After starting work on a function, I stumbled across the sourced link.  I wanted to expand on that post.</p>
<p>That simple method only works well if the LDAP Path is <a href="http://lmgtfy.com/?q=What+is+clean+data?" title="What is clean data?" target="_blank">clean</a>.  If you&rsquo;re possibly working with unclean data (or typo the DC structure), you&rsquo;ll need to catch your errors.<!-- more --></p>
<div class="gist"><a href="https://gist.github.com/VertigoRay/6091753">https://gist.github.com/VertigoRay/6091753</a></div>
<p>Since <em>DC=domain,DC=com</em> doesn&rsquo;t exist (or at least isn&rsquo;t accessible for an LDAP query), I get the following outputted from the above example; which is expected, since I threw the <em>Supplied Path is invalid</em> error (you can handle the error however you want):</p>
<pre>Supplied Path is invalid.
Exception calling "Exists" with "1" argument(s): "A referral was returned from the server.
[...]</pre>
<p>In my case, I only work within a particular OU in our Domain, so I&rsquo;ve made it so my <em>$Path</em> can be abbreviated.  Here&rsquo;s how I handle things:</p>
<div class="gist"><a href="https://gist.github.com/VertigoRay/6091801">https://gist.github.com/VertigoRay/6091801</a></div>
<p>If the <em>OU=foo,OU=test,DC=domain,DC=com</em> OU exists, the following will be outputed, in the above example:</p>
<pre>DEBUG: Path Exists (2):  OU=foo,OU=test,DC=domain,DC=com</pre>
<p>Hope this helps others out there.  Cheers!</p>
