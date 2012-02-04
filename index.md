---
layout: page
title: Just a <s>Functional</s> Programming enthusiast in Ruby land
---
{% include JB/setup %}

<article class="recent">
  <h4> most recently... </h4>
  <ul class="posts">
    {% for post in site.posts limit:5 %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
</article>

<article>
    <em> latest </em> >> {{ site.posts.first.date | date_to_string }}
    {{ site.posts.first.content }}
</article>
