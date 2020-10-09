---
layout: page
title: Notes
---

<ul>
  {% for post in site.posts %}
    <li itemscope>
       <a href="{{ site.github.url }}{{ post.url }}">{{ post.title }}</a>
    </li>

  {% endfor %}
</ul>
