# Key Takeaways

* Start with meeting a target market needs, not an idea/solution
* Make/refine hypotheses based on data, then test is
  * Use a data driven approach to measure customer satisfaction
* Iteratively model your customer with personas, express your hypotheses
* Deeply understand the customer needs, and be very pragmatic.
* Use iterative interviews/surveys to dig deeper
* Define the product value proposition as a list of needs to be addressed
* Focus on a small set of the most important needs, reducing risk -- say "no" lots.
* The goal of an MVP is quick development, and fast feedback. You can test if an idea will take off, and minimise cost and risk if it does not
* Selecting features for an MVP is a balance between high opportunity (demand) features, and cost of implementation -- it's a measured and purposeful process
* Test and iterate on the product layout, user interaction, general experience and visuals -- gauging on usability and delight
* Bridge the feature set with design metaphors (aka conceptual model), you must deeply understand the target users

# Part I: Core Concepts

### Chapter 1 & 2: Achieving PMF & Problem Space vs. Solution Space

* [Mindmap](part-i-core-concepts/mindmap.png?raw=true)
* [PMF Pyramid][pmf-pyramid]

When attempting to follow this process keep this in mind:

> Obey principles without being bound to them -- Bruce Lee

> Adapt what is useful, reject what is useless, and add specifically what is your own -- Bruce Lee

### Market

A market can be defined by existing customers, potential customer, or by customers that have problems in common.  You can determine the current (or future) market size through determining the total market revenue, or by the number of customers. You should avoid happy markets, and target markets with problems that need to be solved instead.

Competitors form market segments, and you can segment the market with any metric, need, or product you see fit.

Sometimes you can create a new market, creating solutions to problems that nobody has solved yet.

### Product Market Fit

The goal is to ream PMF as soon as possible. Do as little rework as possible by being rigorous and thinking quickly. 

The top half of the [PMF Pyramid][pmf-pyramid] must satisfy the bottom half -- the product must satisfy the market.

The book isn't clear on how iteration should occur, but it explicitly states that an iteration should follow through the entire [PMF Pyramid][pmf-pyramid]. However, the book also implies later that each layer should be iterated upon individually, and have its hypotheses fully validated before moving onto the next layer -- which is actually critical to avoid costly rework.  The book also hints at revisions (major versions), which translates to a complete pass through the pyramid (ignoring some lower layers if necessary).

The book also talks about problem/solution space, and explicitly states that the problem space (target customer, understand needs, value proposition) should be fully understood before moving onto the solution space (feature set, UX). This implies that the problem space should be iterated upon, as a whole, then the solution space once the former has been fully validated.

In conclusion, I think it's a bit of both - iterate on each level as best you can, iterating on the problem space and fully validating it first, then moving onto the solution space.

### Solution Space vs. Problem Space

> Customers don't care about your solution. They care about their problems -- Dave McClure

The problem space should be fully understood before proceeding to the solution space. The problem space can be understood via customer discovery techniques (aka contextual inquiry) like interviews, observation, questionnaires etc.

With the problem space you define problems, not solutions -- the NASA pen is an example: "a need to record notes in space" is the problem, the NASA pen is a solution, hence the pencil being overlooked.

The problem space focuses on *what* the product needs to achieve (needs, desires, pain points, and wants), and targets the *target customer*, underserved needs, and value proposition layers of the [PMF Pyramid][pmf-pyramid]

The solution space focuses on *how* it will be achieved (ideas, design, prototypes, product/MVP), whose artefacts are the feature set and UX layers of the [PMF Pyramid][pmf-pyramid].

The value proposition is the bridge between the problem and solution space.

You can use the solution space to define the problem space through observing customers using current solutions, observing and recording their pain points.

The problem space is usually best defined via your own prototypes/artefacts.

### Hypotheses

Hypotheses should be formed for each layer in the [PMF Pyramid][pmf-pyramid] -- e.g. a hypothesis on the customer's underserved needs,  the value proposition they'd receive well, the feature sets they want etc.

Articulate a hypotheses, and solicit feedback.

### Misc

The product strategy is really a determination of how the product will be better than competitors -- how each market need is met, a determination made through validated learning -- the feature set.

# Part II: The Lean Product Process

## Chapter 3: Determine Your Target Customer

* [Mindmap](part-ii-the-lean-product-process/3-determine-your-target-customer/mindmap.png?raw=true)
* [Adoption Life-cycle Notes][adoption-lifecycle]
* [Persona Template][persona-template]

