

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


