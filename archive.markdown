---
layout: default
title: Archive
permalink: /archive/
---

# All Posts

<ul class="archive">
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}" class="title">{{ post.title }}</a> <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
    </li>
  {% endfor %}
</ul>