### Summary

You must target a specific market - a group of potential customers with specific attributes -- called a market segment. Understand your customer's profile (needs, wants, attributes) and model them early.

To model them you would use personas. Personas allow you to capture your hypotheses in a more tangible form. Personas are not real people, but are based on individual real customers, and are never an average or generalised profile.

Personas can be derived from data captured through interviews or surveys. Another source for personas can be the ["technology adoption lifecycle framework"][adoption-lifecycle]. You should understand the development stage your product is in, and the kind of customer it's likely to attract -- via the aforementioned framework.

* The target customer
  * Product development should be driven by the customer's needs
* Market
  * Markets are groups of people bound by some common attributes - demographics, psychographics, behavioural characteristics, and needs.
    * The business equivalent of demographics is firmographics
  * Market segmentation occurs around common attributes of customers
  * Determine a market segment to target -- this may require higher level reasoning outside the scope of this book
  * The economic buyer may not be the person using the product, and the user may influence the economic buyer
* Technology adoption lifecycle
  * A simple framework for understanding customer personalities, relative to new technology adoption
  * Understand what stage your product is in, and determine who will typically be adopting it
* The technology adoption lifecycle is a simple framework 
* Personas
  * Used early to capture hypotheses about the target customer
  * Represents real people, not averages -- hypothetical archetypes of actual users
  * Iterate until they are accurate -- pragmatic
  * Use a [template][persona-template] and fit it on a single page
  * Capture attributes like demographics, psychographics, behavioural, and needs
  * You can source information from interviews or surveys

## Chapter 4: Identifying Underserved Customer Needs

* [Frameworks](part-ii-the-lean-product-process/4-identifying-underserved-customer-needs/customer-discovery-frameworks.notes.md)
* [Mindmap](part-ii-the-lean-product-process/4-identifying-underserved-customer-needs/mindmap.png?raw=true)
* [Activity Diagram](part-ii-the-lean-product-process/4-identifying-underserved-customer-needs/activity-diagram.png?raw=true)
* [Laddering Notes][laddering]

### Summary

Initially, you will make a guess at a set of hypotheses. You will then derive a set of customer benefits, prepare questions, and conduct an interview.

The purpose of the interview is to test hypothesis against the declared benefits through carefully created question. Questions measure the importance and satisfaction with each proposed benefit -- relative to competition, and to discover new needs. Use techniques like [laddering][laddering] to discover related benefits, or common root benefits. The newly discovered benefits feed a revised set of hypotheses, from which a revised set of benefits is derived.

Plot and reason about the data, systematically discover opportunities, and repeat the entire process until statistical opportunities are at a point of high importance, and high satisfaction (which has been captured relative to the competition).

* Hypothesis
  * Initially a guess when there's no data to go on
  * Create a set of hypotheses, each one serves as a foundation for a benefit 
  * Derived directly from customer feedback -- their needs and pain points
  * Focus on the problem space (no solutions permitted)
  * Are there related needs? Common root need?
* Benefits
  * Are needs written from the perspective of the customer
  * Derived from hypotheses, each hypothesis underpins a benefit
* Interviews
  * Are used to test hypotheses - how true are they?
    * (Adequate questions are defined in the mindmap and activity diagram)
  * Comparing to competitors means the data reflects relative quality
  * Determine goals/needs and pain points
    * [Laddering][laddering] helps to uncover common root,or related needs
      * Recursively enquiring about answers until you hit an atomic need -- go deep
      * This can simplify the hypothesis (common root), or reveal a set of related needs -- needs that must be addressed together
  * Importance and satisfaction are used to assess opportunity -- further research and development 
* [Frameworks][customer-discovery-frameworks]
  * Plot importance/satisfaction
  * Use to track progress, and reveal opportunity
  * Opportunity is low satisfaction, high importance -- high importance is paramount 

## Chapter 5: Define Your Value Proposition

* [Mindmap](part-ii-the-lean-product-process/5-define-your-value-proposition/mindmap.png?raw=true)
* [Value Proposition Template][value-proposition-template]

### Summary

In order to define a successful value proposition you need to focus on **high importance/high value** needs -- it's not worth your time pursuing needs that are already met with high satisfaction. Focus on a small set of needs to reduce committed resources, and reduce risk in case of a product failure.

