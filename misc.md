---
layout: home
title: Misc
permalink: /wiki/misc
---

## Misc Content
{% for tag in site.tags %}
{% if tag[0] == "misc" %}
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}