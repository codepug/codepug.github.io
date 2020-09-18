---
layout: home
title: CodePug Web Server for the Zune
permalink: /wiki/zune-web-server
tag: misc
---

## CodePug Web Server for the Zune

Thanks to the new functionalities opened up by the OpenZDK development environment (http://zunedevwiki.org/wiki/) network connectivity can now be supported by custom Zune HD applications. Now you can be the first on your block to carry around your own web server.

Released on May 1st, 2010, the CodePug Web Server is the first web server for the Zune. The source code has been made available below in hopes that it will aid in maturing the homebrew community of Zune coders. There is also a list of upcoming planned features for improving this Zune web server even further.

Right now to use the web server, it will first need to be downloaded and installed. After uncompressing the Zip file below, locate the deploykit.exe file to install the application on your Zune HD. Next connect to your wireless network on your Zune by using the Zune's pre-existent Internet browser. After connecting to a page, close the browser by pressing the button under the screen. Next, go to the apps menu, find the "CodePug WebServer" and click on it. The web server should then start up and show your IP on the screen. Now within the same network, open up a web browser on another device and connect to the URL showing on the Zune's screen. If everything works, you should see a web page similar to this.

License: Creative Commons-Zero (public domain)

![Zune Web Server](/assets/images/zune-web-server.png)

### Current Features

  * Supports multi-threading
  * Sends list of files and folders in the root directory
  * Source code available for customization
  * Provides the http: address and IP needed to connect

![Zune Web Server Browser](/assets/images/zune-web-server-browse.jpg)

### Enhancements Not Included At This Time

  * Automatically connect to a network and obtain an IP
  * Directory navigation
  * Zune HD registry exploration
  * Sharing controls (security and directory configuration)
  * Allow for the downloading of binary files
  * Support for custom static content
  * Ability to disable power saving mode

### Downloads

The content and/or source code for the "CodePug Web Server for the Zune" application has been made available as a reference below. It is our hope that it will be an encouragement to others learning to program other freely available applications.

^ Filename	^ Vers.	 ^ File type	^ Size	^ Comments    ^
|[[http://localhost/downloads/Deploy%20CodePug%20WebServer.zip|CodePug WebServer for the Zune HD]]|	1.0a|	Zune App Installer|	167k|	Run deploykit.exe|
|[[http://localhost/downloads/Source%20CodePug%20WebServer.zip|CodePug WebServer Source]]|	1.0a	| C++ Source Code	| 2870k |	Zipped Project Folder|

<html>
        <span style="font-size: 8pt;">
                Note: This code has not been fully tested. Please do not run this unless you acknowledge that you assume all risks associated with its operation.
        </span>
        </html>