These needs, when structured with the [Kano model][kano-model] will be categorised into three sets. The most competitive category is the performance benefits, in which you will focus on the most importance benefit. You must be better than your competitors for that benefit, and you must also at least match all other performance benefits to overcome the competition. Must-haves are non-negotiable, and form a critical dependency for your product. Markets with high satisfaction are hard to dethrone the competition. 

Use the [value proposition template][value-proposition-template] to clarify your product benefits, and easily compare them. The list of benefits for your product form your value proposition.


* Needs
  * [Kano model][kano-model]
    * Must-haves
      * Non-negotiable, and you must match your competitors
    * Performance
      * How the product performs -- not just in speed, but in results, latency, effectiveness, UX and a number of other areas
      * You must at least match all of your competitors performance benefits
      * You must win on the most important benefit, with respect to your competitors -- as determined through customer data
      * This is where the competition is, and is the most important category of benefit
    * Delighters
      * Unique features not offered by your customers
      * Provides extra value
      * Not as important as performance
  * Focus
    * An MVP reduces risk -- if you get it wrong, not too many resources have been committed 
    * Focus on eliminating benefits until what you are left with is a small subset of the most important benefits -- as defined through customer feedback/data
    * Don't commit too many resources -- reduces risk 
    * Only focus on **high importance**, **low satisfaction** needs
* [Value Proposition Template][value-proposition-template]
  * The benefits defined by your own product is its value proposition
  * You can use the template to make projections -- aka "product strategy"

## Chapter 6: Specify Your MVP Feature Set

* [Mindmap](part-ii-the-lean-product-process/6-specify-mvp-feature-set/mindmap.png?raw=true)
* [Activity Diagram][mvp-features-activity-diagram]
* [Prioritised Feature Chunk Table][prioritised-feature-chunk-table]


### Summary

You first want to focus on a subset of features from the value proposition. You will use the chosen features in a brainstorming session, and formalise them in user stories -- this makes them testable with user acceptance testing, and keeps them clear.

Next you will "chunk" the user stories into smaller scope, which decreases the risk due to a smaller scope and faster feedback time. It's also easier to understand and estimate smaller stories. A priority should be assigned to each chunk, either a customer derived importance statistic, or a developer projected user importance rating. Chunking only stops when all chunks are atomic.

You will then process them by categorising them by their associated benefit, accept or reject them based on their feasibility, and prioritise them via an ROI. Once you have processed them you are to select the top 3-5 priority stories per benefit -- considering any dependencies.

Finally you will organise all of the features in terms of their priority, and category in a ["prioritised feature chunk table"][prioritised-feature-chunk-table]. All of the must-haves, the top performance benefit, and the top delighter will form the features for the MVP.

* User stories
  * Used the capture features in brainstorming sessions
  * Keeps customer benefits clear, and discrete
  * Testable via user acceptance testing
  * INVEST: independent, negotiable, valuable, estimable, small, testable
* Priorities
  * User define importance assigned to each benefit -- through data collection
  * Projected user defined value, assigned by the developer
  * ROI - derived from value/cost, where the value is projected customer value, or actual customer importance, and cost is any relevant metric -- like story points, time, revenue etc.
* Brain storming
  * Use divergent thinking - get ideas down, don't worry about viability (within reason) or cost etc.
  * Produce a number of ideas per benefit
  * Address each benefit
  * Capture ideas in the form of user stories
* Story points
  * A value that estimates the cost of implementing a certain story
  * Assigned story points over a certain threshold means the story is chunked
* Chunking
  * Subdivide large stories into smaller stories
  * Reduces the scope
  * Makes them easier to reason about and estimate
  * Faster feedback, reduces the risk
  * Assign priorities and scope to each new chunk
* Capture/Process
  * Review: are they viable?
  * Score: user story points - which convey the difficulty of implementing the feature
  * Organise: arrange ideas with their associated benefit
  * Prioritise: this is ROI = value/cost, which is ratio between the customer value and the cost of implementation -- time or development cost, like story points. Any metric can be used for the cost.
* [Prioritised feature chunk table][prioritised-feature-chunk-table]
  * Based on the [Kano model][kano-model], and used must-haves, performance, benefits, and delighters
  * Each benefit has a number of features/user stories associated with it
  * Features/user stories are assigned a priority, and features/stories of high priority align to the left
  * It's important to use an adequate metric for priority -- ROI is a good candidate

### Notes

What I don't like about this process: brainstorming, chunking, and processing features that are of lower customer importance.

