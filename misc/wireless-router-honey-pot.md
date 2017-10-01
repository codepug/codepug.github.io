---
layout: home
title: Create a Honey Pot Using a GT704WG Wireless Router
permalink: /wiki/wireless-router-honey-pot
---

## Create a Honey Pot Using a GT704WG Wireless Router

After having to chase some people down the street several weeks in a row for trying to crack my wireless WEP key from their cars, it occurred to me that instead of viewing the popularity of my wireless network as a nuisance it could actually be an opportunity. Recently, I was fortunate enough to acquire a spare wireless GT704WG router. After tinkering around with it for a while, I found that wireless routers provide an excellent platform for delivering personalized content to would be hackers, neighbors, and anyone in the area connecting to available networks. This page provides a list of steps that I have taken to create a captive portal (a.k.a. honeypot) from my GT704WG wireless router.

![GT704WG Router](gt704wgRouter.jpg)

=== Steps ====
  * Download a telnet client such as <a href="http://ftp.chiark.greenend.org.uk/%7Esgtatham/putty" target="0">PuTTYtel</a>
  * Telnet to your router using the IP: 192.168.1.1
  * Run something similar to the following script at your own risk: 
<code>
#! /bin/sh
#
# Setup wireless captive portal
#
# Run at your own risk, toggle the power if run you need to restore
# @author www.CodePug.com

mkdir /var/www
mkdir /var/www/errors
# TODO: use wget to copy your index.html into the www and errors dir

# Redirect all TCP web traffic to your router''s own thttpd server
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 80

# Restart the web server using our var writable directory
kill `pidof thttpd`
/usr/sbin/thttpd -d /var/www

# Copy dproxy from the downloads section to /var
cd /var
wget http://www.codepug.com/downloads/dproxy

# Restart the proxy server using our proxy server below that always
# responds with the router''s address for all requests (192.168.1.1)
kill `pidof dproxy`;dproxy
</code>

### Useful Links
  * [Wireless Honeypot Countermeasures](http://www.securityfocus.com/infocus/1761)
  * [Original Router GPL Source Code](http://www.google.com/search?q=%61ctiontec+open+source&amp;btnI=I%27m+Feeling+Lucky)

### Downloads
The content and/or source code for the modified dproxy application has been made available as a reference below. It is our hope that it will be an encouragement to others learning to program freely available applications.

^ Filename	^ License	^ File type	^ Size	^
|[gt704wg-dproxySrc](http://www.codepug.com/downloads/gt704wg-dproxySrc.zip)	|GPL v2	|Compressed C Source	|40k	|

<html>
        <span style="font-size: 8pt;">
                Note: This code has not been fully tested. Please do not run this unless you acknowledge that you assume all risks associated with its operation.
        </span>
        </html>
