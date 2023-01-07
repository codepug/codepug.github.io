---
layout: page
title: Netbook Minecraft Server
permalink: /wiki/netbook-minecraft-server
tag: misc
---

## Netbook Minecraft Server

Minecraft is certainly a fun game, and you know what is even more fun... having your own server.  
I recently decided to repurpose an old 1.6 Ghz Asus EEE Netbook that I had hanging around to function as my new Minecraft server.

### Steps
  * Installed Lubuntu linux which is nice lightweight linux installation
  * Installed Java 8, which seems to provide better performance for running minecraft than Java 7
```
# Downloaded the latest JDK 8 for 32-bit Linux
tar zxf jdk-8u40-linux-i586.tar.gz
sudo mkdir /opt/jdk
sudo mv jdk* /opt/jdk
sudo update-alternatives --install /usr/bin/java java /opt/jdk/jdk1.8.0_05/bin/java 100
sudo update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk1.8.0_05/bin/javac 100
```

  * Install helpful tools for video playback (when not using as Minecraft server
```
sudo apt-get-repository ppa:relan/exfat
sudo apt-get install rcconf exfat-utils ffmpeg vlc exfat rcconf
```

  * Disable GUI to save on memory and CPU
```sudo mv /etc/init/lightdm.conf /etc/init/lightdm.conf.bak```

  * Enable remote file transfer
```sudo apt-get install ftpd```

  * Enable remote administration
```sudo apt-get install openssh-server```

  * Disable sleep mode when closing the netbook lid
```sudo nano /etc/systemd/logind.conf
# Add HandleLidSwitch=ignore```

  * Install screen utility so can type screen -r later to get to minecraft console
```sudo apt-get install screen```

  * Enable start-up of minecraft server
```
mkdir /home/user/spigot
# Copy your startup script to it (I called mine mc.sh)
sudo nano /etc/rc.local
#exit 0
sudo -u user /home/user/spigot/mc.sh start
```

  * Disable wireless if using hard wired connection
```
sudo nano /etc/network/interfaces
# Remove to get wireless working
iface wlan0 inet manual
sudo service network-manager restart
```

  * On another system, grab the [[https://hub.spigotmc.org/jenkins/job/BuildTools/|BuiltTools.jar]] and build spigot-1.8.3.jar if you are not using the minecraft.jar from Mojang