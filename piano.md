---
layout: default
title: Piano practice
---
### My Piano practice

Atempt to accelerate my piano practice by tracking progress publicly - practicing consistently, sharing progress and easily getting feedback. 

<div class="other-talk-row">
{% for task in site.piano %}
    {% assign mod = forloop.index0 | modulo: 2 %}
    <div class="other-talk-details-column">
    {% if mod == 0 %}
        <div class="other-talk-details-column-div" style="background-color:#F5FCFE;">
    {% else %}
        <div class="other-talk-details-column-div" style="background-color:#F4F4F4">
    {% endif %}
      <div class="talk_title"><strong>{{ task.title }}</strong></div>
      <div>Last updated: {{ task.last_updated }}</div>
      <p>
        <a href="{{ site.github.url }}{{ task.url }}">See more</a>
      </p>
    </div>
    </div>
{% endfor %}
</div>
