---
layout: page
title: Raspberry Pi - Minecraft Server
permalink: /wiki/raspberry-pi-minecraft-server
tag: pi
---

## Raspberry Pi - Minecraft Server
The Raspberry Pi may be small, but it does have enough horse power to be leveraged as a limited minecraft server with decent performance.  Previously I had a Core 2 Duo Dell Studio Hybrid machine as my server, but the constant hum of the fan and size behind my TV had me looking for something better.  After some research and trial and error, I was able to setup an environment where I could play one of my favorite games online with some of my family members.  The steps that I took are listed below. 

  * Grab the latest version of Raspbian from the Raspberry Pi main site
  * Copy this onto an SD card (Steps for the Mac similar to the following, Use at your own Risk!)
  * Run 'df -h' to find the SD cards partition to unmount
  * Unmount the partition with sudo diskutil unmount /dev/disk{#}s1
  * Get the rdisk id to increase write speed (For example, /dev/disk{#}s1 => /dev/rdisk{#})
  * If you know the correct rdisk # only, copy the image to the SD card with a command similar to sudo dd bs=1m if=~/Downloads/2012-10-28-wheezy-raspbian/2012-12-16-wheezy-raspbian.img of=/dev/rdisk{#}
  * sudo diskutil eject /dev/rdisk{#}
  * Boot the PI using the SD card
  * sudo rasp-config
  * Disable desktop boot
  * Split video memory to 16Mb from 64Mb
  * Enable SSH
  * Set timezone, keyboard mappings, localizations, etc.
  * Enable overclock in 1000Mhz Turbo mode (Warning: may shorten the life of your PI)
  * sudo apt-get install lynx screen
  * mkdir ~/minecraft
  * cd ~/minecraft
  * sudo wget http://ci.md-5.net/job/Spigot/lastSuccessfulBuild/artifact/Spigot-Server/target/spigot.jar
  * sudo /opt/jdk1.8.0/bin/java -Xms256M -Xmx496M -jar /home/pi/spigot.jar nogui
  * Install world borders and run commands as op from within Minecraft client
  * Install http://dev.bukkit.org/bukkit-plugins/worldedit after modifying in Eclipse and recompiling with mvm to allow non-op users permissions
  * /wb shape rectangular
  * /wb setcorners 167 696 -231 -516
  * /wb trim
  * /wb fill
  * Edit server.properties to disable Nether and limit view distance from 10 to 4
  * Create a startup script to run the server
  * sudo nano /etc/rc.local (and call the startup.sh script that was created)

### Optional Steps
  * sudo /opt/jdk1.8.0/bin/java -Xms256M -Xmx496M -jar /home/pi/spigot.jar nogui
  * wget https://s3.amazonaws.com/Minecraft.Download/versions/1.7.4/minecraft_server.1.7.4.jar

