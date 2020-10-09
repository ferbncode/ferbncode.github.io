---
layout: page
title: Sketches
---

<ul>
  {% for post in site.posts %}

    {% if post.p_tags contains 'diagram' %}
    <li itemscope>
      <a href="{{ site.github.url }}{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endif %}

  {% endfor %}
</ul>
