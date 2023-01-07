---
layout: page
title: Raspberry Pi - Static Dynamic IP
permalink: /wiki/raspberry-pi-static-dynamic-ip
tag: pi
---

## Raspberry Pi Static Dynamic IP
If you have a dynamic IP at home and write access to a web site with a static IP, you can create for yourself a static address capable of redirecting to your dynamic home network IP.  

Your Raspberry Pi system can be configured to send its current URL over to a PHP script running on your static IP web site at regular intervals.  I was able to configure this using cron.

At the command prompt type 'sudo crontab -e' and enter a scheduled command similar to the following using the default editor:
```
0 7,9,11,1,3,5,8 * * * curl --url "http://codepug.com/saveFeedback?name=IP_CHECK3&saveFeedback=y" >/dev/null 2>&1
48 22 * * * curl --url "http://codepug.com/saveFeedback?name=IP_CHECK3&saveFeedback=y" >/dev/null 2>&1
```

To check cron's updated schedule you can type the '/etc/init.d/cron status'
