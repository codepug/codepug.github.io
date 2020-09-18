---
layout: home
title: Media
permalink: /wiki/media
---

## Artistic Media

{% for tag in site.tags %}
{% if tag[0] == "media" %}
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}