Since you will have the data, a more efficient approach would be to select only the necessary features of the highest customer importance, before processing.

Using the [Kano model][kano-model], choose:
* Must-haves
* Most important performance benefit
* Most important delighter

However, this has some drawbacks:

1. You won't get a high level overview of all the features, their scope, and priority
1. The prioritised feature chunk table will organise features based on their customer value, and cost of implementation -- which means lower priority features will naturally not be implemented first.

This idea means less up-front planning, so less risk when needs inevitably change, but it also means a smaller overall picture.

## Chapter 7: Create Your MVP Prototype

* [Mindmap](part-ii-the-lean-product-process/7-create-your-mvp-prototype/mindmap.png?raw=true)
* [Activity Diagram](part-ii-the-lean-product-process/7-create-your-mvp-prototype/activity-diagram.png?raw=true)
* [MVP Pyramid][mvp-pyramid]
* [Test Categorisation](./part-ii-the-lean-product-process/7-create-your-mvp-prototype/test-categorisation.md)

### Summary

The goal is to initially test market interest in your specific product, its value proposition, and to improve engagement/conversions. Then to iteratively test UX design, until you reach an MVP that suitably attracts interest, and satisfies customer UX needs. To get there, you will need to employ a data-driven approach, with a good balance between qualitative and quantitative sources.

#### Start with Marketing Validation

To start, quantitative data can be collected from marketing materials like landing pages (aka smoke test), crowdfunding engagement, ad campaigns, explainer/product videos. The value proposition should be clear in all cases. To get useful data you should track engagement, from which you will iteratively test new designs/approaches. This whole process should give you insights into interest for the product.

Qualitative data can also be collected from marketing material like landing pages, with methods like the "5 second test". Qualitative data gives you valuable opinions, and direction for new ideas to increasing engagement and interest.

#### Then Move Onto Product Validation

Once you have validated market interest, and your marketing approach, you can move onto product (UX) validation which is all about ensuring the customer sees value.

To validate the UX you should start with a low fidelity prototype, and rapidly iterate on designs moving up in fidelity towards an eventual live product -- the MVP. For each phase you should collect qualitative and quantitative data.

Qualitative data consists of things like customer opinions, and are collected via methods like -- sketches, wireframes, mockups, interactive prototypes, and the Wizard of Oz technique.

Quantitative data can be collected through A/B testing, product analytics, and the fake door technique. Each of which allow you to test engagement in designs, and the effects of changes on key performance metrics -- such as conversion rate.

Eventually you will reach the live product phase, which tests real issues such as latency, load performance, response times etc. The end goal for the live product is to have developed a suitable and complete UX for a **minimum feature set** -- see the [MVP pyramid][mvp-pyramid].

* Deliverable
  * The revised prototype/product, delivered to the customer
* Goals
  * Test/improve market interest
  * Test/improve UX
  * Attain feedback
  * Product-market fit
* Methods
  * Low fidelity
    * Low risk
    * Quick iterations and thus quick feedback
    * Hand sketch, wireframes, mockups, interactive prototype, Wizard of Oz etc.
  * High fidelity
    * Live product
    * Test issues unreachable by low fidelity tests -- performance etc.
  * Other approaches
    * Marketing products
      * Product videos, ad campaigns, emails, landing pages, 5 second test, fake door etc.
      * Track and test engagement with A/B testing, analytics, metrics etc.
    * Crowdfunding
      * Test engagement
      * Reach early adopters
* Data collection
  * Qualitative
    * Small sample size
    * Start here
    * Opinions
  * Quantitative
    * Large sample size
    * Analytics, A/B testing -- behaviour

## Chapter 8: Apply the Principles of Great UX design

* [Mindmap](part-ii-the-lean-product-process/8-apply-principles-of-great-ux-design/mindmap.png?raw=true)
* [UX Iceberg Mindmap](part-ii-the-lean-product-process/8-apply-principles-of-great-ux-design/ux-iceberg.mm.png?raw=true)
* [UX Iceberg][ux-iceberg]
* [Layout Grid][layout-grid]
* [Site map][sitemap]

### The UX Team

UX Teams consist of interaction a designer, visual designer, frontend developer, and a product manager. An interaction designer is responsible for the measuring and developing the interaction between the product and the user. A visual designer is responsible for the look and feel -- which colour, visual hierarchies, placement etc.

### Design Principles

