ISBN-10: 0321321367 

## Notes

### 1.1 - What Is Data Mining? (p2)

Preprocessing => data mining => post-processing

Preprocessing:

* cleaning: removing noise
* aggregating multiple sources
* ...
* is very laborious

Post-processing

* ensuring only valid and useful results are incorporated into the decision making system
* data visualisation

### 1.2 - Motivating Challenges (p4)

* scalability
  * efficient data structure, algorithms, memory management techniques
* high dimensionality
  * literally the number of dimensions, or attributes of data to analyse
  * spatial and temporal data have high dimensionality
* Heterogeneous and complex data
  * heterogeneous data is typically simple to deal with
  * complex data objects need to take into account correlative data - like time, parent-child relationships from web pages, location etc 
* non-traditional analysis
  * traditional analysis is based on hypothesise-and-test methodology 
    * extremely labour intensive
    * current data analysis requires potentially thousands of hypothesis
    
### 1.4 - Data Mining Tasks (p7)

Generally, mining tasks are divided into two categories:

* predictive tasks
  * predict the value of an attribute relative to values of other attributes
  * the subject/target is called the target or dependent variable
  * the source attributes are called the explanatory or independent variables
* descriptive tasks
  * to derive patterns (correlations, trends, trajectories, anomalies) that summarise the underlying relationships in data 
  * requires post-processing to explain the patterns

The four core data mining tasks

* Cluster analysis
  * grouping observations based on some arbitrary concept - and using an algorithm to identify what cluster the data belongs to
  * {dollar, industry, country, load, deal, government} - economy related words found within a document
* Predictive modelling
  * build a model for the target mode as a function of the explanatory variables
  * the goal is learn a model that minimises the error between the predicted and true values of the target
  * two tasks
    * classification: used for discrete target variables
      * requires that the output is one of two or more classifications [\[1\]][1] (the book gives an example that has a binary result) - predicting whether a customer will/will-not purchase a product
      * classification can take regressive data (real numbers) and classify them into categories - like small, medium, large - when describing the lengths of flower petals for example
    * regression: used for continuous target variables
      * requires that the output is a quantity, or real "continuous"-value [\[1\]][1] - and not a classification
* Association analysis
  * used to discover patterns that describe strongly associated features in data
  * typically represented as implication rules or feature subsets - i.e. descriptions of the data that describe what holds true, or is - as a matter of fact
  * examples: genes that have related functionality, or web pages that are accessed together, items that are frequently bought together
* Anomaly detection
  * identfying observations whose characteristics significantly vary from the rest of the data
  * aka outliers
  * you must avoid falsely labelling normal objects as anomalies - aka low false alarm rate
  * credit card fraud, network intrusions etc.

### 1.6 - Bibliographic Notes (p13)

* Lots of author recommendations in this section - with specific focus, like business applications, statistics, introductory books etc.
* An number of conferences are also mentioned
* Journal publications are mentioned too, along with some specific articles.
* streamed data is also a source for data mining - stock prices is an example of streamed data
  * some journals are also mentioned in this section that specifically publish articles on mining streamed data

### 2.0 - Data (p19)

> Explores data related issues that are important for successful data-mining

* Types of data
  * the type of data will determine what tools are used 
  * types
    * qualitative
    * quantitative
    * time series - data objects with a relationship to time
    * objects with explicit relationships with each other
* data quality
  * often not perfect
  * most techniques tolerate some imperfections
  * data should be cleaned up
  * issues
    * noise
    * outliers
    * missing data
    * inconsistencies
    * duplicate data
    * bias
* preprocessing is used to clean the data
  * to improve the data quality
  * modifying it to prepare it for specific types of processing - e.g. a continuous attribute being classified
  * reducing the number of attributes in a data set because many techniques perform better with less
* analysing data in terms of its relationships
  * one approach is to extrapolate relationships and use those for further data mining, and not the raw data itself
* misc
  * know your data
    * know what each attribute means
    * how attributes are correlated with others
    * if the data is sorted
    * the example in the book showed that there was a correlation between two unknown fields, but one was an ID field, which was assigned after the whole set was ordered by the other field - this created a correlation, but it's meaningless. Know your data.

### 2.1 - Types of Data (p22)

* a data set is a collection of data objects - aka. record, point, vector, pattern, event, case, sample, observation or entity
  * e.g. - a file, where each row is a record, and each column is an attribute
* a data object is described by a number of attributes - e.g. a record is made up of a number of fields
* measurement scale: see glossary
* measurement: see glossary
* it's important to know the type of the attribute, so that you know how it relates to other attributes, and you don't do foolish things with it
* it's common to refer to the type of an attribute as the type of a measurement scale

### 2.1.1 Attributes and Measurement (p23)

* attributes can vary in more than one way - e.g. by person etc. or over time

The different types of attributes:

* properties of attributes
  * =/=, ==, +, -, <, >, <=, >=, *, /
* qualitative types
  * nominal: names etc. just distinguishes objects
  * ordinal: can be ordered < > - good/bad/better/best, street numbers, grades etc.
* numeric types
  * interval: values where differences are meaningful  +/- -- temp, date
  * ratio: both differences and ratios are meaningful -- temp, count, mass, length etc.
* attributes like IDs are qualitative, because they lack most of the properties of numbers, and they cannot be treated in the same way - they should be treated more like symbols 
* attribute types are defined in terms of permissible transformations (see glossary)
* the best statistical operations are ones that preserve the attributes meaning - e.g. the average length means the same thing whether it's in feet or meters. The calculated average can be transformed into meters or feet
  * kelvin to Celsius is a good example
  * Celsius to Fahrenheit is not - because the ratio between the two is not meaningful

