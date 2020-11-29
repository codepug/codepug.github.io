---
layout: page
title: Media
permalink: /wiki/media
---

## Artistic Media

{% for tag in site.tags %}
{% if tag[0] == "media" %}
  <ul class="list-group">
    {% for post in tag[1] %}
      <li class="list-group-item list-group-item-primary"><a class="text-primary" href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}