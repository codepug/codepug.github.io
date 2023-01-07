---
layout: page
title: Raspberry Pi - Intercom
permalink: /wiki/raspberry-pi-intercom
tag: pi
---

## Raspberry Pi - Intercom
A wireless, configurable software driven intercom for the house sounds great.  Here on this page, I've listed out a number of the steps that I took to transform my Raspberry Pi into an intercom where I could communicate from my PC to the PI in real-time.  Unfortunately, the USB audio card attached to my PI that provides a jack to connect a mic, did not provide very good quality back to the PC.  I tried to modify the sampling rate, but didn’t have much luck.  Here are the setup steps and commands that I used.

  * sudo raspi-config
  * sudo rpi-update
  * sudo apt-get install lynx screen festival ffmpeg libjpeg8-dev imagemagick subversion libjpeg8-dev mplayer libasound2-dev bison python-dev python2.7-dev python python-alsaaudio linphone python-dev python-rpi.gpio tightvncserver
  * tightvncpasswd
  * tightvncserver
  * #Connect to VNC server from the other machine.  Type mumble.  Choose the ALSA audio card instead of Pulse.  
  * linphonec -C
  * sudo apt-get update
  * sudo dpkg-reconfigure mumble-server
  * sudo modprobe snd_bcm2835