Design principles are used to ensure a proven UX:

* **visual hierarchy** (colour/size/placement/contrast): elements are first ordered by importance, then placed according to guiding principles
* **Gestalt principle**: related elements are placed close to each other, unrelated elements are not, and are also always visually differentiated
* **principles of composition**: unity, contrast, balance, and use of space -- do elements sit well together; do high important elements contrast; is there a visual weight/colour balance; and is there adequate use of spacing?

### Primary Concerns

Two important aspects of UX are usability, and delight. Usability is concerned with efficiency (effort/flow/learnability/cognitive load), ease of use, and the tasks users perform. Usability is achieved through developed personas, and user tested -- through various metrics of interaction, while the user performs user centric tasks and goals.  Delight is concerned with user emotions, aesthetics, simplicity, pre-emptive actions or state -- like smart defaults, personality, and even surprise -- e.g. funny 404 pages.

### The UX Iceberg

The entire UX layer in the [PMF pyramid][pmf-pyramid] can be expressed as the [UX iceberg][ux-iceberg]. The [UX iceberg][ux-iceberg] consists of, in order:

1. **Visual design**: the part that the user sees and is responsible for reinforcing the visual hierarchy, brand personality, user delight and differentiating your product from competitors. The way these responsibilities are achieved is through conveying emotion and contrast with **colour**, style and visual hierarchy with **typography**, **graphics** (which are critical for conversion rates), consistency with **style guides** and [**layout grids**][layout-grid]. Visual design UX is attained through gradually increasing the fidelity of prototypes, eventually reaching mockups -- which provide a rich interactive user experience. Each phase in fidelity is carefully tested, and feeds back into prototype iteration.
1. **Interaction design**: deals with how the user interacts with the product -- input, feedback, navigation (flow) etc. A flowchart can be used to model the interaction and navigation. Wireframes should be used to gather user feedback on the layout, UX, and general interaction. Divergent thinking should be applied to brainstorm *all* ideas (even bad ones) derived from feedback, making sure not to narrow the choice of solutions too early -- test and see. How the user interacts with the product is often tied quite closely to the conceptual design -- e.g. a shopping cart.
1. **Information architecture**: is concerned with the arrangements of feature set elements, optimised for findability -- which is the focus for user tests. A technique to optimise organisation is card sorting, where each element is a card and the user arranges them. Card sorting, and producing the resulting prototype, is an iterative process, and feedback from tests is measured for optimisation. Another technique for optimising findability is through analytics of the prototype, measuring the number of steps/time taken to achieve a goal. A model that can be used to express the architecture called a [site map][sitemap], which expresses the interaction with elements in a hierarchical way.
1. **Conceptual design**: is essentially a design metaphor, and is supposed to resonate with the intended audience in a stylistic or intuitive way -- aiding learnability. A product can implement many conceptual designs -- such as a shopping cart, being only a small part of the product. The conceptual design layers sits just above the feature set layer of the [PMF pyramid][pmf-pyramid], and forms the bridge between the feature set and the itself. Often, this bridge is what drives product innovation. To bridge this gap you have to engage in *deep* user research, building personas -- while modelling the **context** and **technical abilities** in addition to the attributes that personas typically model. User research is conducted through interviews, usability tests, and surveys -- documenting the summary of results and key takeaways, which facilitates and simplifies learning capture. Other team members should be directly involved in the research, like product team members, so that they can observe the results first-hand -- which is a far more effective means to communicate lessons learned when compared to a second-hand report.

## Chapter 9: Test Your MVP with Customers

* [Mindmap][ch9-mindmap]
* [Customer mindmap][customer-test-mm]
* [Activity Diagram][customer-test-ad]
* [Feedback template][feedback-template]

Once you have an MVP built you must test it with [customers][customer-test-mm] to feed the iterative process of feedback and refine.

The purpose of testing is to uncover product blindness (developer bias), and to validate/invalidate the hypotheses about the customer.

### The Customer

You must choose around 5-8 [customers][customer-test-mm] that are members of the target market -- this is very important because choosing the wrong [customer][customer-test-mm] means potentially iterating your product in the wrong direction.

Often-times, discoveries are made about [customer][customer-test-mm] needs, or product features, that will cause you to refine your target [customer][customer-test-mm] [(persona)][persona-template] or the product.

