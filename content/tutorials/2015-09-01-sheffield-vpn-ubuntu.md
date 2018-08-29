---
title: Sheffield VPN in Ubuntu
date: 2015-09-01
author: philmikejones
categories:
  - PhD
tags:
  - cisco compatible vpn
  - ubuntu
  - vpn
  - vpnc
---

## Update 2016 &#8211; Ubuntu 16.04 Xenial

With Ubuntu Xenial the VPNC GUI no longer seems to work but I've managed to piece together the following instructions, based on [Using vpnc as a Command Line VPN Client](https://www.lullabot.com/articles/using-vpnc-as-a-command-line-vpn-client):

  1. Install vpnc with `sudo apt install vpnc`
  2. There's a default VPN connection template in `/etc/vpnc/default.conf` 
      1. Make a copy of this template with `sudo cp /etc/vpnc/default.conf /etc/vpnc/shef.conf`
  3. Edit this file with `sudo gedit /etc/vpnc/shef.conf` (or use whichever text editor you prefer)
  4. Enter the following details, taken from <https://www.sheffield.ac.uk/cics/vpn/linux>

    IPSec gateway vpn.shef.ac.uk
    IPSec ID unishef
    IPSec secret unishef
    Xauth username [uni-username]
    Xauth password [remote-access-password]

To connect, use `sudo vpnc shef`. To disconnect, use `sudo vpnc-disconnect`.

## Ubuntu 14.04 Trusty

By default in Ubuntu you need to install vpnc to connect to the University of Sheffield VPN. You can do this with:

<pre>sudo apt-get install network-manager-vpnc</pre>

You will need a Remote Access Password in order to connect. If you don't have one, you can [request a remote access password](https://sheffield.ac.uk/cics/password) from CICS. Note this is not your regular account password.

With vpnc installed, set up the VPN by:

  1. Open <tt>System Settings</tt> and click <tt>Network</tt>.
  2. Click the <tt>+</tt> to create a new service.
  3. From the Interface drop-down menu select <tt>VPN</tt>.
  4. A new menu for VPN Connection Type will appear. Select <tt>Cisco Compatible VPN (vpnc)</tt>.
  5. You can rename you VPN connection if you wish by editing the <tt>Connection Name</tt>.
  6. In the gateway field enter: <tt>vpn.shef.ac.uk</tt>
  7. In account name enter your University username.
  8. Change Always Ask for password to <tt>Saved</tt> in the drop-down list.
  9. Enter your Remote Access password in the <tt>User password</tt> field.
 10. Change Always Ask for Group password to <tt>Saved</tt> in the drop-down list.
 11. For both Group name and Group password enter <tt>Unishef</tt>
 12. Click <tt>Save</tt>.
 13. Your VPN is now set up. To use it left-click on the network icon in the status bar (two arrows facing up and down), select VPN connections and choose your new VPN.