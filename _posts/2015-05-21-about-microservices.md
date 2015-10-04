---
layout: post
title: Migrating to a Microservices Architecture
author: Rentaro
---

There are two ways an organization achieves a microservice architectured web service. One way is by initial design: this involves thinking through service boundaries and logical groupings. The worse way, and also probably most common way, is by migration from a monolithic architecture.

## Some Pros and Cons

Migrating from a monolithic to microservices architecture is terrible for many reasons. Splitting up existing functionality into separate source code repositories is difficult technologically and organizationally. Shifting from database centric thinking to API centric thinking may also twist your brain at first. You will likely need to build your build and deploy pipeline from the bottom up.

The benefits may be worth the difficulty you face while migrating. The diversity in technology choice allows for better talent acquisition and more appropriate selection of tools to solve problems. Assuming that the service boundaries are well thought out, you'll see improved maintainability in shorter code with closer adherence to the single responsibility principle. However, I'll only explain the challenges I met since it's harder to have forsight into such things.

## Good Luck Migrating Code

Changing deployed code always causes nervousness. First off, nobody wants to mess with something that already works. You may face organizational push back to even discuss whether to split up services, let alone where to define the service boundary. Also, who likes refactoring code for existing services? Few people like redoing someone else's work.

Aside from the human challenges, you also have to figure out how to divide your services. It's pretty hard figuring out how to group API endpoints and functionalities without having a clear goal of how these services will be consumed and maintained.

## Silos Form along Service Boundaries

If you have a small developer pool, siloing can be a very dangerous unintended consequence of the flexibility you get from microservices. I experienced this issue first hand when a core developer created a rails app despite being the only ruby developer in the team. That developer made himself a bottleneck not only to the roll out of the rails app, but to releases of new features in other services.

Siloing in itself can lead to more issues as well. It becomes much more challenging to standardize practices like how to productionize the app. System Administrators must publicize where to expect production environment variables and access credentials. Dev-Ops needs to be a philosophy ubiquitous to all developers.

## Shifting Mindsets 

How can it be that microservices should have their own databases? I initially could not accept this fact because I was stuck in what my colleague calls "database centric thinking". Done the right way,microservices should expose data and functionality to be consumed as a backend in a way that abstracts the databases. As the diagram below illustrates, microservices should be the backbone of your service.

![diagram](img/2015-05-21-database-centric-thinking.png)

When the microservices, rather than the databases, are used as the backbone of the application the need to choreograph database model changes across service boundaries disappears. In the design on the right, both microservice A and the backend microservice need to validate data against object models. This results in functionality duplication possibly across code written in different languages i.e. a maintenance nightmare.

And of course, to avoid all these issues your code will need significant refactoring.

## Orchestrating Documentation???

I believe that developers should maintain documentation alongside code. Requiring developers to maintain up-to-date documentation of their code separately from their code takes unsustainable amounts of nagging. But if each microservice is written in different languages and maintained in separate repositories, how do you create a unified developer portal for consumers of the microservices? Answer: standardize your documentation format and create the developer portal as an orchestrated service that consumes many microservices. I ended up using Swagger across my microservices and simply hardcoding the documentation endpoints into the portal.

![diagram](img/2015-05-21-distributed-documentation.png)

How then does one maintain orchestration "logic" for pulling together all of the documentation? Afterall, if we have to update the documentation portal to include the new microservice, have we really solved the issue of having to nag developers to maintain multiple things? To be honest, I don't know. At least now from the developers perspective they only need to register their microservice once.

##Automating Everything

To really reap the benefits of a microservices architecture you really need a fully automated bulid and deploy pipeline. Atomizing your functionalities into microservices can make you super agile. However, none of this will work long term if you do not have automated regression tests. Being able to deploy code quickly also means you can quickly destroy your microservice and its consuming services as well. Without disciplined testing, versioning, and depracation strategies things can go to s**t pretty quickly.

##Closing Thoughts

If you find this discouraging, then you're probably ready to make this migration. There's no such thing as a free lunch. If you don't see that this technical debt costs lots of work, you're probably not ready.

This is an edited version of an older blog post.
