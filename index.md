---
# YAML Front Matter
layout: default
title: my first jekyll site
---
## Blog Posts

{% for post in site.posts %}
###[{{post.title}}]({{post.url}})
<h4>({{post.date | date: "%-d %B %Y"}})</h4>
{% endfor %}


![food](/food.jpg)
