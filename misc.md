---
layout: page
title: Misc
permalink: /wiki/misc
---

## Misc Content
{% for tag in site.tags %}
{% if tag[0] == "misc" %}
  <ul class="list-group">
    {% for post in tag[1] %}
      <li class="list-group-item list-group-item-primary"><a class="text-primary" href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}
