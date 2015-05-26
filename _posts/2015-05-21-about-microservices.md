---
layout: post
title: A Quick Note on Microservices
author: Rentaro
---

In a monolithic system, its technology stack is often limited to just one option (most likely to one I don't like). Services employing a microservices architecture, on the other hand, offers flexibility in technology choice as well as other advantages. These advantages come at some costs and challenges, some of which I've encountered and will be sharing here.

To give context, I've been working with friends on a side project ever since we were hired into the same workplace. It started out as a simple MEAN stack project. However, seven months later the project has ballooned in complexity and participants; so, out of convenience and curiosity we piloted adopting a microservices architecture.

##The Challenge of Documentation
Unifying documentation arose as a challenge in migrating to a microservices architecture. Each microservice has an accompanying API documentation endpoint that provides swagger specifications. In order for documentation from all of the microservices to show up in a single UI, which ever microservice serving that UI has to be aware of all of these other microservices. This poses a challenge as each microservice will be separate processes listening on differing ports, and possibly even running on different hosts. In decoupling the microservices, so only the software for the changing service needs to be updated, we inevitably introduced dynamic behavior in some other part of the system.

There are several solutions to this. One could have whatever's managing cluster nodes, or alternatively the CI tool, keep tabs on all of the endpoints. This would work great if it supports service discovery. One could also create a microservice that takes in documentation generated and sent by every microservice and serve a large compiled documentation page. 

##The Challenge of Business Models
RESTful APIs CRUD (Create, Retrieve, Update, & Delete) "business models". In our case the models represent things like customers, accounts, bills, and such things relevant to a bank. In a microservices architecture managing implementations of these models can be painful. 

For example, in situations in which one removes or renames a field in a business model, one may also need to modify every microservice that depends on this model. This is due to the fact that logic pertaining to the field may be embedded in multiple microservices. The challenge may even lie in keeping track of all the microservices that are dependent on this model. Ideally this situation can be avoided by planning around business models; however, many people will experience this challenge because they'll be migrating from an existing monolithic architecture. 

Unfortunately, one may also encounter an issue in implementing OOP classes for these models in whatever language is used for each microservice. This can be time consuming and require additional work to maintain.

##The Challenge of Deploying
Without using a tool like docker managing all of the separate microservices processes become a nightmare. It's entirely impractical to have to manually start and stop many microservices processes and run them via tools like screen and tmux. It's also very hard to health check each of the microservices. A tool like Swarm or Consul are musts in managing such a system.

##Closing Thoughts
To me, these issues do not pose too much of a technical challenge. The difficulty in confronting these issues actually lie in their subjective nature. There really is more than one right solution, so it's difficult to have conviction in choosing any particular one. Especially with the indeterminate future state of projects, one can't do much better than searching the web or reading books, and perhaps trial and error.

