ISBN-10: 1491950358

### 3: How To Model Services

#### p64: What Makes A Good Service?

* High cohesion: define boundaries to ensure related behaviour is in one place

#### p67: The Bounded Context

* each bounded context has an explicit interface
* if you requires something from a bounded context, you communicate with its boundary using models
* two concepts that share little in common are different bounded contexts (think about it, low cohesion) - although they may have some common interests, this form part of the shared model
* shared models don't need to expose everything about themselves - there is an internal and shared view of that same model, which helps to avoid tight coupling
* bounded contexts lend themselves to the concepts of modules in a monolith
  * they should have their own hidden modules if they are to map to a service properly
    * these hidden modules are implementation details for the service

#### p72: Business Capabilities

* when thinking about bounded contexts, you should be thinking in terms of the capabilities those boundaries provide - what does it do? Not in terms of the data that is shared
  * e.g. "it processes foo", not "it produces foo"


#### p73: Turtles All the Way Down | (aka nested bounded contexts)

* A bounding context may also have sub-bounded contexts - e.g. microservices can rely upon other microservices that are hidden to external clients
* sometimes the higher-level (outer) bounded context may not make sense to be modelled, and the inner contexts will stand on their own
* the nested approach can be easier to test because the outer context is what is tested

#### p76: The Technical Boundary

* Boundaries should be made with regards to organisational structure
* Technical boundaries occur when there are divisions based on the underlying technology, like database - an API whose sole reason to exist is to wrap a DB. This is a bad boundary for a service.
* Technical boundaries can sometimes make sense (like performance reasons), but they are secondary to the business context

### 4: Integration

#### p86: Interfacing With Customers

* Exposing the database outside of the service creates coupling - to implementation and the underlying tech
  * If that happens, it will require large amounts of regression testing for implementation changes

#### p89: Synchronous vs Asynchronous

* event-based: think of it as "this thing happened" - pub/sub

#### p90: Orchestration vs Choreography

* The orchestrator can be any service that requires other services, from the book, a customer service service (yes, service service) orchestrates several other services
* orchestration
  * leads to centralisation
  * brittle
  * higher cost of change
* choreography can be achieved through an even-based approach
  * this takes additional work to ensure things have worked correctly across service boundaries
    * [personal]: perhaps subscribing can also include a reverse subscription, such that subscribers can inject a subscription so that the publisher of the original event can be notified of status updates from the subscriber 
* [personal]: you can use a centralised logging service to track events

#### p93: Remote Procedure Calls

