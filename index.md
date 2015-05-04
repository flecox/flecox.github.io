---
layout: page
title: Hello World!
tagline: My programming blog!
---
{% include JB/setup %}

##I'm Gonzalo Almeida


<img src="{{ site.url }}/assets/images/gonzo.jpg" alt="Drawing" style="width: 150px; float: right; padding: 20px;"/>


A freelance web developer and traveler, I love meeting new people and leanrning new things all the time.
I mostly use Python (django) and Javascript(learning react.js now) for working and personal stuff, I also have some experience on low level apps but I haven't use c/c++ in a while heh.


This will be my personal blog and I'll talk mostly about programming but from time to time I'll
add different topics, like cool places, cool things to do, python and javascript!.

please stay tuned for rock and roll!!


<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
