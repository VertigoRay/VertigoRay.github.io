---
layout: post
title: Synergy - Send CTRL+ALT+DEL to Client
date: 2014-01-02 21:19
author: VertigoRay
comments: true
categories: [Uncategorized]
---
<p>I&rsquo;m mostly posting this here for ease of finding it in the future.  It seems like most people prefer to disable CTRL+ALT+DEL instead of actually allowing the <em>Synergy service</em> to initiate the Secure Attention Sequence (aka: CTRL+ALT+DEL).</p>
<p>Since the location of the Policy setting changes from Win7 to Win8, I&rsquo;m going to tell you how to search/filter for it.  <strong>From the client</strong>, follow these steps:</p>
<ol><li>Lauch <em>Local Group Policy Editor<br /></em>(Run: <em>gpedit.msc</em>)</li>
<li>Browse to: <strong>Computer Configuration &gt; Administrative Templates &gt; All Settings</strong></li>
<li>Click <em>Action &gt; Filter Options</em>, from the Main Menu.</li>
<li>Check the box to <em>Enable Keyword Filters</em>.</li>
<li>Filter for the word:  <strong>Ease</strong></li>
<li>Click: OK</li>
</ol><p>The only (as of the time of this writing) policy that should show up is <strong><em>Disable or enable software Secure Attention</em><em> Sequence</em></strong>.  Edit the policy and ensure the settings are:</p>
<ul><li><span><strong>Enabled</strong></span></li>
<li><span>Options: <strong>Services<br /></strong><em>(Note:  <strong>Services and Ease of Access applications</strong> will also work.)</em></span></li>
</ul><p><span>Once you click <strong>Apply</strong>, the settings will take affect.  Press <strong>CTRL+ALT+PAUSE/BREAK</strong> to initiate the Secure Attention Sequence on the client.</span></p>