Describing attributes by the number of values:

* you can distinguish between types by the number of values it takes
* discrete - finite, countably infinite - qualitative or numerical
  * see glossary
  * often represented by integers
  * binary is a special case of discrete values with only two possibilities - yes/no, true/false, 1/0
  * nominal and ordinal types are typically binary or discrete
* continuous 
  * typically floating point 
  * interval and ratio attributes are typically continuous

Asymmetric Attributes

* only non-zero values are important - zero values are ignored, and unimportant
* an object may have a number of zero attributes, but only the ones that are non-zero are significant - the example in the book was the courses that are attended by a student, if the attributes were all names of courses that the institution offers, and set to a binary value, then most of the attributes will be set to zero.
* asymmetric binary values
  * both values are not equally important [\[2\]][2]
  * e.g. you are only interested in true results - pass == false is of no interest, nor is it important
  * particularly important for association analysis
* asymmetric discrete and asymmetric continuous values are possible 

### 2.1.2 - Types of Data Sets (p29)

General characteristics of data sets

Three characteristics that have a significant impact on the data mining techniques used:

* dimensionality
  * the number of attributes the data set possesses
  * high dimensionality data sets are much harder to analyse
    * dimensionality-reduction is a common preprocessing step
* sparsity
  * example: data sets with lots of asymmetric attributes will mostly be set to zero, which means it is highly sparse
  * high sparsity with asymmetric sets can be an advantage - because only the non-zero values need to be processed
  * some algorithms work well for only sparse data
* resolution
  * essentially the level of detail that the data set contains - e.g. the surface of the earth is almost completely flat when viewed at a resolution of 10km 
  * patterns in the data depend on the resolution
    * too fine means the pattern could be buried in noise
    * too coarse, the pattern may disappear (10km flat earth theory - look into it)

record data:

* much data mining assumes that the data is a set of records with a fixed set of data fields
* usually stored in flat files or relational databases

transactional or market basket data:

* Transaction data
  * a special type of record data where each record is a transaction
  * each transaction involves a varying set of data - conversely to a typical record where the fields are set
  * typically the attributes (market basket data) of the transaction are asymmetric binary - e.g. products bought at a market, where each item purchased is non-zero
* market basket data
  * typically asymmetric binary
  * can be discrete or continuous - where a non-zero value indicated the inclusion of an attribute, but also a quantity or some other metric
* the example in the book
  1. a customer goes shopping
  1. fills his market basket with arbitrary goods - where the relative attribute is set to a non-zero value
  1. a transaction is made and each transaction is potentially unique

data matrix:

* it's basically as it sounds - a table, or matrix with n spatial dimensions
* one axis is a data object, the other axis is attributes
* consists of numeric values
* standard matrix operations can be used to transform data
* is the standard data format for most statistical data

sparse data matrix:

* is a special type of data matrix 
* all attributes are of the same type, and asymmetric
* A record is a sparse matrix
* document data can also be a sparse matrix
  * document-term matrix
    * the name for sparse matrix of a document that tracks terms 
    * each record is a document
    * each term is an attribute of a record, and the value is the (asymmetric) number of times that phrase appears in the document

graph-based data:

* two cases (more cases could be possible)
  * capture relationships between data objects
    * usually important
    * web pages and SEO for example - anchors usually provide a great deal of contex
    * links between objects can be just relationships or sometimes properties - properties that somehow link two units of data, like direction, weight, age, etc.
  * data objects themselves are represented as graphs
    * if objects have sub-objects that have relationships
      * sub-structure mining of a branch of data mining, and mines such data
      * an example is chemical compound data, where the sub-structure is the atoms and bonds

ordered data:

* sequential data
  * aka. temporal data
  * each record has time associated with it
  * each record and attribute can each have time associated with it
  * a simple example: each record indicates a transaction at a specific time index, the associated customer, and the items they bought
* sequence data
  * similar to sequential data, except there are no timestamps
    * sequence is defined by position in the sequence, like the nth word in a document, or letter in a word
  * examples: words in a document, letters in a word, gene sequences in a genome 
* time series
  * a special type of sequential data
  * each record is part of a time series, and attributes are measurements at that specific time index
  * temporal autocorrelation: values close together in the time sequence are usually closely correlated
  * examples
    * temperature over time, stock prices over time
* spatial data
  * when objects have position, area, geographical location attributes etc.
  * spatial autocorrelation: items that are close, spatially, tend to be similar
  * examples:
    * weather - with geographical locations

## Glossary

* attribute: a component of a data object - aka. variable. characteristic, field, feature or dimension
* continuous attribute: an explanatory attribute that is a real value (typically floating point), and not a classification - e.g. a metric, or quantity
* data object: can be any of - a record, point, vector, pattern, event, case, sample, observation or entity
* data set: a collection of data objects, and probably a better description of a data source than API, database, public data etc.
* discrete attribute: has a finite number of values, or countably infinite - either qualitative, or numerical
* explanatory/independent variables: the source attributes for predictive tasks
* KDD: Knowledge Discovery in Database
* measurement: the process of applying a measurement scale to associate an attribute of an object with a value or symbol of the measurement scale.
* measurement scale: is a rule (function) that associates a numeric or symbolic value with the attribute of an object - and typically correlate to attribute types - nominal, ordinal, interval, ratio
* permissible transformations: e.g. the meaning of length attribute is the same whether it's in meters of feet
* subject/target variable: the target for a predictive task

[1]: https://machinelearningmastery.com/classification-versus-regression-in-machine-learning/
[2]: https://www.geeksforgeeks.org/understanding-data-attribute-types-qualitative-and-quantitative/
