---
layout: default
title: Home
---
# About

We develop algorithms and mathematical foundations for machine learning, optimization, and control. Our research spans online learning and decision-making, dynamical systems and sequence modeling, and the evaluation and alignment of increasingly capable AI systems.

Our work on AI evaluation and alignment is part of [Princeton AI Alignment and Safety (AIAS)](https://alignment.dais.princeton.edu/). We also collaborate with [Google DeepMind Princeton](https://sites.google.com/view/gbrainprinceton/home).

See our [research](/research/), meet the [team](/people/), or read our [blog](/blog/).

<div class="group-photo-pair">
<figure class="group-photo">
  <img src="{{ '/assets/img/princeton-superalignment-group.jpg' | relative_url }}" alt="Princeton SuperAlignment group gathered by the tiger statue on campus" width="1600" height="1030">
  <figcaption>Our Princeton SuperAlignment group.</figcaption>
</figure>
<figure class="group-photo">
  <img src="{{ '/assets/img/2019-summer-0.jpg' | relative_url }}" alt="Hazan research group in Summer 2019" loading="lazy">
  <figcaption>Summer 2019.</figcaption>
</figure>
</div>

## Research

- **[AI evaluation and alignment](/research/#ai-evaluation-and-alignment):** measuring capabilities beyond human expertise and designing incentives for reliable behavior.
- **[Online learning and optimization](/research/#online-learning-and-optimization):** regret minimization, adaptive optimization, and decision-making with bandit feedback.
- **[Control and sequence modeling](/research/#control-and-sequence-modeling):** online nonstochastic control, spectral methods, and efficient prediction over long sequences.

## From the blog

{% for post in site.posts limit:3 %}
- [{{ post.title }}]({{ post.url | relative_url }}) — {{ post.date | date: "%B %-d, %Y" }}
{% endfor %}
