---
title: Configure ssh server with encrypted home directory
date: 2015-07-17
author: philmikejones
categories:
  - Code
tags:
  - encrypted home
  - ssh
  - ssh-server
---

The following instructions are to set up an ssh server on Ubuntu linux with an encrypted home directory. Throughout <tt>username</tt> refers to an actual username like <tt>phil</tt>.

Install OpenSSH server:

<pre class="brush: bash; title: ; notranslate" title="">sudo apt-get install openssh-server</pre>

Configure <tt>sshd_config</tt> (NOT <tt>ssh_config</tt>, note the <tt>d</tt>) to initially accept password logins, after creating a backup:

<pre class="brush: bash; title: ; notranslate" title="">sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.factory-defaults
sudo chmod a-w /etc/ssh/sshd_config.factory-defaults
sudo gedit /etc/ssh/sshd_config
</pre>

Change the line <tt>#PasswordAuthentication yes</tt> to read <tt>PasswordAuthentication yes</tt> (i.e. remove the #) and only allow certain users:

<pre class="brush: bash; title: ; notranslate" title="">PasswordAuthentication yes
AllowUsers username</pre>

Finally tell the configuration file to look in <tt>/etc/ssh/username/authorized_keys</tt> for client keys. The default is to look in <tt>~/.ssh/</tt> which is no good because this is encrypted until you've logged in!

<pre class="brush: bash; title: ; notranslate" title="">AuthorizedKeysFile    /etc/ssh/%u/authorized_keys</pre>

Restart the ssh server with:

<pre class="brush: bash; title: ; notranslate" title="">sudo service ssh restart</pre>

Next create the authorized_keys file and give it the appropriate permissions:

<pre class="brush: bash; title: ; notranslate" title="">sudo mkdir /etc/ssh/username/
sudo chown username /etc/ssh/username
sudo chmod 755 /etc/ssh/username
sudo touch /etc/ssh/username/authorized_keys
sudo chown username /etc/ssh/username/authorized_keys
sudo chmod 644 /etc/ssh/username/authorized_keys</pre>

Then copy the client's public key to authorized_keys. The easiest way to do that is to ssh in to the server (which is why we allowed password logins earlier) and do it from there. So from the client:

<pre class="brush: bash; title: ; notranslate" title="">nano ~/.ssh/id_rsa.pub</pre>

Copy the key to the clipboard then:

<pre class="brush: bash; title: ; notranslate" title="">ssh username.host.tld</pre>

Enter log in password when prompted, then:

<pre class="brush: bash; title: ; notranslate" title="">nano /etc/ssh/username/authorized_keys  # Paste the key here and save</pre>

Then logout:

<pre class="brush: bash; title: ; notranslate" title="">logout</pre>

Disable password logins from <tt>/etc/ssh/sshd_config</tt> and restart the ssh server (<tt>sudo service ssh restart</tt> from the server). Log in is now done using the ssh keys and without prompting for a password. The client will prompt to see if the public key fingerprint sent from the server is correct and to add it to the white list. Check it's right by running <tt>ssh-keygen -l -f /etc/ssh/ssh_host_rsa_key</tt> on the server.

## Sources:

- <https://help.ubuntu.com/community/SSH/OpenSSH/Keys>
- <https://help.ubuntu.com/community/SSH/OpenSSH/Configuring>
- <http://stackoverflow.com/questions/14301519/how-to-copy-pub-file-to-ssh-authorized-key>
- <http://ubuntuforums.org/showthread.php?t=789301>