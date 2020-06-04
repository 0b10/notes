# Key Takeaways

* Start with meeting a target market needs, not an idea/solution
* Use a data driven approach to measure customer satisfaction
* Iteratively model your customer with personas, express your hypotheses
* Deeply understand the customer needs, and be very pragmatic.
* Use iterative interviews/surveys to dig deeper
* Define the product value proposition as a list of needs to be addressed
* Focus on a small set of the most important needs, reducing risk -- say "no" lots.

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

[adoption-lifecycle]: part-ii-the-lean-product-process/3-determine-your-target-customer/adoption-lifecycle.notes.md
[persona-template]: part-ii-the-lean-product-process/3-determine-your-target-customer/persona-template.notes.md

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

[laddering]: part-ii-the-lean-product-process/4-identifying-underserved-customer-needs/laddering.notes.md
[customer-discovery-frameworks]: part-ii-the-lean-product-process/4-identifying-underserved-customer-needs/customer-discovery-frameworks.notes.md

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

[kano-model]: part-ii-the-lean-product-process/4-identifying-underserved-customer-needs/kano-model-framework.png
[value-proposition-template]: part-ii-the-lean-product-process/5-define-your-value-proposition/value-proposition.template.md
