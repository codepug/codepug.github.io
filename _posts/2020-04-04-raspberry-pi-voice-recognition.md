---
layout: post
title: Raspberry Pi - Voice Recognition
permalink: /wiki/raspberry-pi-voice-recognition
tag: pi
---

## Raspberry Pi - Voice Recognition
The Raspberry Pi offers a nice embedded platform capable of providing near realtime voice recognition. 

In order to respond to recognized text, a voice synthesis engine can be used.  One can choose either a system running locally on the system such as festival or one that is executed remotely.  
For a local solution, one such option is a program called festival.

     sudo apt-get install festival
     echo "Testing this out" | festival -tts

For the following steps you will also want to get your sound working.  Make sure that you have a USB device attached that has a microphone in jack for this to work.  **Note**, not all USB sound card devices may be compatible.
    sudo apt-get install ffmpeg
    sudo modprobe snd_bcm2835
    sudo apt-get install alsa-tools alsa-oss flex zlib1g-dev libc-bin libc-dev-bin python-pexpect libasound2 libasound2-dev cvs

It maybe helpful to test out your ability to record and play back sounds before progressing to building out pocket-sphinx.
    arecord -d 10 -D plughw:1,0 test.wav
    aplay test.wav
Or even try streaming sound to another machine at <remoteip>
    arecord -D plughw:1,0 -f dat | ssh -C user@remoteip aplay -f dat

In order to get the speech recognition working, you will need an appropriate engine such as pocket-sphinx.
```
    sudo apt-get install mplayer
    sudo apt-get install libasound2-dev
    sudo apt-get install bison
    sudo apt-get install python-dev python2.7-dev python python-alsaaudio
    wget http://downloads.sourceforge.net/project/cmusphinx/sphinxbase/0.8/sphinxbase-0.8.tar.gz
    wget http://downloads.sourceforge.net/project/cmusphinx/pocketsphinx/0.8/pocketsphinx-0.8.tar.gz
```

Next change your directory into the sphinx base directory and type the following commands:
     ./configure --enable-fixed
     make
     sudo make install

Now change your directory into the pocket-sphinx directory and type the following commands:
    ./configure
    make
    sudo make install
    ./src/programs/pocketsphinx_continuous -samprate 48000 -nfft 2048 -adcdev hw:1,0

Custom dictionaries can be created for pocket-sphinx which greatly improve accuracy for command and control type applications.  They can be specified with the -dict and -lm parameters:
    ./src/programs/pocketsphinx_continuous -samprate 8000 -nfft 2048 -adcdev hw:1,0 -lm 2530.lm -dict 2530.dic