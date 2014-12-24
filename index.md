---
layout: page
title: 求知若饥，虚心若愚
tagline: Supporting tagline
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    <li><span>
{{ post.date | date: '%Y' }}
{{ post.date | date: '%m' }}
{{ post.date | date: '%d' }}
</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

