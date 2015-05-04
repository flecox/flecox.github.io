---
layout: page
title: Hello World!
tagline: My programming blog!
---
{% include JB/setup %}

##I'm Gonzalo Almeida


<img src="{{ site.url }}/assets/images/gonzo.jpg" alt="Drawing" style="width: 200px; float: right; padding: 20px;"/>


A freelance web developer and traveler, I love meeting new people and leanrningnew things all the time.
I mostly use Python (django) and Javascript when I work and personal stuff, I also have some experience on low level apps.

this will be my personal blog and I'll talk mostly abaout programming but from time to time I'll
add different topics.

please stay tuned!


<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
