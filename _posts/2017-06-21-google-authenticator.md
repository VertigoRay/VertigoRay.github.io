---
layout: post
title: Multi-Factor Authentication: Switching Google Authenticator to Authy
date: 2017-06-21 21:29
author: VertigoRay
comments: true
categories: [Authy, Google Authenticator, LastPass, MFA, Uncategorized]
---
I've been a long time fan of Google Authenticator because Multi-Factor Authentication (MFA) is a must in today's easily compromised society. Unfortunately, Google Authenticator has been a struggle for many people, and I'm glad that I recently discovered Authy.

FYI: 2-Factor Authentication (2FA) is Multi-Factor Authentication. However, not all MFA is 2FA.
<h1>Google Authenticator Woes</h1>
Google Authenticator provides a neat way to use MFA. But it has a massive downside that is mostly ignored. If you lose/reset/replace your phone (which is normally your primary MFA device) then you’re likely completely out of luck. This is why I started using Google Authenticator on my tablet as a backup.

Why? Because all your MFA codes are gone, and never to be seen again. The huge effort in recovering from this sort of mini-disaster makes me cry.

I've finally found the solution that will end these woes. Why has it taken me so long?
<h1>Authy App</h1>
<a href="https://www.authy.com/" target="_blank" rel="noopener">Authy is a fully-fledged</a> MFA service. But don’t get this confused with Google Authenticator. They’re completely different.

What I’m referring to specifically is the <strong>Authy App.</strong> <a href="https://authy.com/blog/authy-vs-google-authenticator/">The Authy App also handles Google Authenticator MFA code registration.</a> This means that instead of using the official Google app, you’ll now use the Authy App instead.

But isn’t the problem of your losing your phone exactly the same? No; because with an Authy account you can now <strong>backup</strong> your Google Authenticator codes off your phone (to your Authy account via the app). You read that right: You now have Google Authenticator backups!

What happens if you lose/reset your phone? You just download the Authy App and retrieve your Google Authenticator codes from their backup.

It’s really as easy as that!
<h1>LastPass Authenticator</h1>
<a href="https://lastpass.com/f?1006456">LastPass</a> is service that remembers your passwords, so that you don't have to.

The <a href="https://lastpass.com/f?1006456">LastPass</a> service is a cloud-based password manager with extensions, mobile apps, and even desktop apps for all the browsers and operating systems you could want. It’s extremely powerful and even offers a variety of <a href="https://helpdesk.lastpass.com/multifactor-authentication-options/">two-factor aumthentication options</a> so you can ensure no one else can log into your password vault. LastPass stores your passwords on LastPass’s servers in an encrypted form – the LastPass extension or app locally decrypts and encrypts them when you log in, so <a href="https://lastpass.com/f?1006456">LastPass </a>couldn’t see your passwords if they wanted to.

<a href="https://lastpass.com/f?1006456">LastPass</a> has recently launched <a href="https://lastpass.com/auth/">LastPass Authenticator</a>. Their app also backups all of your MFA tokens to your <a href="https://lastpass.com/f?1006456">LastPass</a> account. Keep in mind, I'm a huge fan of <a href="https://lastpass.com/f?1006456">LastPass</a>, but <strong>it seems like a horribly bad idea to keep your passwords and MFA backups in the same service. </strong>With that said, I decided to go with Authy.
<h1>Getting Setup in Authy</h1>
You will have to manually tranfer all those Multi-Factor Authentication codes you currently have running on the original Google Authenticator app over to your new Authy app.

You can’t transfer them directly, so it’s more of a “turn it off and on again” process. These are the basic steps:

For every Google Authenticator account you have:
<ol>
 	<li>Go to the original service for the account and remove Google Authenticator 2FA.</li>
 	<li>Re-enable Google Authenticator for that account</li>
 	<li>Use the Authy App instead of Google Authenticator app to register the account.</li>
</ol>
It might be a bit tedious, but if you’ve already experienced the pain that comes with losing your GA codes, then you’ll agree some tedium is a cheap price to pay for the huge upside.

Don't forget to turn on the app <em>protection pin</em>; under settings of the app. This way, your MFA codes have that extra layer of protection from people you otherwise trust to peruse you phone.
