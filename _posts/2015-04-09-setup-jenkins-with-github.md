---
layout: post
title: Setting up Dockerized Jenkins with Github
author: Rentaro
---

I use Hudson as a Continuous Integration (CI) tool at work; it watches the SVN code repository and tests, builds, and deploys my services as code changes are commited. That got me wondering, how do I set it up for myself? 

For convenience and other arbitrary reasons I decided to use Jenkins with Github. Jenkins can listen for Github webhooks (event triggered HTTP requests) for cues on when to perform user configured build tasks. In my case, I ultimately want Jenkins to automatically test and deploy web services per code change.

##Jenkins on My Mac
In order for Jenkins to listen for webhooks it needs to be listening on a port. Several domain names registered through [no-ip](http://www.noip.com) point to an nginx reverse-proxy on my Mac so I naturally decided to set it up there. 

##Setup Jenkins Job


##Add Github Webhook
Once Jenkins was setup I setup webhooks for one of my Github projects.

Settings > Webhooks & Services > Add webhook

Payload URL: http://<hostname>/github-webhook/
Content type: application/x-www-form-urlencoded
Secret: [blank]
Trigger on push
