---
layout: page
title: Notes
---

<ul class="posts">
  {% for post in site.conv %}
    <li itemscope>
      <a href="{{ site.github.url }}{{ post.url }}">{{ post.title }}</a>
    </li>

  {% endfor %}
</ul>
