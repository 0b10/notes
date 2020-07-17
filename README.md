# Notes

## TOC

1. [Dev](dev)
    1. [Cloud](dev/cloud)
        1. [Object storage](dev/cloud/object-storage.md): A cost-effective, scalable, binary storage solution.
        1. [Serverless](dev/cloud/serverless.md): A very scalable, on-demand solution for bursty requests and processing.
        1. DigitalOcean
            1. [Provisioning with Terraform](dev/cloud/misc/digital-ocean-infrastructure.notes.md): Use Terraform and learn some architectural basics.

## Study Path

### Sequence

1. Cloud / hosting
1. Agile
1. HTTP
1. CSS
1. SCSS
1. HTML
1. Project management
1. Databases
1. Testing
1. Wordpress

### Development

#### Messaging

* What are the different messaging systems out there?
    * What are the benefits of each one?
    * Which are the simplest and easiest to implement and maintain?

#### Databases

* What are the different databases out there?
    * What are the use cases for each database type?
    * How is each database type categorised?
    * What are strengths and weaknesses of each database type?
* How to architect a database?
    * How to do data modelling?
        * What tools are used?
    * What are the best practices?
* SQL
    * What is the strength of SQL? 
    * What are the best frameworks/ORMs/query builders for Node?
    * What are the best security practices?
    * How to build efficient queries?
        * How to leverage indexing?
        * What do bad queries look like?
    * How does data modelling affect query efficiency?
* General
    * How to use triggers?
        * Why would you use triggers, what are some common use cases? 

#### CI/CD

* What are the differences between continuous delivery, continuous deployment, and continuous integration?
* What are the best approaches for each?
* What are the differences between the tools for each?
* What are the benefits for each?
* When to use each?
* How does Gitlab fit into all of this?
    * How does it compare to competition?
    * How much is Gitlab?

#### CDN

* How to CDNs work?
    * How do they relate to object storage, is there a relation?
    * How much do CDNs generally cost?
    * How is a CDN integrated with a web app?

#### Cloud

* What are the differences between each cloud provider offering?
    * What are the pros and cons between each platform?
        * What are the limitations for each platform?
        * What are the benefits for each platform?
        * What database types are supported for each platform?
        * How does each platform do scaling?
    * Which platforms are affordable for new businesses?
    * Which platforms require orchestration?
    * Which platforms cause vendor lock-in?
    * What do you lose by not using AWS?
* How to avoid vendor lock-in?
    * What technologies are used?
    * What can be migrated, and what cannot?
    * Can some vendor offerings be abstracted to provide portability?
* Use a managed scaling solution, or manually implement one?
    * What are the different scaling solutions?
    * How much work is it to manually maintain scaling infrastructure?
        * How much code is required?
        * How is it tested?
    * What are the costs for managed scaling?
        * Can it be done without vendor lock-in?
        * Can it be affordable?
* Serverless?
    * Can vendor lock-in be mitigated?
    * Why is monitoring and debugging harder?
* Kubernetes
    * What problems does it solve?
        * What are its range of features?
    * How does it differ from a load balancer?
    * How complex is it to set up and use?
        * How hard is it to maintain?
        * How much effort is it to implement?
        * Can some of the complexities be reduced, or eliminated?
    * What are its strengths and weaknesses?
    * Who uses it?
    * How does it work underneath?
    * What are the alternatives?

#### HTML

* Accessibility
    * What are all of the supported elements?
    * What are the best tools used to assessing accessibility?
        * Is there a framework for assessment, if not, develop one?
    * What are the key takeaways form WCAG? 
* What are ALL of the elements, and their function?
* What are the best industry practices?
* What are the best frameworks, and tools?
* DOM
    * What are the most commonly used events?
    * What are ALL of the events, and how what is a good reference resource?
    * How to get data from a form?
    * How does the shadow DOM work exactly?

#### HTTP

