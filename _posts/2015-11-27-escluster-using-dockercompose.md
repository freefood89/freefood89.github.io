---
layout: post
title: Local Elasticsearch Cluster with Docker Compose 
author: Rentaro
---

This is a short post on how to build an Elasticsearch cluster on your dev machine using Docker Compose. At work I was asked to look into performing AMI rotations on Elasticsearch cluster nodes and as a first step I set out to build a local cluster. Elasticsearch comes with a nice thing called Zen that auto-discovers other Elasticsearch nodes on the same network interface (whatever that means), forms a cluster, and then elects a master node. I wanted to use this with Docker to minimize setup time as much as possible. 

Maybe it's because I'm a noob, but this was a little harder than I thought. I had to set the Docker network setting to "host" instead of the default value of "bridge":

```yaml
es1:
  image: elasticsearch
  net: "host"
es2:
  image: elasticsearch
  net: "host"
```

## Some Explanation

Apparently, Zen Multicast uses UDP to find other Elasticsearch nodes on its own network interface, but Docker containers on the bridge network have their own addresses so the nodes can't find each other. From [this old github issue](https://github.com/docker/docker/issues/3043) it seems like Multicast on the bridge network isn't happening but, Using Zen Unicast as a workaround would require knowledge of the containes' IP addresses before they started. This would force me to start containers one by one, editing the elasticsearch.yml file as each container gets an IP address. I wasn't about to write a complicated container orchestrator or modified init script for Elasticsearch (a docker network equivalent of the [aws discovery plugin](https://github.com/elastic/elasticsearch-cloud-aws)).

Luckily I stumbled across [this blog post](http://www.dasblinkenlichten.com/docker-networking-101-host-mode/) explaining what "--net host" does when using Docker and realized that if all the containers are on the same network interface (the host's) then Multicast will work. Well that was easy.
