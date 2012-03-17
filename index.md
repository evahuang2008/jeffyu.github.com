---
layout: page
title: Latest entries
tagline: Supporting tagline
---
{% for post in site.posts limit: 6 %}
<span>{{ post.date | date: '%B' }} {{ post.date | date: '%e' }}, {{ post.date | date: '%Y' }}</span>
<h4>
    <a href="{{post.url}}">{{ post.title }}</a>
</h4>
{% endfor %}

