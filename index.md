---
# YAML Front Matter
layout: default
title: my first jekyll site
---

{% for post in site.posts %}
<div style="clear: both">
<h3 style="display: inline"><a href="{{post.url}}">{{post.title}}</a></h3>
<h4 style="display: inline">at ({{post.date | date: "%-d %B %Y"}})</h4>
</div>
{% endfor %}

