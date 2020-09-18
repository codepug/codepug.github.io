---
layout: home
title: Raspberry Pi - Gaming System
permalink: /wiki/raspberry-pi-gaming-system
tag: pi
---

## Raspberry Pi - Gaming System
The Raspberry Pi supports the ability to emulate game systems allowing you to play retro games.  Developers are still creating game files for 
Open Source games that play under these emulators and may be found via searches on the Internet.  This section only describes some aspects of how the Raspberry Pi may be configured to play these open source games.

First you will need to retrieve the source for the game emulator and try running it.
<code>
     sudo apt-get install -y git dialog
     git clone --depth=0 git://github.com/petrockblog/RetroPie-Setup.git
     sudo ./retropie_setup.sh
     emulationstation
</code>

Next you can optionally install the blue tooth software
<code>
    sudo apt-get install bluetooth
    /etc/init.d/bluetooth status
    hcitool dev
    hcitool scan
    sudo apt-get install python-cwiid
    wget https://sites.google.com/site/brianhensleyfiles/wiimotetest.py
    sudo python wiimotetest.py
    sudo apt-get install wminput
</code>

To get a bluetooth remote such as the Wiimote working correctly with the emulator, you may need to additionally configure the mapping of the buttons.  Type **sudo nano /home/pi/RetroPie/configs/nes/retroarch.cfg** and try adding something similar to 
     input_player1_select = c

Additionally, I found the following commands helpful in configure the proper mappings.
     cat /etc/udev/rules.d/
     cd /etc/udev/
     cat udev.conf
     sudo wminput -c buttons -d
     cat /sys/devices/system/cpu/cpufreq/
     nano buttons
     sudo wminput -c gamepad
     sudo wminput -d &
     xmodmap
     cd /usr/lib/cwiid/plugins
     ./retroarch-joyconfig
