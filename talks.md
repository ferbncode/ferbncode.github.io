---
layout: default
title: Talks I loved!
---
### My talks


<div class="self-talk-row">
{% for talk in site.selftalks %}
    <div class="self-talk-video-column">
        <div class="if_wrapper">
            <div class="h_iframe">
                <img class="ratio" src="http://placehold.it/9x9" />
                <iframe src="https://www.youtube.com/embed/wPxn7lBSUnQ" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
            </div>
        </div>
    </div>
    <div class="self-talk-details-column">
      <div class="talk_title"><strong>{{ talk.title }}</strong></div>
      <div>{{ talk.speaker }}</div>

      <p>
        {{ talk.content | strip_html | truncate: 350 }} <a href="{{ site.github.url }}{{ talk.url }}">Read more</a>
      </p>
      <div>
        <span><a href="{{ talk.slide-link }}" class="watch_slide_text_div">Slides</a>/
        <a href="{{ talk.video-link }}" class="watch_slide_text_div">Watch it here!</a></span>
      </div>
    </div>
{% endfor %}
</div>

<br/>

### Learning from the great talks on the Internet
<!-- <div style="font-size:17px;line-height: 0rem; word-wrap: break-word"> -->
<p style="font-size:20px">There are a lot of awesome talks on the web and I love to learn from them. Keeping my notes and learnings from the wonderful talks here :)</p>
<!-- </div> -->
<div class="other-talk-row">
{% for talk in site.talks %}
    {% assign mod = forloop.index0 | modulo: 2 %}
    <div class="other-talk-details-column">
    {% if mod == 0 %}
        <div class="other-talk-details-column-div" style="background-color:#FFF ">
    {% else %}
        <div class="other-talk-details-column-div" style="background-color:#FFF;">
    {% endif %}
      <div class="talk_title"><strong>{{ talk.title }}</strong></div>
      <div>{{ talk.speaker }}</div>
      <div>
        <span><a href="{{ talk.video-link }}" class="watch_slide_text_div">Link to the talk</a></span>
        {% if talk.slide-link %}
        /<a href="{{ talk.slide-link }}" class="watch_slide_text_div">slides!</a>
        {% endif %}
      </div>
      <p>
        <strong>My notes:</strong> {{ talk.content | strip_html | truncate: 200 }} <a href="{{ site.github.url }}{{ talk.url }}">Read more</a>
      </p>
    </div>
    </div>
{% endfor %}
</div>




<!-- a href="{{ site.url }}{{ site.baseurl }}{{ page.url }}">{{ page.title }} -->
