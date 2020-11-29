---
layout: post
title: Raspberry Pi - Setting Up a Browser Based Kiosk
permalink: /wiki/raspberry-pi-windows-sharing
tag: pi
---

## Raspberry Pi - Setting Up a Browser Based Kiosk

The Raspberry Pi computer makes an excellent web-based kiosk for displaying information off of a website. Web HTML content can be either stored locally on the device or the device can be connected to the Internet.  If you plan on connecting it to the Internet, then you will need either an RJ45 ethernet cable or a WIFI adapter to connect to your home network.  

The following materials will be needed:
  * Raspberry Pi
  * HDMI cable
  * RJ45 ethernet cable (optionally WIFI adapter)
  * SD card with at least 2Gb in size

After installing the latest version of Raspbian onto the Pi, then you will want to run the following commands.
    sudo apt-get upgrade -y
    sudo rpi-update
    sudo raspi-config
    sudo apt-get install mini-httpd
    chmod -R 777 /usr/share/mini-httpd/html

Next we'll want to prevent the screen from going into sleep.
    sudo nano /etc/lightdm/lightdm.conf adding the following under the [SeatDefaults] section: xserver-command=X -s 0 dpms

Hide the cursor when it's not being used with the following:
   sudo apt-get install unclutter

Next you will want to remotely connect to your Raspberry Pi using SSH.  After logging in you will want to disable the full GUI interface process and have it run the Midori web browser in fullscreen mode.  
    sudo nano /etc/xdg/lxsession/LXDE/autostart 
Comment out everything that is there by prepending a # character and add the following lines.
    @xset s off
    @xset -dpms
    @xset s noblank
    @midori -e Fullscreen -a http://www.codepug.com

Optionally, you may need to take some steps to enable sound through the HDMI port.  This can be done by doing the following:
    sudo nano /boot/config.txt
    Add hdmi_drive=2 and press Control-X and enter to save
    Connect the Pi to your display ensuring the input device is set correctly and reboot your Pi
    
Instead of pointing your kiosk to an external site, you can also install a local web server and simply point it directly to the Pi itself.  This is particularly handy if your Raspberry Pi does not have a persistent connection to the Internet.
    sudo apt-get install mini-httpd
    nano /etc/mini-httpd.conf
    ln -s /usr/share/mini-httpd/html www
    sudo chown pi -R /usr/share/mini-httpd/
    sudo nano /etc/rc.local # and add sudo mini-httpd -d /usr/share/mini-httpd/html/ &
    
To make things even fancier, you can have an external program interact with the kiosk's displayed webpage using the xdotool.
    sudo apt-get install xdotool
    export DISPLAY=:0.0
    xdotool key "ctrl+s"
    xdotool key "Escape"