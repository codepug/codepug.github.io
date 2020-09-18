---
layout: home
title: Games
permalink: /wiki/games
---

## CodePug Games: Download Them Today
Feel free to explore some of my experimental games below. The resources below include Zune HD games, java applets, downloadable Win32 executables, images, and interesting links. As unique pug contributions to the Internet are created, I hope to post a selection of them here.

{% for tag in site.tags %}
  {% if tag[0] == "games" %}
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}

### iOS Apps on the App Store on iTunes
  * [PineSweeper](https://itunes.apple.com/us/app/pinesweeper/id572200964?mt=8)
  * [Chinese Card Match](https://itunes.apple.com/us/app/chinese-card-match/id581446042?mt=8)

### Android Apps on Play Store
  * [PineSweeper](https://play.google.com/store/apps/details?id=com.codepug.pinesweeper&hl=en)
  * [Chinese Card Match](https://play.google.com/store/apps/details?id=com.codepug.memory&hl=en)
  * [King of GUID - UUID Generator](https://play.google.com/store/apps/details?id=com.codepug.guid&hl=en) - Over 1,100 installs