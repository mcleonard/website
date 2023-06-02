---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

title: matatat.org - Deliberately practiced
layout: default
---
<ul class="blog-roll">
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.content }}
      <span class="post-date">Posted on {{ post.date | date: "%b %d, %Y" }}</span>
    </li>
    <hr>
  {% endfor %}
</ul>
<a href="/archive">Older posts</a>