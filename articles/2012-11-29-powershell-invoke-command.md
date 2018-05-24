---
layout: post
title: PowerShell:  Invoke-Command
date: 2012-11-29 20:25
author: VertigoRay
comments: true
categories: [posh, powershell, Uncategorized]
---
<p>Had some issues with <a href="http://technet.microsoft.com/en-us/library/hh849719.aspx" title="Invoke-Command" target="_blank">Invoke-Command</a> today:</p>
<pre>[PS] H:&gt;Invoke-Command -ScriptBlock { get-process } -ComputerName MyScriptServer</pre>
<p><!-- more -->It gave me the following error:</p>
<blockquote>
<div>
<p>Connecting to remote server failed with the following error message : WinRM cannot process the request. The following error occured while using Kerberos authentication: <strong>The network path was not found.</strong></p>
<p> Possible causes are:</p>
<p>  -The user name or password specified are invalid.</p>
<p>  -Kerberos is used when no authentication method and no user name are specified.</p>
<p>  -Kerberos accepts domain user names, but not local user names.</p>
<p>  -The Service Principal Name (SPN) for the remote computer name and port does not exist.</p>
<p>  -The client and remote computers are in different domains and there is no trust between the two domains.</p>
<p> After checking for the above issues, try the following:</p>
<p>  -Check the Event Viewer for events related to authentication.</p>
<p>  -Change the authentication method; add the destination computer to the WinRM TrustedHosts configuration setting or use HTTPS transport.</p>
<p> Note that computers in the TrustedHosts list might not be authenticated.</p>
<p>   -For more information about WinRM configuration, run the following command: winrm help config. For more information, see the about_Remote_Troubleshooting Help topic.</p>
<p>    + CategoryInfo          : OpenError: (:) [], PSRemotingTransportException</p>
<p>    + FullyQualifiedErrorId : PSSessionStateBroken</p>
</div>
</blockquote>
<p>&ldquo;The network path was not found&rdquo; is clearly a DNS resolution error. I would venture to say there is a Name Suffix Routing issue.</p>
<p>The -ComputerName property description says that <em>NETBIOS name</em> should work, but it does not in my testing in my environment. The FQDN is another option for the <em>-ComputerName</em> property and fixed this error for me when done in all lowercase.</p>
<p>Try using (use your FQDN, of course):</p>
<pre><code>Invoke-Command -ComputerName myscriptserver.vertigion.com </code></pre>
<p><strong>Note:</strong> <em>Notice it&rsquo;s in all lowercase.</em> Using camel case (serverA.vertigion.com) failed with the same error.</p>
<p><strong>Note:</strong> I did NOT have the issue with the <em>Enter-PSSession</em> command. I believe there&rsquo;s a bug (or at least a blatant inconsistency) with <em>Invoke-Command</em>.</p>
<p>Another option would be to create the PSSession first (<a href="http://technet.microsoft.com/en-us/library/hh849717.aspx" title="New-PSSession" target="_blank">New-PSSession</a>) and reference it.  This is the option I used as it also prevents constant renegotiation when sending multiple commands back-to-back.</p>
