---
layout: home
title: Raspberry Pi
permalink: /wiki/raspberry-pi
---

## Experiments in Raspberry Pi

Enhance your computing experience with these free fun and/or useful DIY projects for the Raspberry Pi. These electronic treats will start your tail wagging in no time.

{% for tag in site.tags %}
{% if tag[0] == "pi" %}
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}