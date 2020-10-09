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

<!-- a href="{{ site.url }}{{ site.baseurl }}{{ page.url }}">{{ page.title }} -->
