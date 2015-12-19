---
layout: post
title: Software Project Management and Interfaces 
author: Rentaro
---

I've had an interesting year or so of pretending to be a software developer. 

I spent the first 10 months in an API development team using Java+Spring with hundreds of members. During that time I also quasi-managed my own after hours API development project, of which I set up the cloud infrastructure for. Having struggled without proper source code management and infrastructure automation at my workplace I did it the right way for my side project: everything from automated testing with Jenkins (with Mocha and NoseTests) to the automated deployment of containers in Amazons EC2 Container Service (ECS).  In July, I left my API team and joined a DevOps team to gain further experience in automating infrastructure.

In the past year I've picked up "Project Phoenix" by Gene Kim and recently started reading Fred Brooks' "The Mythical Man Month". This is a reflection on the year with respect to lessons learned about software development work flow.

## Observations on Workflow

During the early months of working I began realizing that the API team at work was horribly unproductive. The developers are talented and the manager is sharp, but there were blocking factors everywhere. Hopefully this doesn't come out as me venting, as I already have been for months.

One of the most critical issues was improper use of SVN. We'd been disallowed from creating our own branches, effectively limiting the number of developers on one code base to just one. Of course, we passed code around by email and took turns modifying the code, but this is clearly ridiculous and caused issues. As another side effect of only having one branch to work on, we were expected to only checkin code that works. Typically if I was "collaborating" with someone on an API, we would finish it individually and verbally coordinate code merges.

This first issue was made exponentially worse by our lack of automated Unit Testing and Integration Testing. We constantly suspected each other of introducing bugs into the shared code base because we would not know about bugs until the tester got around to in another month. We also needed to become experts on the entire shared code base to avoid situations where development is blocked due to sickness or paid time off.

### Applying Lessons Learned

Seeing the horrors of improper Source Code Management and nonexistent automation was very educational. Doing these the right way on my after-hours project at the same time and seeing its benifits was nothing short of revelational.

Proper use of Git and Jenkins allowed us to split up tasks into smaller issues. These issues had achievable requirements and deadlines that people committed to based on how they felt about it. Being able to modularize the code also meant that the the code needed to be designed for modularity, which lead to more testable code. Requiring every Pull Request to include tests allowed us to limit the "sequential nature of debugging" (Brooks, 17) by limiting the introduction of bugs by discovering the majority of them prior to merging code.

I was starting to see the point Brooks makes about the difference between picking cotton and creating a "programming system product". Development can be very sequential and hard to partition into independent tasks. Furthermore, each engineer must communicate with each other in order for their products to fit together. Brooks says that desipite the fact that "[computers] are tractable" (Brooks, 15), developer optimism is what results in mismanagement of project schedules. However I think that people are the actually the dominant work medium and thus are also the dominant time-sink in software development. He said himself that the cost of communication increases quadratically (n)(n-1)/2 with the number of people. 

### Agile Development is Real

As a college-hire I was put through Agile training. At the time I shrugged it off as a joke because in Electrical Engineering (my field of study) it was obvious that development had to be modularized and unit tested. Without question, design requirements were necessary for parts made by different people to properly interconnect. I'd failed to see that Electrical Engineering is a much more mature field with better defined practices. Agile forces developers to focus on modularizing projects early and incrementally discuss designs that fit together rather than hoping everything fits together later when work becomes harder to change. 

There also seems to be value in standardizing (and naming e.g. Agile, Kanban) development planning and scheduling across an entire development organization. Utilizing the same project planning practices between collaborating teams makes planning a lot simpler because all members of their respective teams have expectations of what needs to be hashed out during initial planning sessions. By constraining communication patterns within and between teams, maybe we can reduce the cost of communication to at least be linearly proportional to the number of developers.

## Interfaces, Everywhere!

Aside from the devices that improve our workflow like Git and Agile, there seems to be a constant effort to make development work partitionable. I'm particularly insterested in how interfaces are implemented throughout our technology stack to constrain the design process.

In Object Oriented Programming, an Interface is "a common means for unrelated objects to communicate" ([Wikipedia](https://en.wikipedia.org/wiki/Protocol_(object-oriented_programming)), 2015). This has code reusability implications in OOP, but in project management it also serves as a contract of interconnection between two parts of code able to be used as a boundary for modularization. Because business logic is codified within Objects in OOP, interfaces readily serve as logical boundaries of work.

This concept applies to RESTful APIs and for CQRS as well. Unlike with typical RPCs and custom SOAP services with which the clients can request servers to do things that vary greatly in scope and load, REST and CQRS are much more strictly defined HTTP interfaces that allow better partitioned development. From a technical perspective strict CRUD-dy REST is a silly limiting constraint that increases network costs and orchestration work at the front end (Mobile/Web). However, it holds value from a project management and maintenance perspective; it allows one to expose a service through a technology agnostic interface in a way that leverages its consumers expectations. As an example one might look at tools like Consul and Elasticsearch, which have RESTful interfaces allowing developers to access both of these unrelated tools using similarly structured code. Not only doesn this make the tools accessible, but it also makes it easier to develop SDKs because there are now established patterns for developing SDKs for REST APIs. 

As an aside, I often hear people complain about how strict REST and Microservices has high network costs because of the orchestration and layering. That is factually accurate, but I think it's not too relevant as technological progress increases the performance of infrastructre. We've always sacrificed performance for productivity as we used higher level programming languages and concepts such as OOP, which itself is an interface for manipulating data without having to worry about the hardware it runs on.

Even much of modern DevOps is just building a codified replicable interface between the System + Resources (e.g. databases) and the Code. Aside from automating the workflow of development, DevOps standardizes how developers access and even monitor hardware resources. Container technology is another iteration in building a better interface between hardware and software.

It's interesting that unlike in electrical engineering where a system engineer provides the component constraints or where physics and circuit topologies can be limiting constraints, software engineering has much fewer constraints. As freeing as that can be, it's also interesting that the abstract unconstrained nature of software can also be an impediment to accomplishing tasks.




