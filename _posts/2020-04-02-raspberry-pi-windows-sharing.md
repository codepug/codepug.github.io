---
layout: home
title: Raspberry Pi - Windows Sharing
permalink: /wiki/raspberry-pi-windows-sharing
tag: pi
---

## Raspberry Pi - Windows Sharing
The Samba open source software provides a convenient mechanism for sharing files across your computers and Raspberry PI machines.  Outlined below are various commands and configurations options that I used to enable the sharing of my home folder to other machines on my network in read/write mode.  Please use caution when following any of the steps below as they will make your files accessible for yourself (or others) to access from your machine.

  * sudo apt-get update
  * sudo apt-get install samba samba-common-bin
  * sudo smbpasswd -a pi
  * sudo nano /etc/samba/smb.conf

### Configuration Content Added to smb.conf
<code>
[pihome]
   comment= Pi Home
   path=/home/pi
   browseable=Yes
   writeable=Yes
   only guest=no
   create mask=0777
   directory mask=0777
   public=no
</code>
