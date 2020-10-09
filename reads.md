---
layout: default
title: Book Reads
---

<ul class="posts">
      <!-- <a href="{{ site.github.url }}{{ read.url }}">{{ read.title }}</a> -->
      <!-- {{ read.title }}<br/> -->
      <!-- {{ read.author }} -->
      <div class="row">
      {% for read in site.reads %}
        {% assign total_pages_float = read.total_pages | times: 1.0 %}
        {% assign read_percentage = read.read_pages | divided_by:total_pages_float  | times:100 %}
        <div class="column">
          <div class="img-container image is-256x256">
              <img src="../assets/images/{{read.img}}" />
          </div>

        <div id="progress">
        <div id="progress-bar">
          <div id="progress-bar-percentage" style="width: {{ read_percentage }}%">
            <span>{{read.read_pages}}/{{read.total_pages}}</span>
          </div>
        </div>
        </div>

        </div>
      {% endfor %}
      </div>
</ul>
<!-- a href="{{ site.url }}{{ site.baseurl }}{{ page.url }}">{{ page.title }} -->