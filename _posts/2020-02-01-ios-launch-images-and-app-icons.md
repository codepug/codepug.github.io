---
layout: home
title: iOS Development - Generating Launch Images and App Icons
permalink: /wiki/ios-launch-images-and-app-icons
tag: programming
---

## iOS Development - Generating Launch Images and App Icons
If you are using Xcode to develop an iOS application, one of the more tedious development steps is creating the application icons and launch images for the various resolutions of iOS devices out there today.  If you are Target SDK and your Base SDK span a number of iOS versions, then the number of required images at varying resolutions will also be somewhat large.  To address this, I have put together a script that I use to call the ImageMagick library to automatically generate launch images and application icons of the correct sizes that I will need. 

### Requirements
Here is a list of steps that I used to install the required libraries for OS X Yosemite.  Instead of using brew another option would be to use Mac Ports (http://guide.macports.org/#installing.xcode)
  * Install brew 
  * sudo ln -s /usr/local/Libary/ruby /usr/bin/ruby
  * sudo nano /usr/local/Library/brew.rb
  * Added #!/System/Library/Frameworks/Ruby.framework/Versions/Current/usr/bin/ruby -W0
  * brew install imagemagick
  * xcode-select --install
  * Selected an image to be centered within the generated launch images 
![iOS Launch Imags](/assets/images/codepug-launch-image.png)

### App Icon Script
This script can be called passing a large icon to generate square icons of the necessary sizes.
<code>
#!/bin/bash

mkdir -p generated
SOURCE_ICON="$1"
listOfSizes="29 58 87 80 57 114 120 180 40 50 100 72 144 76 152"

for imageSize in $listOfSizes
do
  sips -Z ${imageSize} --out generated/icon${imageSize}.png "${SOURCE_ICON}"
done
</code>

### Launch Image Script
This script can be called to generate launch images of the required sizes.
<code>
#!/bin/bash
# @Author: CodePug, C. 2014
# usage:  generate-iOS-app-launch.sh sourceImage-1024x1024.png

SOURCE_ICON="$1"
BG_COLOR="#ffffff"
CMD="../${SOURCE_ICON} -resize 100x100^ -gravity center -borderColor ${BG_COLOR} -border 1200x1200"

mkdir -p generated
cd generated

echo -n Generating Images:
convert ${CMD} -crop 1242x2208+0+0 +repage ios8P_PH55RetHD.png
convert ${CMD} -crop 750x1334+0+0 +repage ios8P_PH47RetHD.png
convert ${CMD} -crop 2208x1242+0+0 +repage ios8L_PH55RetHD.png
convert ${CMD} -crop 768x1024+0+0 +repage ios7P_PADx1.png
convert ${CMD} -crop 1536x2048+0+0 +repage ios7P_PADx2.png
convert ${CMD} -crop 1024x768+0+0 +repage ios7L_PADx1.png
convert ${CMD} -crop 2048x1536+0+0 +repage ios7L_PADx2.png
convert ${CMD} -crop 640x960+0+0 +repage ios7P_PHx2.png
convert ${CMD} -crop 640x1136+0+0 +repage ios7L_PHx2Ret.png
convert ${CMD} -crop 320x480+0+0 +repage ios5P_PHx1.png
convert ${CMD} -crop 640x960+0+0 +repage ios5P_PHx2.png
convert ${CMD} -crop 640x1136+0+0 +repage ios5P_PHRet4.png
convert ${CMD} -crop 768x1024+0+0 +repage ios5P_PADx1NoBar.png
convert ${CMD} -crop 1536x2048+0+0 +repage ios5P_PADx2NoBar.png
convert ${CMD} -crop 768x1004+0+0 +repage ios5P_PADx1.png
convert ${CMD} -crop 1536x2008+0+0 +repage ios5P_PADx2.png
convert ${CMD} -crop 1024x768+0+0 +repage ios5L_PADx1.png
convert ${CMD} -crop 2048x1536+0+0 +repage ios5L_PADx2.png
convert ${CMD} -crop 1024x748+0+0 +repage ios5L_PADx1NoBar.png
convert ${CMD} -crop 2048x1496+0+0 +repage ios5L_PADx2NoBar.png
echo Done.

cd  ..
exit
</code>