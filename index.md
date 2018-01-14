---
layout: default
---

<div id="home" class="typo">
  <h1>所有文摘</h1>
  <ul class="posts">
    {% for post in site.posts %}
      <li><span>{{ post.date | date: "%Y.%-m.%-d" }}</span> &raquo; <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
