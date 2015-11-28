---
layout: post
title: Software Projects 
author: Rentaro
---

I've had an interesting year or so of pretending to be a software developer. 

I spent the first 10 months in an API development team using Java+Spring with hundreds of members. During that time I also quasi-managed my own after hours API development project, of which I set up the cloud infrastructure for. Having struggled without proper source code management and infrastructure automation at my workplace I did it the right way for my side project: everything from automated testing with Jenkins (with Mocha and NoseTests) to the automated deployment of containers in Amazons EC2 Container Service (ECS).  In July, I left my API team and joined a DevOps team to gain further experience in automating infrastructure.

In the past year I've picked up "Project Phoenix" by Gene Kim and recently started reading Fred Brooks' "The Mythical Man Month". This is a reflection on the year with respect to lessons learned about software development work flow.

## Observations on Workflow

During the early months of working I already began realizing that the API team at work was horribly unproductive. The developers are talented and the manager is sharp, but there were blocking factors everywhere. Hopefully this doesn't come out as me venting, as I already have been for months.

One of the most critical issues was that we were using SVN incorrectly. We'd been disallowed from creating our own branches, effectively limiting the number of developers on one code base to just one. Of course, we passed code around by email and took turns modifying the code, but for obvious reasons this was ridiculous and caused issues. As another side effect of only having one branch to work on, we were expected to only checkin code that works. Typically if I was "collaborating" with someone on an API, we would finish it individually and verbally coordinate code merges.

This first issue was made exponentially worse by our lack of automated Unit Testing and Integration Testing. We constantly suspected each other of introducing bugs into the shared code base because we would not know about bugs until the tester got around to in another month.

#### Applying Lessons Learned

Seeing the horrors of improper Source Code Management and nonexistent automation was very educational. Doing these the right way on my after-hours project at the same time and seeing its benifits was nothing short of revelational.

Proper use of Git and Jenkins allowed us to split up tasks into smaller issues. These issues had achievable requirements and deadlines that people committed to based on how they felt about it. Being able to modularize the code also meant that the the code needed to be designed for modularity, which lead to more testable code. Requiring every Pull Request to include tests allowed us to limit the "sequential nature of debugging" (Brooks, 17) by limiting the introduction of bugs by discovering the majority of them prior to merging code.

I was starting to see the point Brooks makes about the difference between picking cotton and creating a "programming system product". Development is very sequential and hard to partition into independent tasks. Furthermore, each engineer must communicate in order for their product to interface with others'. This is where the time-cost comes from. Brooks says that unlike other work media "[computers] are tractable" (Brooks, 15) and that poor scheduling of software projects come from optimism; however, I think that rather than computers, people, the most intractable work medium, may be the dominant work medium in software development.

## The Bigger Picture

As a college-hire I was put through Agile training. At the time I shrugged it off as a joke because in Electrical Engineering (my field of study) it was obvious that development had to be modularized and unit tested. Without question, design requirements were necessary for parts made by different people to properly interconnect. I'd failed to see that Electrical Engineering is a much more mature field with better defined practices, and that there's even value in standardizing (and naming e.g. Agile, Kanban) development planning and scheduling across an entire organization. Agile forces developers to, among other things, focus on modularizing the project earlier on and incrementally agree on how the pieces fit together rather than hoping everything fits together when things are hard to change. Of course with multiple contributing teams, utilizing the same project planning practices makes life much easier.

We're all trying to make software engineering more partitionable like picking cotton and reaping wheat.

#### Interfaces, Everywhere!

On a somewhat related note... in Object Oriented Programming, an Interface is "a common means for unrelated objects to communicate" ([Wikipedia](https://en.wikipedia.org/wiki/Protocol_(object-oriented_programming)), 2015). This has code reusability implications in OOP, but in project management it also serves as a contract of interconnection between two parts of code able to be used as a boundary for modularization. Because business logic is codified within Objects in OOP, interfaces readily serve as logical boundaries of work.

This concept applies to RESTful APIs and for CQRS as well. Unlike with typical RPCs and custom SOAP services where the clients can request servers to do things that vary greatly in scope and load, REST and CQRS are much more strictly defined  HTTP interfaces that allow better partitioned development. From a technical perspective strict CRUD-dy REST is a silly limiting constraint that increases network costs and orchestration work at the front end (Mobile/Web). However, it holds value from a project management and maintenance perspective. It allows one to expose a service through a technology agnostic interface in a way predictable to its consumers. As an example one might look at tools like Consul and Elasticsearch, which have RESTful interfaces allowing developers to access both of these unrelated tools using similarly structured code.

As an aside, I often hear people complain about how strict REST and Microservices has high network costs because of the orchestration and layering. That is factually accurate, but I think it's not too relevant as technological progress increases the performance of infrastructre. We've always sacrificed performance for productivity as we used higher level programming languages and concepts such as OOP, which itself is an interface for manipulating data without having to worry about the hardware it runs on.

I'm starting to see that even much of modern DevOps is building a codified replicable interface between the System + Resources (e.g. databases) and the Code. Aside from automating the workflow of development, DevOps standardizes how developers access and even monitor hardware resources. Container technology is another iteration in building a better interface between hardware and software.






