---
layout: page
title: Games
permalink: /wiki/games
---

## CodePug Games: Download Them Today
Feel free to explore some of my experimental games below. As unique pug contributions to the Internet are created, I hope to post a selection of them here.

{% for tag in site.tags %}
  {% if tag[0] == "games" %}
  <ul class="list-group">
    {% for post in tag[1] %}
      <li class="list-group-item list-group-item-primary"><a class="text-primary" href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}
<br>
### iOS Apps on the App Store on iTunes
<ul class="list-group">
    <li class="list-group-item list-group-item-primary"><a class="text-primary" href="https://itunes.apple.com/us/app/pinesweeper/id572200964?mt=8">PineSweeper</a></li>
    <li class="list-group-item list-group-item-primary"><a class="text-primary" href="https://itunes.apple.com/us/app/chinese-card-match/id581446042?mt=8">Chinese Card Match</a></li>
</ul>
### Android Apps on Play Store
<ul class="list-group">
  <li class="list-group-item list-group-item-primary"><a class="text-primary" href="https://play.google.com/store/apps/details?id=com.codepug.pinesweeper&hl=en">PineSweeper</a></li>
  <li class="list-group-item list-group-item-primary"><a class="text-primary" href="https://play.google.com/store/apps/details?id=com.codepug.memory&hl=en">Chinese Card Match</a></li>
  <li class="list-group-item list-group-item-primary"><a class="text-primary" href="https://play.google.com/store/apps/details?id=com.codepug.guid&hl=en">King of GUID - UUID Generator - Over 1,100 installs</a></li>
  </ul>