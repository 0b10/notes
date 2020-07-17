
* can vendor lock-in be mitigated?
* why is monitoring and debugging harder?

## Summary

* FaaS is an event-driven subset of serverless that handles requests and events;
* The benefits are lack of infrastructure and system management;
* can be used for multiple service classes -- compute, databases etc.;
* apt (cost-effective) for massively parallel tasks, stream processing, data processing, bursty processes, microservices;
* bad for log running processes, or latency critical tasks;
* creates vendor lock-in;
* highly scalable, scales very quickly, and highly available;
 
## Notes

### Intro

Serverless focuses on application logic, and offloads infrastructure responsibilities (scaling, patching, provisioning etc.) onto the cloud provider. The main motivation is a lack of infrastructure.

Serverless has a pay-as-you-use model, and there is no idle time.

Serverless differs from [FaaS][ibm-faas] in that it focuses on any cloud service category -- compute, database etc. FaaS is a subset of serverless, but is instead event-driven, and responds to requests, or other events.

### Serverless vs Containers vs VMs

Serverless solutions are much more scalable that containers and VMs, because they are not bound to any *visible* context (aka server/container). Behind the scenes, these serverless functions will be bound to a context that is managed by the provider. That also  means that there is no manual implementation or required maintenance for scaling mechanisms.*Because* they are so effortlessly scalable, they are well suited to massively parallel tasks -- with tasks scaling horizontally on demand, over a number of managed resources.

There is also much less management in general with serverless because there are no images to maintain, patch, upgrade etc.

For bursty applications, or applications that are well suited for serverless, there may be significant cost effectiveness gains -- a system that only runs when needed, can scale very well, and is massively parallel, could end up being far more efficient, depending on the workload.

Containers and VMs on the other hand are much more suited for long running processes.

Serverless is also well suited for microservices since they are small, well defined units of code, that use event based messaging very well, are stateless, and scalable.

### How Does it Work?

#### TL;DR

Controller/load balancer, containers, message queues, a DB for storing actions/results/credentials, and an activation ID for asynchronous dispatch and result retrieval.

#### Glossary

* **action**: literally code, which is given a name for invocation;
* **activation id**: a job ID -- required because the action invocation is asynchronous;
* **invoker**: a service/daemon, inside a container, that runs actions;

#### The Process

1. an action request is received by a controller, from the client;
1. the request is authenticated, and the code retrieved from a DB;
1. the controller uses service discovery to locate an appropriate and available invoker;
1. the action is sent to the invoker via a message queue, and an activation ID is returned to the client;
1. the invoker runs the action, and stores the result in a DB -- along with the relative activation id.
1. the container is destroyed;

#### OpenWhisk

The Tech Stack:

* Controller: API endpoint, logic/dispatcher, and load balancer;
* Nginx: mainly used to terminate TLS;
* Kafka: message queue;
* Consul: service (invoker) discovery;
* Docker: invoker/runtime;
* CouchDB: persistence -- including the code.

![][openwhisk-tech-stack]

#### Communication

Typically they will use an event-based system. Events cause function invocations, and functions can publish events.

### Definitive Properties

#### Serverless

What makes up serverless?

* **FaaS**: the core of a serverless architecture;
* **serverless databases**: using object storage;
* **event-driven**: well suited for handling events or data streams -- e.g. Apache Kafka;
* **API gateways**: presumably FaaS in this case;

#### FaaS

What makes up FaaS?

* provisioning time -- milliseconds;
* zero administration, maintenance, capacity planning;
* automatic scaling: zero management, and much faster than containers;
* state is stored externally;
* persistent connections are not possible;
* automatic high availability and disaster recovery;
* resources limits;

### Pros

* system and user times are very accessible;
* massively parallel;
* significant cost savings for spiky workloads;
* very scalable;
* zero maintenance, administration, or capacity planning;
* almost no infrastructure;

### Cons

* long running processes are not ideal;
* vendor lock-in;
* unsuitable for low-latency applications -- spin-up delay;
* monitoring and debugging is harder;

### Use Cases

Serverless isn't great at everything, and it only makes sense to use it for some things. With a large backend architecture you will probably end up making use of containers/VMs too. With that being said, here are some potential use cases: 

* data processing: enrichment, transformation, validation, cleansing;
* event processing;
* binary processing: images, PDFs, audio, thumbnail generation, video transcoding;
* IoT;
* microservices (most common): small bits of code that do one thing, with great scaling, and provisioning;
* mobile backends;
* API backends: can be turned into HTTP endpoints, aggregated, and sat behind an API gateway;
* massively parallel tasks: map(-reduce), data search and processing from object storage, web scraping.

### Costs

Using [AWS Lambda][aws-lambda-pricing] as an example, it's $0.20 for every 1m requests, and ~1/1000 of a cent per GB-second (per second, per gigabyte of memory). In other words, 1000 seconds of processing @1GB of memory, will cost ~1 cent (this is just a very rough estimate, and there are explicit rates for different memory allocations).

Some say that serverless functions are cost effective, and it is easy to believe, especially for a low traffic website/saas. A pricey B2B SaaS that can do well with say 10-100 customers, making only a moderate amount of requests, could be essentially free.

There are other considerations, like other services, or other functions. It's unlikely that you will run only one function, or that your functions will all run, all of the time, in just a few milliseconds. It's likely that you will have dozens, or possibly hundreds of functions -- each racking up expenses. Functions are also unlikely to be optimised, especially at the start. Even language choice, like Go vs Java, could have an impact on how much memory, or the how long the execution time is. Serverless databases, or even managed solutions, will all add to the total cost of the application.

In conclusion, unless a thorough cost analysis is done and measured against revenue, the code is optimised, and you have at least some reserves to burn through, serverless seems like it could be quite dangerous -- like a long distance phone bill that could have runaway costs unless closely monitored. Although, some swear that it's cheap, and they're probably right, when taking into account the free quota, and when only using it sparingly for specific tasks where it makes sense. The argument is that you only pay for what you use, but is what you're paying actually match what the computation is worth? Would getting a $5 compute instance, and running it 24 hours a day, be more or less expensive than running a computationally equivalent serverless function, while running invocations back-to-back? Which is actually the cheapest per unit of computation? That is something that can only be answered through experimental testing.

## Glossary

* [*GB-second**][ibm-pricing]: is a cost unit that calculates the cost of serverless function, per second per gigabyte of memory;

## Sources

* [FaaS | IBM][ibm-faas]
* [Pricing | AWS Lambda][aws-lambda-pricing]
* [Pricing | IBM][ibm-pricing]
* [Uncovering the Magic | Markus Thommes][how-openwhisk-works]

[ibm-faas]: https://www.ibm.com/cloud/learn/faas
[how-openwhisk-works]: https://medium.com/openwhisk/uncovering-the-magic-how-serverless-platforms-really-work-3cb127b05f71
[openwhisk-tech-stack]: https://miro.medium.com/max/958/1*W1xT77DJ8ZKDQSKjqbfaEQ.png
[ibm-pricing]: https://cloud.ibm.com/functions/learn/pricing
[aws-lambda-pricing]: https://aws.amazon.com/lambda/pricing/
