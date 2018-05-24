---
layout: post
title: PowerShell: Get-FileEncoding
date: 2015-02-04 00:46
author: VertigoRay
comments: true
categories: [.net, encoding, posh, powershell, Uncategorized]
---
I often work in PowerShell, and one day I needed to create a script that would pull the file encoding out a file.
<h1>Encodings</h1>
However, this proved to be difficult since most encodings don’t require a BOM (Byte Order Mark). <a href="http://stackoverflow.com/a/18918330/615422">Here’s some good information that I found on the subject:</a>
<blockquote>Automatically determining the correct encoding for a given byte array is notoriously difficult. Sometimes, to be helpful, the author of the data will insert something called a BOM (Byte Order Mark) at the beginning of the data. If a BOM is present, that makes detecting the encoding painless, since each encoding uses a different BOM.

However, the problem remains, how do you automatically detect the correct encoding when there is no BOM? Technically it's recommended that you don't place a BOM at the beginning of your data when using UTF-8, and there is no BOM defined for any of the ANSI code pages. So it's certainly not out of the realm of possibility that a text file may not have a BOM. If all the files that you deal with are in English, it's probably safe to assume that if no BOM is present, then UTF-8 will suffice. However, if any of the files happen to use something else, without a BOM, then that won't work.</blockquote>
<!-- more -->
<h1>The Code</h1>
<div>[gist https://gist.github.com/VertigoRay/ce40c0b44b4dc4b34646 /]</div>
<h1>Credits</h1>
I came across some code on a PowerShell sharing site, <a href="http://poshcode.org">POSHCode.org</a>,  that inspired me to do things a different way. So, I <a href="http://poshcode.org/5724">made the ammendments there as well</a>. Unfortunately, since I've written this blog, it appears that POSHCode has gone down for the count:

[caption id="attachment_140" align="alignnone" width="300"]<img class="size-medium wp-image-140" src="https://vertigion.com/wp-content/uploads/2015/02/poshcode.org-is-almost-here-300x167.jpg" alt="poshcode.org is almost here! Upload your website to get started." width="300" height="167" /> Screenshot taken: June 21, 2017.[/caption]
