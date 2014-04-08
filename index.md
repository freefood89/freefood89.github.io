---
# YAML Front Matter
layout: default
title: my first jekyll site
---
# Blog Entries

{% for post in site.posts %}
- [{{post.title}}]({{post.url}})
{% endfor %}


![food](/food.jpg)
