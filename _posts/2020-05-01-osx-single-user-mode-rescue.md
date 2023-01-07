---
layout: page
title: OS X Single User Mode Rescue
permalink: /wiki/osx-single-user-mode-rescue
tag: misc
---

## OS X Single User Mode Rescue

The other day when I was using my Macbook Pro, it all of a sudden froze up on me.  As in many cases when computers act up, I tried turning it off and on again.  Unfortunately each time I tried to boot, the progress bar would make it 3/4's of the way across the screen and then the power would go off.  Since it had been a couple weeks since I last backed up my files, I was worried that I was going to lose some of my recent coding progress.  That's when I found to about single user mode built into OS X.

###  How to Use Single User Mode
Launch into Safe Mode
  * Shut down the computer
  * Press the power button
  * As soon as the grey screen shows, press and hold the command+S keys

Load the following system libraries
  * cd /System/Library/LaunchDaemons
  * launchctl load com.apple.kextd.plist
  * launchctl load notified.plist
  * launchctl load com.apple.configd.plist

Start the networking
  * plug-in the RJ49 ethernet cable
  * type ifconfig to see if an IP has been assigned
  * sftp or ftp to a machine on your local network to receive the backup files