* What does the HTTP spec look like?
    * What are the various headers, and their significance?
        * What are the most common headers?
        * What are the most important headers?
        * What kinds of authentication use headers?
        * Authorisation header
            * How does it work?
            * What are its weaknesses and strengths?
            * Who/what typically uses it?
            * How commonly is it used?
    * What are the various response codes?
        * What are the most common codes?
        * How are the codes used exactly by the browser? (besides displaying an error code)
    * What are the differences between spec revisions?
        * How commonly used is each revision?
        * Should new apps focus on newer revisions?
        * How do old browsers factor into this?
        * What are the security benefits between each?
        * What are the security drawbacks between each?
        * Are there any efficiency gains/losses between each?
        * What are the use cases, or justifications, for using each?
            * Should older revisions be considered for older browsers?
* What is CORS?
    * What is its use case?
    * How to side-step CORS for development?
    * How to develop a secure CORS policy?
        * Is there a framework?
        * What specifically enables cross origin requests?
    * What are browsers' default behaviour with regards to CORS? 

#### Project Management

* How does project management work?
    * What are the best tools?
    * How to create time estimates?
    * How to manage people for projects?
    * What are the different approaches?
        * How does agile work?
            * What are the primary concepts of agile?
            * How does agile work for a solo developer?
            * Is it a strict process, or can parts be selectively used?
            * What tools are available for agile?
                * What categories of tools exist?
                * Which are commonly thought of as the best tools for agile?

#### Security

* IAM
    * What is IAM?
    * What makes use of IAM?
        * What services, platforms, software, architectures do/should use IAM? 
    * Is there a standard set of tools to use for IAM - if so, what are they?
        * What tools are used for what particular job? 
    * How is IAM utilised for internal calls within the cloud?
        * Is this a necessity for all calls?
    * How do microservices use IAM?
        * Should all inter-service communications use IAM, at all times?
    * What are the use cases for IAM?
        * When should it be used?
    * Is there a better approach?
    * What are the drawbacks of IAM?
    * What are the benefits of IAM?
* Authentication
    * What are the different authentication methods?
    * What are the pros and cons for each?
    * What are the caveats for each?
    * How easy is it to implement each?
    * How secure is each?
    * What are JWTs?
        * Are they the recommended way to authenticate with a server?
    * What is the recommended way?
        * What is the least likely to result in security issues? 

#### Style

* CSS3
    * What are the main features?
        * How to use variables?
* SCSS 
* Boostrap
    * (v5): What is the utilities API?
    * How does SCSS fit in?

### Business

* What are the most relevant business models?
* How to model business processes?
* How to write a business plan?

#### Growth

* How to grow a business?
    * When to grow a business?
    * Do I need a growth team?
        * How to structure a growth team?

#### Management

* What's involved in business management?
    * What are the roles and functions of business management?
    * How does one create efficient management systems?
        * Are there standardised techniques?
    * How does one effectively manage people?
    * What makes a good hiring process?
        * What are the implications of bad hiring practices?
        * How does one hire the right people?

#### People

* What are the functions of executives?
    * What are all the executives titles?
    * What kind of skills do executives need?

#### Marketing

* How to market a business?
    * What are the best marketing channels?
        * When to use specific marketing channels? 
    * How to write copy?
        * What, if any, are the legal restrictions/considerations for copy?
    * How does one conduct market research?
        * What are good source for market research?

#### CRM

* What is involved in customer service?
    * How to create good CRM?
        * How does a CRM work?
            * How does CRM fit into other business systems?
            * What benefits does a CRM bring?

#### Founding

* What is expected of founders?
    * How many hats should a founder wear?
    * Can solo founders succeed?
* How is a business legally created?
    * What is incorporation?
    * What are the different business types?
        * What are the legal benefits for each business type?
    * How much does creating a business initially cost?
    * How does a business operate in multiple countries?
        * How can this process be made easier?
        * What are the legal considerations?
    * What are the supporting structures for creating a business?
        * Does the business need legal representation?
        * Does the business need liability insurance?

#### Financial

* How are finances managed?
    * What are the tax obligations?
        * How are the obligations determined?
    * How does bookkeeping work?
* How does a business get funding?
    * Are there any technique, or expected approaches for a pitch?
        * Are there any frameworks or templates for making a pitch? 
