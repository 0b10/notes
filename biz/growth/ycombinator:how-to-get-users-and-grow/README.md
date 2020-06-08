## Summary

* [Mindmap](mindmap.png?raw=true)
* [Funnel Chart][funnel-chart]
* [Retention Graph][retention-graph]

### Key Takeaways

> Most of the world will make decisions by either guessing or using their gut. They will either be lucky or wrong.

* Measure your retention
* Choose a "North Star metric", and set a goal -- e.g. increase user retention/purchases
* Experiment: A/B testing, surveys, analytics -- and optimise
* Find a product-market fit before you grow
* See caveats before adopting growth techniques as a small company
* Use funnels, and track/optimise every stage
* Products are funnels
* Dedicated growth teams are the way to go for large companies, and they should integrate with other teams


Pursue growth after your have achieved product-market fit -- signalled by adequate user retention. User retention can be measured with a [retention graph][retention-graph], which expresses the performance of customers measured against some value -- an example is repeat subscriptions, and measuring how long customers are retained. Retention graphs should not approach zero, and if they do then product market fit has not been achieved -- the customer isn't happy. Instead of tracking some specific value, like subscriptions, small companies can directly talk to customers.

Factors that affect growth are internationalisation, and targeting mobile platforms. Your natural growth rate will slow down over time

Every product is a funnel, even referrals are funnels. Funnels are made up of stages, each stage should be tracked and optimised.

Growth channels focus on what your product is, and leverage (in a scalable way) how people naturally discover your product. You shouldn't focus on growth channels as a small company. Successful companies can be built without focus on growth channels.

Experimentation provides the data you need to drive growth -- be it product growth, conversion optimisation (e.g. funnels, referrals). Data is how you make decisions.

When you are ready to grow, you should work towards a dedicated growth team which includes data scientists, product managers, designers and user researchers. Before a full team, you should divide responsibility between the existing team, by drawing boundaries between part of the product that provides value, and the part that provides a path towards that value. Not having a dedicated team is not a long-term solution.

## Notes

### When

* After you find product-market fit
* Too early means you will grow really fast, but your numbers will drop with a lack of customer satisfaction

### Factors

* Language translations
  * Native languages open up new markets
* Mobile
  * A huge market segment - the majority
* Natural growth rate
  * Will slow down over time

### Product-Market Fit

Don't work on growth unless you have PMF -- i.e. you are retaining users

#### Retention Graph

* Find a metric that represents value to your customers
* Measure the repeat usage of that statistic

Ideal frequency is a reasonable frequency should be

* The average customer purchase items on Amazon daily
* The average customer uses Airbnb once a year
* The average customer uses Lyft once a week

If you wanted to find out the PMF for a specific product, you will have to wait for repurchases for feedback -- e.g. annually, daily etc.

Company | Value Metric | Ideal Frequency
--- | --- | ---
Amazon | Purchases | Daily
Airbnb | Bookings | Annual
Lyft | Rides | Weekly

Tracking these stats over time reveals:

![PMF retention graph][retention-graph]

* The Y axis is % of users
* The X axis (cohort) is a group of users that share a defining characteristics -- perhaps it's subscribers
* It shows the majority perform action X in the first two weeks, but stop after that. The remaining space on the X axis are users who have been retained for that action.
  * An example is user subscriptions -- most people stop subscribing in the first two weeks, while a percentage of the are still subscribed after 10 weeks.
* Most good products flatten out
  * If it goes to zero, you haven't found product-market fit

#### Other Approaches

* Small companies
  * Talk to users

### People Who Push Growth

The types of people/groups that drive growth for organisations.

These groups were historically different departments, but they essentially should work together.

* Product growth / growth engineering
  * Change/developers the product
  * Engineers, product managers, and sometimes marketers
  * Conversion optimisation falls into this group
  * Funnel optimisation -- your product is a funnel
  * Conversion rate optimisation
    * Internationalisation
    * Authentication -- a fragile moment of customers flowing through your application, needs optimising
    * Onboarding
      * What's the first thing the customer experiences
      * What can the product do to bring the customer towards the value of the product
    * Purchase conversion
