---
layout: page
title: Programming
permalink: /wiki/programming
---
## Programming with CodePug

Learning new programming skills can be difficult. Fortunately, CodePug knows this and has put together a collection of examples that will help get you up to frisby catching speed in no time.

{% for tag in site.tags %}
{% if tag[0] == "programming" %}
  <ul class="list-group">
    {% for post in tag[1] %}
      <li class="list-group-item list-group-item-primary"><a class="text-primary" href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}