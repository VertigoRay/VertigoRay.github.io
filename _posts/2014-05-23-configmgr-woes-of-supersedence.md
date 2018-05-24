---
layout: post
title: ConfigMgr: Woes of Supersedence
date: 2014-05-23 15:39
author: VertigoRay
comments: true
categories: [ConfigMgr, Office2010, Office2013, SCCM, Uncategorized, Upgrade]
---
<p>I was tasked with getting an Office 2013 upgrade set-up for early adopters and forced on our deadline. After I built and tested the application, I marked O2013 as superseding O2010 and made O2013 available. The plan was to make another <em>Required</em> deployment for our deadline.  O2013 unexpectedly installed on several machines that night.<!-- more --></p>
<p>The next morning, I got word and was livid.  I removed the supersedence relationship – the issue did not continue to propagate.  I thought the functionality was not aligned with <a href="http://technet.microsoft.com/en-us/library/gg682071.aspx" target="_blank">MS’s documentation on the subject</a> (yes, I read the docs), which explicitly states:</p>
<blockquote>
<p><em>“When you supersede an application, this applies to all future deployments and Application Catalog requests. This will not affect the existing installations of the application.”</em></p>
</blockquote>
<p>It turns out that when you deploy an Application that supersedes another Application, and you have it as <em>Install Available</em> (not Required) you have to pay attention to the verbiage of the <em>Scheduling</em> pane; the bottom is not greyed out due to the supersedence.  The verbiage of the schedule pane says “Installation deadline to <strong>upgrade</strong> users or devices <strong>that have the superseded application installed</strong>” … and notice is defaults to <em>As soon as possible</em>.  I skipped over this pane since it’s normally greyed out when you mark things as <em>Install Available</em>.</p>
<p>That is why Office 2013 immediately started upgrading Office 2010 … cause I told it to.  Lesson learned.</p>