* Performance marketing
  * Mainly marketers
  * Effectively Google and Facebook marketing 
  * Data driven
  * This group, and product growth channels are very similar - engineers should work with performance marketers
* Brand marketing
  * hard to measure - not much direct feedback
  * You shouldn't be doing this until much further down the line, once product growth and performance marketing has been exhausted.

#### Funnels

* Every product is a funnel
* Even referrals are a funnel
  * Stages: people who saw the referral program, take rate, users who share, conversion rate etc..
* Funnels are made up of stage -- break down the capture process into stages
* Every stage has a drop-off -- every stage in your funnel, there are different levels of engagement
* Each stage of the funnel can have an entire team dedicated to optimising it
* Stages: SEO, email marketing, sign-ups, copy, payment conversion etc..

An example of a sales funnel chart:

![][funnel-chart]

### Growth Channels

* How people discover your product
* You shouldn't be considering growth channels for a small company
* These channels are scalable
* Some of the things you do when you are a small company don't scale
* Some companies have grown big without any of these growth channels

(The channel describes what the user does, or needs, and the technique describes how you should promote growth.)


* Does your solution rely on one off searches? Like selling a house/car
  * Focus on SEO + SEM
* Do users spread your product through word-of-mouth?
  * Focus on virality techniques, and referrals
* Is your product socially dependent -- i.e. depends on lots of people, like a social network
  * Focus on virality. The more users your get, the better.
* Are your customers a known, limited set? Like all medical practices in the UK etc.
  * Focus on sales
* Do my users have high lifetime value (LTV) -- the total revenue from that customer over time.
  * Focus on paid acquisition -- paid ads from Google, Facebook etc.

#### Referrals

* Engineering word-of-mouth, essentially aiding, growing, and sometimes incentivising an existing, organic word-of-mouth channel
* Example
  * Subject line has the customer's name
  * Clear value - what the customer gets
    * large, bold font
  * Urgency - time gated
  * "Accept invitation" not "Sign up" -- which gives a sense of exclusivity
  * Social proof -- the sender's profile pic, and bio, with length of time the user has been a member
* Think of it as conversion optimisation

#### Paid Growth

* Don't do it unless you have revenue
* CAC: customer acquisition cost
* LTV (lifetime value): how much is a customer worth over the his/her lifetime
* Payback time: how long does it take to regain the CAC considering the LTV
* You can forecast ROI with a retention graph, and calculating how much customers are worth over their lifetime
* Attribution: something your should learn. You need to understand it when measured against attribution cost
* Channels (that matter): Facebook, Instagram, Google and YouTube

### SEO

* Use an SEO browser tool - does what you see convey customer value, or make sense?
* Google doesn't see JS very easily
* On page optimisation
  * Create a strategy
  * start with keyword research
  * What page are you trying to rank for what keyword?
  * Use experimentation to rank
    * Experiment each page
    * Have a control - a similar page
* Off-page optimisations
  * who is linking to you
    * use tools to determine, are they an authority?
    * Press is an authority, get a backlink
* At Airbnb there's a team of 20 working on SEO

### Growth Teams

* A single growth engineer is not a recipe for success, you need a team
* Going from a small company to a larger company, means other team members are responsible for growth due to a lack of a dedicated growth team. You need to set boundaries for where in the entire product/process that growth occurs, and define responsibilities. This is not a long-term solution -- because it doesn't work, and a dedicated growth team is a must.
* You can segment your product into two parts - one part that provides value, and another part that provides a pathway to that value (how customers get to the value). The latter is the domain for growth -- this helps you divide responsibility for growth, especially in situation where you don't have a dedicated growth team, and other team members need to take on responsibility
* Grows teams include engineers, data scientists, designers, product managers, user researchers
  * You won't start with these people, but you should when you start thinking about growth
* To determine what to work on, forecast the effort and weigh it against the outcome -- avoid small outcomes, regardless if it's minimal effort 
* Organisation
  * one
    * Separate growth / product teams

### Making Decisions

* User experimentation
* Decisions have consequences

## Sources

[Y Combinator - How to Get Users and Grow](https://www.youtube.com/watch?v=T9ikpoF2GH0)

[retention-graph]: retention-graph.png?raw=true
[funnel-chart]: funnel-chart.png?raw=true
