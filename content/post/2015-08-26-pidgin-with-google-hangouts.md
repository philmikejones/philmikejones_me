---
title: Pidgin with Google Hangouts
date: 2015-08-26
author: philmikejones
categories:
  - Research Methods
tags:
  - Google
  - Hangouts
  - Pidgin
  - Two-factor authentication
---

I'm old-fashioned and like a desktop client for online messaging so I use Pidgin on my Ubuntu machines. To install Pidgin:

<pre>sudo apt-get install pidgin</pre>

Then open the Pidgin client. Add an account and select XMPP protocol. Your username is the bit before the &#8216;@' in your email address. Domain is the bit after the &#8216;@'. If you're using a personal Gmail account this will be gmail.com; if you're using a Google Apps email address (for example if your company use Gmail to handle it's mail) it will be whatever's after the @ in your email address. Resource can be left blank.

If you use two-factor authentication to sign in to your Google account (and you really should!) you will need an app-specific password to log in to Pidgin; don't use your normal Gmail password. If this is you, go to [App passwords](https://security.google.com/settings/security/apppasswords) and create a new password to Pidgin. Use this to log in. If you don't use two-factor authentication use your normal password.

Before you save go to Advanced tab. You need to select &#8216;Connection security: Require encryption' and Connect port: 5222. If this doesn't work you can try &#8216;Connection security: use old-style SSL' and Connect port: 5223. Both seem to work but I assume the old-style SSL is less secure. Finally, in Connect server enter talk.google.com. Press Save and connect.

Thanks to @<cite class="fn">mpekas</cite> for the tip about port configurations.