---
layout: default
title: About
---
## About Me

<center>
<img class="user-avatar" src="{{ site.owner.avatar }}" width="250" height="250">
</center>

Hi!

My name is Ichroman Raditya Duwila / @ichromanrd. I am a software developer living in Indonesia.
I've been using Java for around 4 years, lately I also learn some Javascript stuffs, Groovy and Kotlin.

I love coding, reading, hiking and travelling.

Cheers!

<div class="pagination">
  {% if site.owner.linkedin %}
    <a href="{{ site.owner.linkedin }}" class="social-media-icons"><i class="fa fa-2x fa-linkedin-square" aria-hidden="true"></i></a>
  {% endif %}
  {% if site.owner.email %}
    <a href="mailto:{{ site.owner.email }}" class="social-media-icons"><i class="fa fa-2x fa-envelope-square" aria-hidden="true"></i></a>
  {% endif %}
  {% if site.owner.twitter %}
    <a href="https://twitter.com/{{ site.owner.twitter }}" class="social-media-icons"><i class="fa fa-2x fa-twitter-square" aria-hidden="true"></i></a>
  {% endif %}
  {% if site.owner.github %}
    <a href="{{ site.owner.github }}" class="social-media-icons"><i class="fa fa-2x fa-github-square" aria-hidden="true"></i></a>
  {% endif %}
</div>
