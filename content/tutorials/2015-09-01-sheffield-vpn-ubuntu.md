---
title: "Sheffield VPN in Ubuntu"
date: 2015-09-01
author: "Phil Mike Jones"
categories: ["tutorials"]
tags: ["vpn", "vpnc", "ubuntu", "cisco-vpn"]
---

With Ubuntu Xenial the VPNC GUI no longer seems to work but I've managed to piece together the following instructions based on [Using vpnc as a Command Line VPN Client](https://www.lullabot.com/articles/using-vpnc-as-a-command-line-vpn-client).

<!--more-->

1. Open a terminal.
1. Install vpnc with `sudo apt install vpnc`
1. There's a default VPN connection template in `/etc/vpnc/default.conf` 
1. Make a copy of this template with `sudo cp /etc/vpnc/default.conf /etc/vpnc/shef.conf`
1. Edit this file with `sudo gedit /etc/vpnc/shef.conf` (or use whichever text editor you prefer)
1. Enter the following details, taken from https://www.sheffield.ac.uk/cics/vpn/linux

> IPSec gateway:  vpn.shef.ac.uk
> IPSec ID:       unishef
> IPSec secret:   unishef
> Xauth username: [uni-username]
> Xauth password: [remote-access-password]

You need to [set up a remote access password](https://sheffield.ac.uk/cics/password).

To connect, use `sudo vpnc shef`.
To disconnect, use `sudo vpnc-disconnect`.