* are local calls that execute remote procedures - you make a local call, and ignore everything else
* some depend on an interface definition - which make it easier to generate stubs for different tech stacks
* Java RMI introduces tight coupling
* SOAP/XML etc. and sometimes UDP or other lower protocols
* Usually binary in nature
* Is very easy to use, and quick to get started
* comes with some not-so-apparent issues (the book doesn't detail)
* Thrift, protocol - to name a few
* RPC typically creates coupling - to the tech, and internal implementation
* networks WILL fail, pretend that there's a malicious actor - packets can be malformed, dropped, or delivered slowly etc..
* you need to think differently about remote APIs/service boundaries - they are not the same as local calls
* RPC is brittle - changes to a call interface means changes within the client and the server - e.g. a function(foo,bar), if bar is never used, and removed, both the caller and receiver have to change their interface

#### p99: REST

* REST allows for HTTP caching - like Varnish
* allows load balancers - like mod proxy
* supports many of the HTTP tools out there
* HTTPS is suggested as a solution
* Use HTTP well, or it can be hard to scale - see the REST spec.
* REST provides HATEOAS - hyper media as the engine of application state
  * an example is a shopping cart going from a single link, to a Javascript component
  * this decouples the client from the service
  * essentially the client progressively discovers the API
  * A caveat is that this is quite chatty, and the recommendation is to not optimize too early
* JSON, XML, or Something Else?
  * XML can make use of hypermedia controls because elements can store properties - i.e. supports hyperlinking
  * JSON has no native means to deal with hyperlinking, and you need to use other concepts such as HAL
  * There are web base HAL browsers to make creating a client much easier
  * XML is well supported, and has standard tooling around it like XPATH and CSS selectors, for navigating the document
  * JSON is the format for most people
* Beware toomuch convenience
  * DBs should not expose their internal implementation in any way - use an API
  * You can defer building the DB model until the API has stabilized, and reflects what consumers need - use a flat file for intermediate development, this avoids the DB model influencing the API - which couples clients to the DB model
* Downsides of REST over HTTP
  * You will have to stub out REST responses for testing - either find a library, or you will have to roll your own solution (tooling)
  * some REST frameworks don't support all http methods, so you will have to find one that does
  * Thrift is more compact than HTTP/REST
  * HTTP isn't low latency. Other protocols built on top of TCP are lower latency
  * low latency between services isn't really possible with HTTP - look at other protocols. RPC supports many protocols
  * payloads themselves have a particular shape, and consuming them can cause coupling with the remote service
* REST over HTTP is a good choice for inter-service communication - despite the drawbacks 

#### p108: Implementing Asynchronous Event-Based Collaboration

* RabbitMQ
  * a good way to implement decoupled messaging
  * handles pub/sub
  * is stateful, and remembers which channels have receives what messages
  * adds complexity, and requires expertise
    * these systems need to be stubbed out for testing
  * is event-based
  * scalable and resilient
  * the author is "a fan" of it
  * is not EMB - enterprise message bus
* keep your middleware dumb, and endpoints smart - don't accept solutions that push more and more business logic into the middleware 
* HTTP
  * higher latency
  * ATOM
    * ATOM feeds can be polled for changes
    * endpoints must track what messages have been seen
      * duplicated effort for each endpoint to track this, when a central message broker can do it
    * you will end up with a solution to existing message brokers anyway
  * is scalable
  * higher latency than some message brokers
* complexities of asynchronous architectures
  * what do you do when a node it down, and a message it was suppose to handle is sent?
  * have good monitoring in place
  * use correlation IDs for monitoring
* patterns
  * message hospital aka. dead letter queue: a place where failed messages live (e.g. the node fails, and the message isn't processes) - timeouts, and retry limits are a thing to consider for the consumers 

#### p112: Services as State Machines

* Services can be modelled as state machines, because all state/behaviour related to that bounded context should be encapsulated by the service
* avoid dumb services

#### p112: Reactive Extensions | Rx

* can compose the result of multiple results together - concurrently
* can be used for blocking/non-blocking logic
* inverts traditional flows -- rather than asking for some data then reacting, you observe, and react when something changes
* a recommended choice

#### ==== READ ===

* the rest of the chapter - 114-145

### 5:p145: Splitting the Monolith

(this chapter is only briefly read)

#### p146: It's All About Seams

* Seams are areas of code that are highly cohesive - perhaps name spaces
* bounded contexts make good seams
* you should identify these seams

#### p147: Breaking Apart MusicCorp

* packages hold code that are defined by a bounded context
* represent the relationships graphically, if you see any associations that don't make sense in the business domain then investigate, and fix.
* sometimes you can concentrate your efforts on one bounded context, instead of them all

#### p149: The Reasons To Split The Monolith

* do it incrementally, don't do it all at once. However, define the seams up-front

#### p151: Team Structure

* Since the system architecture will/should reflect the organisational structure, then splitting a monolith up to reflect that is one reason for doing microservices

#### p152: Security

* you may want to provide extra security/monitoring for specific services

#### p152: Technology

* Easier to reimplement, or change individual services - there is more development velocity

#### p154: Tangled Dependencies

* Use modelling tools to model an acyclic graph for dependencies - seams that have more entrenched dependencies will be harder to refactor

#### p156: Getting to Grips with the Problem

* You will need to split up the database code by identifying seams -- aka. bounded contexts -- within the database
* schemaspy is a tool that can help visually represent relationships between tables
* any coupling between tables may end up spanning service boundaries - that is, multiple services will collaborate

#### p158: Example: Breaking Foreign Key Relationships

* to split joins, replace the join with an API call.
* foreign key relationships should be removed, with their concepts (targets) maintained individually in each database, and use some kind of consistency check, to ensure each DB are in agreement
  * remember that these items can be changed, removed etc. - and consistency must be maintained across services

#### p167: Transactional Boundaries

* transactions mean everything works, or the transaction is rolled back
* they don't just apply to databases

#### p170: Try Again Later

* when a constituent of a transaction fails (across service boundaries) you can use the "eventual consistency" approach
  * queue up that part of the operation
  * this approach is useful for long-lived operations

#### p171 Abort The Entire Operation

* you can roll back the entire transaction
* sometimes the compensation action can fail - in that case you can retry it, queue it, or something that is manually handled by an admin
* compensation actions can be very challenging when there's several


#### p172: Distributed Transactions

* works by
  * having a transaction manager
  * having multiple services (cohorts) that run constituents to transaction
  * each cohort voting yes/no depending on the outcome of their process
  * completing the entire transaction only when all cohorts vote yes
  * abandoning the entire transaction if only one cohort votes no
* issues
  * locking - until all cohorts vote
  * the transaction manager can go down
  * a cohort can go down
  * a cohort can fail after voting yes
  * it doesn't scale well
* use existing implementations, this is not easy to implement

#### p172: So What To Do?

* systems with eventual consistency are easier to build and scale
* can a single transaction be done in several smaller, local transactions, with eventual consistency?
* try very very hard to avoid splitting up transactions that need to be consistent
* model these transactions at a high level
  * define hooks for compensation actions

#### p175: The Reporting Database

* even in a monolith architecture, a reporting database is usually duplicated, to reduce load on the primary database when generating reports

(== Skip sections on data pumps ==)
(it only provides bad solutions, eluding to the good solution -- event data pump)

#### p182: Event Data Pump

* all the other data pump, syncing/duplicating databases are sub-optimal, and introduce coupling
* a data pump is just pushing data out - probably into a message queue
* event data pump is just pushing data out as events
* as date is written to the database, it is also pushed out to subscribers
* one downside is that it is harder to push out lots of data, in contrast to a traditional (non-event based) data pump

#### p183: Backup Data Pump

* netflix uses cassandra, and has free tools to manage it
* Amazon S3 is a good place to store backups - there are significant data durability guarantees
* Aegisthus is the netflix tool for their reporting pipeline

### 6:p188: Deployment

#### p189: A Brief Introduction to Continuous Integration

* Artefacts can include things like the service you are testing - which is built once, and many tests run against it
* Artefacts are placed into a repository of some sorts - sometimes provided by the CI tool

#### p190: Are You Really Doing It? (CI)

* Using CI isn't the same as practising CI
* check-in your code once per day - you need to check your code against others
* a broken build should be the #1 priority to fix

#### p194: Build Pipelines and Continuous Delivery

* smaller scoped tests should come before larger scoped tests - for faster feedback
* the build artefact is reused for each stage
* each check-in is a release candidate
* Continuous delivery is different from CI, in that it also models other stages outside of the typical integration tests for CI, some manual tests for user acceptance testing - basically everything that's necessary to deploy into production
  * CI uses different tools from CD - you can't hack CI tools to do CD stuff
* Just like with CI, it's one CD pipeline per service 
* a pipeline demonstrated in the book:
  * compile + fast tests => slow tests => user acceptance tests => performance testing => production

#### p196: The Inevitable Exceptions | (i.e. things that don't fit the prescribed advice)

* You should start out with a monolith until the API stabilises
* If there is some discontinuity between services, then merge them back into a monolith until it stabilises
* in the early stages, when/if the API isn't stabilised, you may need to opt for a lock-step release temporarily until it does

#### p197: Platform-Specific Artifacts 

* You may need some configuration management to deploy some artefacts, like nginx, where these kinds of artefacts are necessary to test the service.
  * Chef, Puppet, and Ansible are some suggestions
* lots of different artefact types are not a good thing for CI
  * [personal]: pick a tech stack, and stick to it 

#### p198: Operating System Artifacts

* you can use a package manager to deploy artefacts for the service (instead of configuration management) - rpm, deb etc. are considered OS artefacts
* you should reduce the number of operating systems that you use - just a suggestion

#### p199: Custom Images

* [personal] - TODO: how does a load balancer deal with spinning up new images that have some kind of configuration?
  * with a config manager - does it run the setup first?
  * with a container within - does it clone and set it up?
* the book implies that there is a spin-up time
  * it's an issue for elastic compute
  * it's an issue for CI and CD - which increases the feedback time
  * one solution is a custom image, with all the dependencies installed, and all that is necessary is to pull the latest version of the service
    * [personal] - TODO: but what about things like NPM dependencies? They still need to be installed
* a custom VM image isn't the best solution, many services have their own proprietary formats, and VM images are bulky
  * these tools allow you to create templates, to speed up spin-ups
    * packer is am automated vm image provisioning tool
    * vagrant is an automated development environment vm image provisioning tool

#### p202: Images as Artifacts

* One solution to the spin-up time issue is to bake services into images, and treat images are artefacts
* this solution makes it easier to adopt different tech stacks, because we only care that it works. they also have their own CI/CD pipeline, so the differences in tech stack are again insulated

#### p203: Immutable Servers

* changes made to a server that hasn't when through the build pipeline is called configuration drift
* disabling SSH when the image is created, to ensure that no config drift ensues
* storing data elsewhere is also an issue that needs to be resolved
* these lead to systems that are easier to reason about

#### p204: Environments

* Each stage in the delivery pipeline can have different environments
  * a production environment may have a load balancer, and several instances of a service
  * a test environment may only have one instance
  * an example is sharing state requires some behaviour that can break - which may not be found in a single, testing image
  * use clustering as part of the test environment
* production-like environments
  * as you move through the pipeline, increase the environment to be more production-like
  * are slow (spin-up times), and provide slow feedback - so this is later in the pipeline
  * they can be hard to setup, so make some compromises
  * adjust the pipeline to optimise for faster feedback earlier

#### p206: Service Configuration

* Keep the configuration that changes between services to a minimum
  * this causes services to fail only because of said differences
  * a good example is a db password - that is something that probably will change between services
* don't build different artefacts for different environments -- test, production -- if you only test one, you can't be sure the other works
* one option is to use separate configuration for each environment

#### p208: Multiple Services Per Host

(where a host is an isolated environment - vm, bare metal etc.)

* can interfere with host metrics logging -- like cpu -- which service is causing a spike?
* one service can impact the performance of others
* contradictory dependencies can be an issue
* can result in lock-step releases to ensure that all services work together
* host configuration is shared between teams - so they lose autonomy
* deployment options like image based services, and immutable services are not possible
* interferes with scaling
* secrets for services are not as secret

#### p210: Application Containers | (i.e. many services, one container)

* shared resources can be a benefit - like JVM
* constrained tech stack - each service depends on the same tech stack
* limits the options for automation and management
* analysing resource and thread use is confusing - because of shared resources
* again, monitoring is more convoluted and harder to distinguish between services

#### p212: Single Service Per Host

* probably the best choice
* monitoring is easier
* remediation is easier
* proper isolation between services for security, and performance
* easier to scale each service
* image based deployment and immutable images are possible
* reduces complexity, because things like scaling, and other considerations are no longer a factor
* easier to reason about

#### p214: Platform as a Service

* PaaS is more concerned with a tech-specific artefact, like a jar file.
* it handles scaling for you
* Heroku is a paas - the author described it as the "gold class of paas"
* you don't have control of the environment, and that may work against you in some situations
* some paas scaling algorithms are not that great, and depending on how much your application deviates from the norm, may mean it's less suitable for your needs
* the smarter the paas, the more things go wrong -- as a rule of thumb
* paas is the future

#### 215: Automation

* managing hosts manually (non-paas) is hard work
* automation is essential
* developers should have access to the same tool chain that is used to deploy to production - making it easier to spot problems early on
* everything should be automated -- provisioning machines, starting/stopping machines, deploying databases -- everything

#### p216: Two Case Studies on the Power of Automation

* automation has increased benefits as time goes on.
  * the up-front cost is expensive, but as the overall scope increases, deployment rates can increase exponentially

#### p220: Vagrant

* is a full development environment that accommodates for scenarios - like service/host failure

#### p221: Linux Containers

* requires some routing to be visible to other hosts if you have several container inside one vm host. This will mean lots of port forwarding rules
* not completely secure/isolated - they can be broken out of

#### p226: Deployment Interface

* having a unified deployment interface is vital
  * for dev, test, and production
    * keep all as similar as possible
    * can be triggered by scripts, CI, or manually etc.
    * a single CLI call will suffice
  * How it should look 
    * name and version should be provided
    * for dev you want to deploy the version on your machine
    * for testing you want the latest green build
    * for testing/diagnosing issues, any given build
    * the environment should be provided - like full images for production and testing, docker images for development etc. This should be hidden, and abstracted
    * example: deploy artefact=name environment=local version=local
    * the ci tool could deploy with a specific build version number for example
  * use something like YAML to define remote configuration 
* this is a significant amount of work 

### 7:p231: Testing

#### 232: Types of Tests

* from the book "agile testing":
  * business facing - non-technical
    * Acceptance: did we build it right?
    * Exploratory
      * usability
      * how can I break it?
      * Manual
  * technology facing - developer/technical 
    * Unit
      * did we build it right?
      * automated
    * Property testing 
      * response time
      * scalability
      * performance
      * security
      * tools
* microservices mostly use automated testing - e.g. technology facing tests 

#### 234: Test Scope

* The test pyramid
  1. e2e - few tests
  2. service - happy median
  3. Unit - lots
* unit tests
  * property tests also fall under the category of unit tests
    * [personal]: although I'd say only if a single function is being tested, and not the entire service -- e.g. for response time etc.
  * when e2e or service tests fail, write a unit test to catch it faster in the future 
* service test
  * bypassing the UI
  * tests services in isolation - use stubs
  * [personal]: possibly stub out the database
* e2e
  * tricky to do in a microservices context
* how many tests?
  * an order of magnitude more than the previous stage of the pyramid as you go down it
    1. e2e - 40
    2. service - 400
    3. unit - 4000
  * smaller scoped tests are best
* testing anti-pattern
  * turning the pyramid upside down - i.e. much more e2e tests than unit test
    * these tests take longer to run, and are more difficult to determine what went wrong

#### 241: Implementing Service Tests

* when using mocks, checking that a call was made can lead to brittle test. 
* use stubs more than mocks
* Mountebank is a stub service that can do mocking etc - it's a service that is programmable via http and can be setup in a predictable way for each test
* e2e testing
  * important to find breaking changes between services too

#### 244: Those Tricky End-to-End Tests | (CI and e2e tests)

* CI
  * unit tests, and service tests will be parallel pipelines for each service - that is, each service will have their own CI pipelines for testing themselves
  * e2e tests should be a single stage in a CI pipeline, where all service pipelines merge and a single e2e test suite is executed - this avoids test duplication between otherwise separate suites

#### 247: Flaky and Brittle Tests

* moving parts
  * parts of the system that are not directly under test, but can change - like other services. These can cause a test to fail, but in reality it's not the context of the test failing, but some other concept 
* flaky tests
  * non-deterministic: tests that sometimes passes, and sometimes not
  * multiple threads are a culprit - race conditions, timeouts
  * they don't tell much when they fail
  * usually have moving parts - other services
  * remove flaky tests, or fix them - intermittent failures train people to accept failures as a norm
    * you can rewrite to avoid multiple threads, make the underlying system more stable or simpler, or you can move the testing to smaller scoped tests
* who writes these tests?
  * it's a shared responsibility, and a shared codebase
  * avoid free-for-all, and over-testing
* how long?
  * e2e tests can take hours, days, or weeks - test overlapping is a big issue
  * you can do test in parallel with selenium grid etc.
  * value/burden trade-off for each test - does it provide real value, or is it a burden?  
* the great-pile up
  * failed integration means the build cannot (should not) be deployed, but this leads to a pile up of upstream commits
  * one imperfect way to resolve it is to not allow check-ins until the previous build can be deployed
* the meta-version
  * avoid versioning all services as a single release, this creates coupling between deployments - each service should have its own independent version 

#### 252: Test Journeys Not Stories

* e2e tests become difficult when the number of services increase beyond a couple (1-2)
* don't add tests for every story, this causes the suite to become bloated, and have overlapping tests and poor feedback cycles
* focus on "journeys" not stories - where a journey is a high value interaction, something with importance
  * journeys should be mutually agreed upon to avoid bloat
  * journeys should be jointly owned
  * example: order a CD - and all the steps entailed with that (I don't see the difference between a story and a journey tbh)
  * tests not covered by e2e should be tested via service tests, or better, via unit tests
* integration tests (like e2e) should be few in number -- low double digits, even for complex systems

#### 253: Consumer Driven Tests to the Rescue

* integration tests just check that deploying new services don't break results for consumers
* CDC: consumer driven contracts
  * should be run against individual, isolated services
    * which are the same level as service tests - but they are not service tests, they have a specific focus to catch contract failures and identify which consumer will be affected
    * because it's reliable, faster, and have better feedback than testing them as e2e
  * should be part of a service's CI pipeline
  * each consumer should have a test suite - if a service has two consumer services, a test suite (built against the contract) should be created to represent each consumer - assuming they each have different expectations for how the service should behave
    * [personal]: it might not be necessary if the expectations are identical for each consumer
    * cross-team collaboration would be necessary to define the tests
* Pact
  * is a consumer driven contract testing library
  * it creates a mock consumer service, to consume services rendered by the provider
  * the real consumer team produces a Pact spec that providers have access to
  * providers consume the spec, and a mock server is used to test against the service
  * specs should be part of the CI pipeline via the artifact repository, or via the Pact broker 
* Pacto
  * like pact, but the spec is auto-generated via recorded interactions
  * although, pact is more flexible in that you can define parts of the spec that has yet to be implemented within the service
* CDCs require good communication (spec sharing and testing) between teams from consumers and providers, for third-party vendors, integration tests may be your only option 
* Should you use e2e tests?
  * maybe
  * if you can get good coverage with CDC and have good monitoring, you can do away with e2e tests
    * opting, instead, to use the journeys (e2e drivers) to define semantic monitoring instead

#### 259: Testing After Production

* tests are essentially a series of models - models about the expectations of the system
* test both functional and non-functional aspects
* you can not reduce the chance of failure to zero - there are diminishing returns, and more and more tests are not always the most optimal option
* use smoke tests to test the deployed service, which will catch any environment issues - this should be part of the deploy command
* blue/green deployment involves having two versions of the same service running. the new service has some smoke tests run against it, and when it passes, production traffic is directed to it, keeping the old service around for a short period of time, for a fallback
  * you need to be able to redirect traffic - via dns, or via the load balancer
  * you need to be able to provision enough services to handle the load - so twice as many services as normal
  * the entire process can be automated -- with full roll-out, or reversion
  * depending on what mechanism is used for the switch-over - it can be completely transparent
* Canary releasing
  * works similar to blue/green testing
  * works by testing function and non-functional aspects of a service - like response time, and the quality of results (e.g. if a recommendation service provides the same level of quality for recommendations)
  * failures fall back over to the previous version
  * netflix uses this extensively
  * services will coexist longer
  * traffic ramps up gradually as tests pass
  * shadowing
    * one technique is to shadow traffic to the new service. This allows you to see a side-by-side comparison of real traffic
    * this can be quite complex - especially if the results are not idempotent
    * blue/green deployments serves as a foundation
* tools are built to remediate failures - like in canary releasing etc.
  * sometimes it's significantly more beneficial to do this, than to add more tests
  * most organisations spend little time on error remediation or monitoring - which is bad
  * this lowers MTTR
  * it doesn't lower MTBF, just recovers from it - this is a balance between MTTR and MTBF
* sometimes testing is a waste of time - like if you are testing if an idea works, an untested production mvp/alpha may make more sense, rather than committing resources to thoroughly testing a service/idea 

#### 264: Cross-Functional Testing | (aka. Non-Functional Testing)

* most NFT can only be met in production - like performance testing
* NFT falls into the category of property testing
* some NFTs can be done at the service level if there are special requirements
* some tests should be e2e, like load tests, but you should move tests to a smaller scope if you can - obey the testing pyramid
* consider NFTs early on - don't leave it too late
* review them regularly
* performance testing
  * a service may make several db calls, and depend on other services that do the same thing, which can severely affect performance
  * don't fall into the trap of delaying performance tests until the system is complete
    * [personal]: perhaps stubbed services can be made to response with the maximum SLA time - remembering that cascading calls also add on a response time for each hop, so you have to be careful to not assume that the actual response will be within the SLA, and to not depend on too many hops 
  * you may be able to use e2e journey tests as performance tests als
  * you should test increasing loads, and measure the response time - which will take a while to run
  * can produce false negatives or false positives
    * [personal]: i'm assuming other factors like network latency, poor driver, or some OS issues within the test environment can cause test results to be incorrect
  * create target numbers, expectations, and measure against them
  * should be done before deployment and also as a continual monitoring process

#### 267: Summary

* Optimise for fast feedback, separate types of tests (e2e, service, unit etc.) accordingly
* Use CDC
* Avoid e2e test where possible
* where applicable, accommodate a lower MTTR (remediation) over increasing MTBF (extensive testing)

### 8: Monitoring

* monitor the small things, and use aggregation to get the big picture
* [personal]: this chapter appears to be about metrics, not logs

#### p269: Single Service, Single Server

* nagios or new relic are monitoring solutions to check out
* what to monitor
  * the host - cpu, memory - other important host logs
  * user reported errors
  * the application - response times, number of errors
    * [personal]: errors

#### p270: Single Service, Multiple Servers | (i.e. behind a load balancer)

* what to monitor changes here
  * is 100% CPU something to be flagged? Given that this is normal in an elastic setting
  * is it just 1 or 2 hosts that are 100% CPU - is it a rogue OS process?
  * the solution is to aggregate stats from all hosts, but still collect for individual hosts so that you can drill down
* in a very small setting you can use an SSH multiplexer to grep the logs of multiple services
* you can get aggregate response time from the load balancer itself

#### p271: Multiple Services, Multiple Servers

* central aggregation from multiple services 

#### p272: Logs, Logs, and Yet More Logs...

* logstash is a specialised system for centralise log system
* kibana allows you to search the logs, and view them

#### 273: Metric Tracking Across Multiple Services

* Graphite
  * is a metric tracking system with a very simple API
  * compresses old metrics by averaging them (reducing the resolution) over a given period of time - which is configurable
  * allows you to view the entire system, individual service, or groups of services
* important for capacity planning

#### 274: Service Metrics

* You should probably collect response times, error rates, and any other behaviour related metrics you wish to collect - like a count of the number of transaction, or requests to a particular feature etc.
  * 80% of software features are never used, so it's nice to collect service data for insights
  * other well used features also give good insights
* err on the side of "expose everything" 

#### 275: Synthetic Monitoring

* Lower level services will produce a lot of metrics (hence why it's suggested to have aggregate, grouped, or individual service views)
* Their approach was to generate a fake event every minute, monitor it, and have the result appear in a "junk" destination
  * they monitored a response time (not network latency, but computation time)

#### 276: Implement Semantic Monitoring | (aka. Synthetic Monitoring)

* reuse e2e tests - whole system, or individual service e2e tests
* if your system is dynamic in some way, you may need to set up fake data - specifically for semantic monitoring
* avoid real side-effects - like a real order etc.

#### 277: Correlation IDs

* Zipkin is a distributed tracing tool, but it has heavy requirements (custom client etc.), it's very advanced but a recommendation was to trace using existing logged data, which isn't possible with Zipkin
* always include correlation IDs from the beginning, as they are hard to retrofit.

#### 280: The Cascade

* You need to monitor the integration points to downstream services
  * databases, services etc.
  * the data should be aggregated, and at an individual level
  * monitor response time, and errors
* use the circuit breaker pattern
  * you will need a dedicated library to monitor the link, and break the circuit
  * Hystrix was a lib for the JVM

#### 281: Standardization

* You need to view your system in a holistic way (aggregated)
  * [personal]: and also at a very granular way
* monitoring narrow points like a load balancer, or api gateway is good for holistic views
* determine what should be metrics being monitored should be holistic, and what should be granular
* standardization across all services is crucial for monitoring
* use application libraries (interfaces/adapters) to talk to services like graphite
* preconfigured vm images like logstash and collectd go a long way
  * [personal]: not sure why this is the case, won't this create coupling to a specific tech?

#### 282: Consider The Audience

* what they need right now: information that should be highly visible, and available
* what they might want later: must be easy to get
* how they like to consume data: read a book on data visualisation

#### 283: The Future

* he doesn't speak favourably of data warehousing - "where the data goes to die"
* different metrics systems allow for real-time monitoring, some do not.
* All metrics should be collected by the same service, processed, and routed elsewhere - Suro does a good job at this, Riemann is another choice.
  * [personal]: TODO: this may not be necessary. Investigate the role of these services, and determine if they are required
* Apache Storm can be used to process the routed metrics

#### 284: Summary

(Some of the summary has been skipped if there's no need to distil points already made)

* aggregate host metrics with application level metrics
* maintain data long enough to understand trends
* understand what requires a call to action, and make this data very easy to access
* generic, event processing systems allow you to view your system in a more holistic way

### p347: Microservices at Scale

#### p348: Failures Everywhere

* failure becomes a statistical certainty at scale - the more moving parts you have, the more likely failure will occur
* understand and follow the "fallacies of distributed computing"
* handling failures gracefully means you can do in-place upgrades easier
* handling failures means you spend less time preventing the inevitable 
* everything can and will break - inevitable - including hardware

#### p349: How Much is Too Much?

* don't over engineer things that aren't critical to have said properties - like scaling, robustness etc.
  * your choices should be driven by the users of the system - their need, and numbers
* define some general non-functional requirements, ans override them on a case by case basis
  * response/latency: how long? e.g. 90th percentile response in 2 seconds, for 200 concurrent users
  * availability: can it be down? how long? is it a 24/7 service?
  * durability of data: is data loss acceptable? how much? how long is it kept? security?
  * frequently test and monitor these with performance tests

#### p351: Degrading Functionality

* one crucial property is the ability of the whole system to continue functioning even if one service is down
  * the shopping cart might be down, but customers should still be able to browse the web page
  * this is referred to as safely degrading functionality
  * understand the business context (what the service does), its impact, and how to degrade functionality in a meaningful way

#### p352: Architectural Safety Measures

* a cascading failure occurs when one service brings down a whole chain of services
  * one example of this is a downstream service taking too long to respond. If not properly dealt with this can cause each service to timeout too often, and for too long - causing a cascading failure
* HTTP connection pools can be saturated when a service connection is timing out
  * timeout quicker
  * use a circuit breaker
  * consider a separate pool for each service - that way there is no single point of failure - aka bulkheads
  * [personal]: do tests under load, test that service outage is handled properly
* systems that act slow are harder to deal with than systems that fail fast - latency kills

#### p354: The Antifragile Organization

* DiRT: Disaster Recovery Test - Googles Program
  * tests recover from large scale disaster - like earthquakes 
  * [personal]: it might be worth having a test suite, at least, that tests resilience
* Netflix uses applications to deliberately sabotage part of their service in production - so that teams are always ready, and well practised.Netflix calls these the Simian army of failure bots
  * Chaos Monkey: shuts off single services
  * Chaos Gorilla: shuts down an entire availability server - aka. data centre
  * Latency Monkey: increase latency between services
* timeouts
  * put on all out of service calls
  * get it right - not too short, or too long
  * timeouts that are too long can cause cascading failure
* circuit breakers
  * it's up to you to determine what a failed request is, but a good start is a timeout or http 5XX error
  * ensure that the service is healthy again before reconnecting the breaker
  * don't break the circuit too easily, nor too late
  * for asynchronous requests you can queue them up, until the service is back up
  * for synchronous requests: fail fast
  * you can manually blow circuit breakers for maintenance
  * circuit breakers can also fail for high latency etc.
  * should be applied to at least all of your downstream synchronous calls
* bulkheads
  * separating parts of the system to reduce risk of complete failure
  * one example is a separate threadpool for each service, so if one gets exhausted it doesn't take down the entire system
  * microservices are a bulkhead pattern in principle
  * look at aspects that can go wrong with your system, both inside the services and between them - can you insulate each part from each other?
  * circuitbreakers automatically seal a bulkhead
* sometimes rejecting requests is a good way to ensure that you don't saturate your system
* isolation
  * use integration techniques that allow for downstream services to down (failed)
    * builds resiliency for planned/unplanned outages
    * results in less coordination needed between teams

#### p362: Idempotence

* good for replaying messages when you aren't sure if they have been processes or not
* an example of a lack of idempotence is adding loyalty points to an account for a purchase. It's easy with a single call for +100, but each subsequent call results in an accumulated value
  * this is problematic for collaborating services, perhaps one of the services didn't get the message, they might not be consistent with each other - which means you will have to run and perform some consistency checks
  * if the initial call was idempotent, the +100 could only be accepted once, and each service can safely assume that they are consistent with each other - assuming that there is some eventual consistency for services that go down, and the message can be safely replayed (because it's idempotent)
* an example of an idempotent is adding +100 loyalty points to an account, for a purchase, but also including the purchase ID
  * this way the points are attached to a specific purchase, and can only be done once.
  * replaying this idempotent message means it's subsequently ignored (but the call should probably be logged)
  * providing two pieces of information essentially makes the transaction unique, and much easier to identify as having being completed or not
* works well for event-based collaboration
* works well for a number of the same services subscribing to the same events
  * there are small windows where more than one worker may pick up the same message - but idempotence ensures this isn't a big issue 
* http verbs (GET,PUT etc.) are considered idempotent, which means you should use/design them in an idempotent manner 
  * user expect that multiple calls do not result in multiple results

### 12: Bringing It All Together

* Each of the following subheadings are important principles for building microservice architectures
  * you are encourages to define your own principles too


#### p413: Model Around Business Concepts

* Model the domain
* Use business bounded contexts to define domain boundaries
  * business bounded contexts are more stable than models around technical concepts
* not all bugs will be found, you need effective monitoring and remediation in production
* a shared thin client library, with some behaviours for pushing messages, but some preconditions ensuring some important fields are present, like a correlation ID.
  * keep this very thin, and do not couple it with a specific service implementation and its message format

#### p414: Adopt a Culture of Automation | (e.g. deployment automation)

* front-load effort to create tooling
  * like a unified deployment CLI - which makes people's lives easier
* think about custom images - which speeds up deployment
* think about fully automated immutable servers - which are easier to reason about 

#### p415: Hide Internal Implementation Details

* modelling bonded contexts allows teams to focus on models that should be shared
* hide the service database - which creates coupling
* use data pumps to consolidate data, from multiple services, for reporting purposes
* Use technology agnostic APIs - like REST

#### p416: Decentralise All The Things | (aka distribute responsibility)

* delegate all decision making to teams that own the service
* where some overarching guidance is required (in special cases) use a shared governance model - allow teams to collaborate on things that concern everyone
* avoid approaches the following approaches:
  * enterprise service bus - a central, unified messaging system - leads to centralised business logic
  * orchestration - a mediator - which leads to dumb services
* prefer these approaches which help to keep service business logic highly cohesive:
  * choreography
  * dumb middleware
  * smart endpoints

#### p417: Independently Deployable

* Services should have very low coupling
* Consumers shouldn't have to redeploy when a new service is deployed
* Use coexisting versioned endpoints - allow consumers to update over time
* RPC can result in tightly bound client/servers
* on service per host reduces potential service side effects when deploying
* Use consumer driven contracts to catch breaking changes

#### p418: Isolate failure

* Expect failure anywhere, and everywhere
* Downstream calls can and will fail
* network calls are not local calls, there are different reasons for failure - so don't hide this
* Don't over abstract client libraries - don't hide network failures by trying to make remote calls interchangeable with local calls
* solutions
  * bulkheads, circuit-breakers, time-outs
* Understand when to sacrifice availability or consistency 

#### p419: Highly Observable | (aka Logging, Testing, Tracing)

* Use a "joined up view" of all services when observing
* Aggregate logs, and stats - use a single location/service
* Use semantic monitoring a.k.a. synthetic monitoring
  * (periodic automated tests against live services + logging)
* Use correlation IDs - like UUID 
  * [personal]: perhaps a count of the number hops would also be a good idea

#### p420: When Shouldn't You Use Microservices

* when you don't understand the domain - which means you will be unable to define bounded contexts
* You should start as a monolith - it's easier to define boundaries with something that already exists

## Glossary

* choreography: each service acts in unison via having a unified API - this allows services to communicate directly, without an orchestrator [\[source\]][6][\[source\]][7]
* consumer driven contracts: a contract between client and provider, where the provider uses a test suite to ensure the contracts are obligated [\[source\]][3]
* correlation id: an ID given to a transaction, that can be use to trace correlated logs through the system - typically UUIDs. An example is a customer order, where each order is given an ID, and that ID persists through the entire lifetime of the transaction across the network [\[source\]][2]
* data pump: TODO 
* HATEOAS - Hypermedia as the Engine of Application State: REST/JSON objects that embed URIs to such effect that clients do not need to know how to interact with a server, because all the appropriate information is provided in other words, embedded URIs [\[source\]][9]
* Hypermedia: An extension of hypertext to include media [\[source\]][8]
* Hypermedia controls: A REST response that sets the href and rel properties inside data elements of a hypermedia format, with URIs, that point to remote resources for state transitions. [\[source\]][10][\[source\]][11]
* Hypermedia format: A document (XML, JSON HAL...) that describes what should be done with the remote resources fetched via hypermedia controls, by using the href and rel props. [\[source\]][10][\[source\]][11]
* journey: TODO
* Lock-step releases: deploying all services at the same time, as part of the same build
* MTBF - Mean Time Before Failure: The mean time before a failure occurs. Calculated by defining a time-frame, determining the number of failures, and calculating with uptime / failures = MTFB - downtime is not part of the calculation [\[source\]][12]
* MTTR - Mean Time To Repair: the mean time it takes to repair a service/product over a defined period of time. total outage time per period / number of outages = MTTR
* orchestration: a number of services need a conductor (orchestrator) to control and organise communication between services [\[source\]][6]
* semantic monitoring aka synthetic monitoring: running a subset of automated tests against a service, regularly, to find problems. The results are gathered in logs, and continually monitored. [\[source\]][1]
* system message bus: a central message system that has a unified interface. It handles routing, security, monitoring, transformations and more. It becomes a single point of failure, can be complex, and be slow. A federated solution is used to combat a single point of failure. [\[source\]][4][\[source\]][5]

## Notes

* The author refers to services being overly chatty, I think it means too much traffic, or syn requests - such a thing can degrade performance.
* sunk-cost fallacy

[1]: https://techbeacon.com/enterprise-it/semantic-monitoring-why-its-great-microservices
[2]: https://hilton.org.uk/blog/microservices-correlation-id
[3]: https://thoughtworks.github.io/pacto/patterns/cdc/
[4]: https://www.youtube.com/watch?v=VHzWswQNtgk
[5]: https://en.wikipedia.org/wiki/Enterprise_service_bus#Key_disadvantages
[6]: https://www.youtube.com/watch?v=cYENNwDK2dA
[7]: https://en.wikipedia.org/wiki/Service_choreography
[8]: https://en.wikipedia.org/wiki/Hypermedia
[9]: https://en.wikipedia.org/wiki/HATEOAS
[10]: https://developer.paychex.com/api-documentation-and-exploration/documentation/documentation/hypermedia-controls
[11]: https://apisyouwonthate.com/blog/rest-and-hypermedia-in-2019
[12]: https://www.atlassian.com/incident-management/kpis/common-metrics
