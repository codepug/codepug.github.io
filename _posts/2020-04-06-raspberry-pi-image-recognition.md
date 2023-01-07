---
layout: page
title: Raspberry Pi - Image Recognition Initial Setup
permalink: /wiki/raspberry-pi-image-recognition
tag: pi
---

## Raspberry Pi Image Recognition Initial Setup

The Raspberry Pi system provides a low power solution with enough CPU to perform realtime image recognition capabilities.  For this I used a creative camera with **UVC** support so that I didn't have to worry about compiling any special drivers into Raspbian.  
On the software side, some starting steps to take may include installing a video capture software such as mjpg_streamer.  First, grab some of the dependent utility and image processing libraries.

     sudo apt-get update
     sudo apt-get install libjpeg8-dev imagemagick
     sudo apt-get install subversion

You will also need to download the source and compile it for mjpg_streamer.
     cd ~
     mkdir tmp
     cd tmp
     svn co https://svn.code.sf.net/p/mjpg-streamer/code
     cd code/mjpg-streamer
     make
     sudo make install
After mjpg_streamer is built, then you can run it using a command similar to the following:
     ./mjpg_streamer -i "./input_uvc.so -n -f 15 -r 240x160" -o "./output_http.so -n -w ./www"
The above command assumes that you have changed to the directory containing mjpg_streamer and the relevant *.so files.

The resolution can be changed from 240x160 to higher values depending on what your camera supports.  I found that the lower resolution images were much more responsive in terms of any analysis that I needed to do on video.  These numbers may need to vary depending on the work load placed on your Raspberry Pi and network interface bandwidth.

To automatically run mjpg_streamer on system startup, you can type '**sudo nano /etc/rc.local**' and add something similar to:
     /usr/local/bin/mjpg_streamer -i "/usr/local/lib/input_uvc.so -n -f 15 -r 240x160" -o "/usr/local/lib/output_http.so -n -w /usr/local/www" &

One can then use the default or create a custom page to display the video.  I used the following which I placed at /usr/local/www/index.html:
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Live Feed</title>
<style>
body {
    background-color: #ccc;
}
img {
    border: solid 1px #000;
}
</style>
</head>
<script type="text/javascript">

var imageNr = 0; // Serial number of current image
var finished = new Array(); // References to img objects which have finished downloading
var paused = false;

function createImageLayer() {
  var img = new Image();
  img.style.position = "absolute";
  img.style.zIndex = -1;
  img.onload = imageOnload;
  img.onclick = imageOnclick;
  img.style.width='500px';
  img.src = "/?action=snapshot&n=" + (++imageNr);
  var webcam = document.getElementById("webcam");
  webcam.insertBefore(img, webcam.firstChild);
}

// Two layers are always present (except at the very beginning), to avoid flicker
function imageOnload() {
  this.style.zIndex = imageNr; // Image finished, bring to front!
  while (1 < finished.length) {
    var del = finished.shift(); // Delete old image(s) from document
    del.parentNode.removeChild(del);
  }
  finished.push(this);
  if (!paused) createImageLayer();
  finished.push(this);
  if (!paused) createImageLayer();
}

function imageOnclick() { // Clicking on the image will pause the stream
  paused = !paused;
  if (!paused) createImageLayer();
}

</script>
<body onload="createImageLayer();">
<div id="webcam"><noscript><img src="/?action=snapshot" /></noscript></div>

</body>
</html>
```

One can then use a computer vision analysis package such as OpenCV from another computer and process images streamed from the Raspberry Pi by connecting to the Raspberry Pi's assigned IP address.