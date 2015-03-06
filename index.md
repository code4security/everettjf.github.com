---
layout: page
title: dump my brain
tagline: dump my brain , some note
---
{% include JB/setup %}

<pre>
小和尚问老和尚，年轻时你做什么？老和尚说：挑水、砍柴、做饭。
小和尚又问老和尚，得道后你又做什么？老和尚说：挑水、砍柴、做饭。
小和尚说，有什么区别呢？
老和尚说：

年轻时，我挑水的时候想着砍柴，砍柴时想着做饭。
而现在，我挑水时只想挑水，砍柴时只想砍柴，做饭时只想做饭。
</pre>

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date: '%Y' }}-{{ post.date | date: '%m' }}-{{ post.date | date: '%d' }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

---