Customers should be pre-screened with a questionnaire to recruit people who meet a specific demographic, and behavioural (and possibly psychographic) profile. [Personas][persona-template] should be used to serve as a base for creating pre-screener questions.

Customers can be recruited from conferences, meet-ups, events, [customer][customer-test-mm] research companies, Craigslist, MTurk, TaskRabbit, UberTesting, freelance websites, or Starbucks etc. -- depending on your target [customer][customer-test-mm] profile, resources, needs, or budget. User testing services generally provide an existing userbase. Refer to the [customer mindmap][customer-test-mm] for more specific details. 

Frequently [customers][customer-test-mm] will not show up for interviews (about 10% of the time) so plan for this, and recruit one extra participant for every ~10.

About 10% of [customers][customer-test-mm] will offer bad feedback -- where they won't be critical, or they won't say much.

### The Interview

Generally, [customers][customer-test-mm] are interviewed on a one-to-one basis, unless there are time constraints. Interviewing [customers][customer-test-mm] in groups is not recommended, because group dynamics (group-think; dominant people etc.) can affect the collected data.

In a moderated setting, the moderator can record the customer's face to get emotional cues, their voice for audio cues, and generally observe the user's interaction in a more detailed way, and probe variances in that interaction. Some of these things are available in a limited way with unmoderated observations, but a lot of "in-the-moment" experience and observation is lost.

User testing services allow you to gather both qualitative and quantitative data, but generally not a one-to-one interview experience -- i.e. they are unmoderated. Unmoderated tests allow you to scale the interviews up and run them concurrently, but the data gathered is less rich -- visual, audio, and emotional cues are not recorded, probing questions are not possible. As a result the questions need to be well thought out beforehand.

Each iteration, or wave of testing, is usually a different set of customers, unless there are participants who have explicitly signed up for further testing, and they are recruited again.

The interview itself consists of a **warm-up**, the **main portion**, and a **wrap-up**, and should follow a **script** -- which denotes tests, tasks, questions, artefacts, and the organisation of each.

The **warm-up** is short and is about building a rapport with the [customer][customer-test-mm] -- which is important to make them feel comfortable.

The **main portion** can be split into two sections: **customer discovery**, and **product feedback**. With **customer discovery** you want to focus on their feelings with the proposed benefits, uncover their needs, specific end-to-end examples of their current solutions or problems, and any information that validates/invalidates the value proposition or [customer][customer-test-mm] hypotheses. The **product feedback** portion is a fly-on-the-wall approach to observing product usage, with the [customer][customer-test-mm] verbalising their thought process, and the observer asking non-leading, probing questions about why the user does what they do.  Most of the questions will be open-ended, and always objective (non-leading).

The **wrap-up** is about getting the users ratings on **usability (UX)**, **product value (PMF)**, overall impressions, a Q&A, and asking whether they are interested in being notified about product release, or being re-invited to another interview session -- these latter questions help gauge whether there is genuine interest in the product.

It's a good idea to pilot tests, to ensure that they are effective before they are put to use.

Customers can be compensated for their time in the form of gift cards, money, invites to
open beta, or swag. $75-$100 per hour is a reasonable amount, depending on the target customer.

### Capture

The recorded data should be categorised as thee distinct categories:

1. **Functionality**
  * Benefits are correct?
  * Features are important / missing?
1. **Messaging / feedback**
1. **UX**
  * Primarily with regards to the feature set

And two smaller, more focused categories -- called key ratings:

1. Usability (UX)
1. Product value (PMF)

See the [feedback template][feedback-template] to understand how these are recorded.

**Usability** questions would looks like: "how easy was the product to use?"; **product value** questions could be "how valuable do you find the product?", or "how likely are you to use the product?".

## Chapter 10: Iterate and Pivot

* [Mindmap][ch10-mindmap]

The iterative process for developing the product can be expressed as **hypothesise-design-test-learn**.

Focus on the most important items, not every problem needs to be solved each iteration -- iterate quickly, and track performance.

Where necessary, you can use brainstorming sessions to dig yourself out of a rut -- e.g. maybe to develop a more effective test script, or during the learning phase, or even the hypotheses stage. Any stage can use brainstorming if it's useful.

There is no hard-and-fast rule to determine when you should stop iterating and move onto the live product -- but when you do, don't forget to test the live product too. Don't get held back by analysis paralysis, move quickly.

### 1: Hypothesise

Start off by defining what the customer wants, derived from uncovered needs. Initially this data isn't available, and the hypotheses is just a guess. The hypotheses is validated via the subsequent phases.

