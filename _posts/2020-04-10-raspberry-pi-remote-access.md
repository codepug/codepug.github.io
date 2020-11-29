---
layout: post
title: Raspberry Pi - Accessing Remotely
permalink: /wiki/raspberry-pi-remote-access
tag: pi
---

## Raspberry Pi - Accessing Remotely
The Raspberry Pi computer can be accessed remotely from another computer with a few modifications.  This is especially handy if you plan to use it without an external monitor attached.

Here you can do this by installing the VNC server onto your system.
    sudo apt-get install tightvncserver
    tightvncserver
    A session can be started with vncserver :1 -geometry 1024x728 -depth 32

Adjusting the depth to a lower value from 32 such as 16, will help increase responsiveness and bandwidth consumption.
Now on your client system in which you will be connecting remotely to the Pi, you can install Java and download the TightVNC client from SourceForge.

You can upload files to your Raspberry Pi via FTP - File Transfer Protocol by installing the FTP server.
    sudo apt-get install ftp

Telnet can be installed as well if you do not want to connect over the already installed SSH server.
    sudo apt-get install telnets

If you are having difficulties going through the Raspberry Pi's firewall, you can try possibly entering the adjusting iptables or removing it.  The following provides some example parameters that can be used.
```
    iptables -F 
    iptables -X 
    iptables -t nat -F 
    iptables -t nat -X 
    iptables -t mangle -F 
    iptables -t mangle -X 
    iptables -P INPUT ACCEPT 
    iptables -P OUTPUT ACCEPT iptables -P FORWARD ACCEPT
    sudo apt-get remove --purge iptables
```

Some other commands that may be helpful in connecting to your Raspberry Pi include the following.
```
    sudo /etc/init.d/ssh status
    sudo /etc/init.d/ssh status
    vncserver
    cd /home/pi/.vnc
    top
    tailf
    netstat
    ifconfig
```