---
layout: page
title: Configuring the Linksys 1900AC Wireless Router with OpenWrt
permalink: /wiki/openwrt-linksys-1900ac
tag: misc
---

## Configuring the Linksys 1900AC Wireless Router with OpenWrt

The Linksys 1900AC router was released to the public as a great option for people who wanted to have a top notch router with 
support for open source firmware.  Now that some time has passed there is now alternative OpenWrt firmware (Chaos Calmer) available 
allowing a finer degree of customization then the factory default firmware.  

### Steps
After installing the latest [[https://downloads.openwrt.org/snapshots/trunk/mvebu/generic/
|firmware]] (at your own risk), you will then want to add the LUCI GUI interface.
```
opkg update
opkg install luci  (or luci-ssl for https access)
/etc/init.d/uhttpd start
/etc/init.d/uhttpd enable
```