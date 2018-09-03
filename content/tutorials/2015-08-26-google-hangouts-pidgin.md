---
title: "Google Hangouts with Pidgin"
date: 2015-08-26
author: "Phil Mike Jones"
categories: ["tutorials"]
tags: ["google-hangouts", "instant-messaging", "pidgin", "Ubuntu"]
---

To set up Google Hangouts with Pidgin, first install it:

```bash
sudo apt install pidgin
```

<!--more-->

Then open the Pidgin client.

1. Add an account and select XMPP protocol. 
1. Your username is the bit before the '@' in your email address.
1. Domain is the bit after the '@'. If you're using a personal Gmail account this will be gmail.com; if you're using a Google Apps email address (for example if your company use Gmail to handle it's mail) it will be whatever's after the @ in your email address.
1. Resource can be left blank.

If you use two--factor authentication to sign in to your Google account (and you really should!) you will need an app--specific password to log in to Pidgin; don't use your normal Gmail password.
If this is you, go to [App passwords](https://security.google.com/settings/security/apppasswords) and create a new password to Pidgin.
Use this to log in.
If you don't use two--factor authentication use your normal password.

Before you save go to Advanced tab.
You need to select 'Connection security: Require encryption' and Connect port: 5222.
If this doesn't work you can try 'Connection security: use old-style SSL' and Connect port: 5223.
Both seem to work but I assume the old--style SSL is less secure.
Finally, in Connect server enter talk.google.com.
Press Save and connect.

Thanks to @mpekas for the tip about port configurations.