Determine what level of the [PMF Pyramid][pmf-pyramid] each hypothesis is targeting, because you want to start as low as you can (value proposition) and work your way up (UX), making sure your hypotheses are fully validate for each level, before moving on. For example, changing your value proposition when you are validating the UX can be very costly. The lower layers form the foundation for the higher layers, so make sure that you are moving forward with care -- use validated learning to support your hypotheses.

### 2: Design

Create the artefact (wireframes, mockups, or the full product etc.). The goal here is to test the hypotheses in the next phase, and your design/product should reflect your hypotheses, and be testable.

### 3: Test

This is where you measure and record everything. There will be a great deal of qualitative information collected directly from customers to help guide your decision making, this is on top of quantitative data -- like A/B testing, and engagement analytics.

### 4: Learn

Uncover unknowns to feed the hypotheses. Do it quickly, and iterate quickly. Doing it quickly means reaching PMF quicker.

### Pivot or Persevere?

One important question you should keep in mind for each iteration is -- should we continue or pivot?

Pivoting essentially means changing the main hypothesis you have about your customer -- which results in changing your target customer, or changing the differentiators in your value proposition.

You would pivot when your customers don't seem to get excited about your artefact as you iterate; there are better opportunities that have been identified; when only part of your value proposition resonates with your target customers, and pivoting towards that makes sense; a sub-market of your target customers gets exciting, and you focus on them.

The mountain metaphor can be used to visualise a pivot -- each set of value propositions represents a mountain, and the tip of the mountain is PMF. The goal is to find a path to the tip of *any* mountain, which means changing paths/mountain may become a necessity.

Having problems reaching PMF may not always be *having* the wrong hypotheses, but perhaps poor execution of product development, poor marketing, or the product build process could be flawed etc. When you have issues reaching PMF, you should take a step back (before pivoting) and brainstorm potential problems. The aforementioned problems can easily be masked by poor feedback, and the assumption that PMF is just not being reached. So be careful.

[ch10-mindmap]: part-ii-the-lean-product-process/10-iterate-and-pivot/mindmap.png?raw=true
[customer-test-ad]: part-ii-the-lean-product-process/9-test-mvp-with-customers/activity-diagram.png?raw=true
[ch9-mindmap]: part-ii-the-lean-product-process/9-test-mvp-with-customers/mindmap.png?raw=true
[customer-test-mm]: part-ii-the-lean-product-process/9-test-mvp-with-customers/customers.mm.png?raw=true
[feedback-template]: part-ii-the-lean-product-process/9-test-mvp-with-customers/feedback-template.md
[adoption-lifecycle]: part-ii-the-lean-product-process/3-determine-your-target-customer/adoption-lifecycle.notes.md
[persona-template]: part-ii-the-lean-product-process/3-determine-your-target-customer/persona-template.notes.md
[kano-model]: part-ii-the-lean-product-process/4-identifying-underserved-customer-needs/kano-model-framework.png
[value-proposition-template]: part-ii-the-lean-product-process/5-define-your-value-proposition/value-proposition.template.md
[sitemap]: part-ii-the-lean-product-process/8-apply-principles-of-great-ux-design/site-map.gif?raw=true
[pmf-pyramid]: part-i-core-concepts/pmf-pyramid.png?raw=true
[ux-iceberg]: part-ii-the-lean-product-process/8-apply-principles-of-great-ux-design/ux-iceberg.jpg?raw=true
[layout-grid]: part-ii-the-lean-product-process/8-apply-principles-of-great-ux-design/layout-grid.jpg?raw=true
[mvp-features-activity-diagram]: part-ii-the-lean-product-process/6-specify-mvp-feature-set/activity-diagram.png?raw=true
[prioritised-feature-chunk-table]: part-ii-the-lean-product-process/6-specify-mvp-feature-set/prioritised-feature-chunk-table.notes.md
[mvp-pyramid]: part-ii-the-lean-product-process/7-create-your-mvp-prototype/mvp-pyramid.jpg?raw=true
[laddering]: part-ii-the-lean-product-process/4-identifying-underserved-customer-needs/laddering.notes.md
[customer-discovery-frameworks]: part-ii-the-lean-product-process/4-identifying-underserved-customer-needs/customer-discovery-frameworks.notes.md
[lean-product-process]: part-i-core-concepts/lean-product-process.notes.md
