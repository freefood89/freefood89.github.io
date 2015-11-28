---
layout: post
title: Local Elasticsearch Cluster with Docker Compose 
author: Rentaro
excerpt_separator: <!--more-->
---

This is a short post on how to build an Elasticsearch cluster on your dev machine using Docker Compose. At work I was asked to look into performing AMI rotations on Elasticsearch cluster nodes and as a first step I set out to build a local cluster. Elasticsearch comes with a nice thing called Zen that auto-discovers other Elasticsearch nodes on the same network interface (whatever that means), forms a cluster, and then elects a master node. I wanted to use this with Docker to minimize setup time as much as possible. 

<!--more-->

Maybe it's because I'm a noob, but this was a little harder than I thought. I had set the Docker network setting to "host" instead of the default value of "bridge":

```yml
es1:
  image: elasticsearch
  net: "host"
es2:
  image: elasticsearch
  net: "host"
```

## Some Explanation

Apparently, Zen Multicast uses UDP on its own network interface, but Docker containers on the bridge network have their own addresses. Using Zen Unicast as a workaround would require knowledge of the containes' IP addresses before they started if I wanted to use Compose to stand up all the containers at once. I wasn't about to write a complicated container orchestrator or modified init script for Elasticsearch.

Luckily I stumbled across [this blog post](http://www.dasblinkenlichten.com/docker-networking-101-host-mode/) explaining what "--net host" does when using Docker and realized that if all the containers are on the same network interface (the host's) then Multicast will work.