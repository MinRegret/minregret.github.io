---
layout: default
title: Videos
---

# Videos

{% for video in site.data.videos %}
<div class="video" markdown="1">
## {{ video.title }}
{{ video.description }}
<iframe width="560" height="315" src="{{ video.url }}" title="{{ video.title }}" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
{% endfor %}
