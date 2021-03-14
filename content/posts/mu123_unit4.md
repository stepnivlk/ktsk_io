+++
title = "MU123 Unit 4 Notes"
date = 2021-03-14

[taxonomies]
categories = ["uni", "math"]
+++

# 1 Questions, questions
* Quantitative view - uses numbers -> measurments, counts
* Qualitative view - describes what something is like in words

Statistics is about quantitative view

## 1.1 Types of statistical question
* Summarising: how can the information be reduced?
	* Reduction of many numbers to few representatives, e.g. average
	* Statistical charts or plots
* Comparing: is there a difference?
	* Depends on various factors
		* Sizes of the samples on which averages are based
		* The degree of variation
		* Whether the size of the observed difference is sufficiently large to act upon
* Seeking a relationship: what sort of relationship is there?
	* Finding a possible relationship between quite separate things
	* Statistical relation doesn't prove a cause-and-effect relationship
	* Useful to determine the kind of relationship
		* How much does one factor change relative to the other?

## 1.2 The statistical investigation cycle
The stages of statistical investigation
1. **P**ose a question
2. **C**ollect relevant data
3. **A**nalyse the data
4. **I**nterpret the data

Forming **PCAI** cycle:
{% mermaid() %}
stateDiagram-v2
	P: P Real world
	A: A Statistical world
	P --> A : C
	A --> P : I
{% end %}

The question has to be as focused as possible.

# 2 Dealing with data
* Issues to do with collecting data (**C**)
* Important distinctions between different types of data (**A**)

## 2.1 Primary and secondary data
* Primary data - data that I collect by myself (a research unit)
* Secondary data - data that already exist and can be used or adapted
* Dataset - a collection of data (e.g. in tabular form)
	* Reference should be provided

## 2.2 Discrete and continuous data
* Discrete - counting
	* Can take one of a particular set of values, typically integers
	* Non-numerical data can be coded to discrete values
		* e.g. binary yes/no -> 1/0
	* Exact answer can be given
* Continuous - measuring
	* Can take all the in-between values on the number scale
	* All the real numbers, can be constrained to e.g. finite interval 
	* Never possible to get an exact answer
		* Measurements can be only approximated with some degree of precision

The approximation given by measuring of continuous data implies that its a dicrete representation of continous data

## 2.3 Checking and cleaning data
One or more data values that are considerably smaller or larger than the other values in the same dataset are called **outliers**.
Outliers sometimes correspond to errors. Sometimes its just unusual observation (e.g. woman 1.92m tall).
Therea are various statistical techniques to deal with outliers.

## 2.4 Spurious precision
Can arise in various ways, e.g.:
* Conversion of units
	* E.g.: age given as $29.91666$ that is a result of months-to-years conversion $=29\text{years} + 11\text{months}/12$
* Implying that a quantity can be measured to a greater level of precision than is possible with the measuring instrumet used. 
* Quoting figures to a greater number of significant figures than is warranted in the context. 

Generally, displayed data should be just precise enough to reveal the key features.

## 2.6 Single and paired data
* **Sigle data** - can be analysed in isolation, e.g. in weights of persons I can: 
	* Find average
	* Find dispersion of values
	* Plot it to discren the overall pattern visually
* **Two-sample data** - second dataset is added, e.g. weights of old persons
	* Interest now is in comparing features
* **Paired data** - e.g. statistical interest being in comparing weight of babies to the weights of their mothers at the start of pregnancy.
	* Essentially seeking a relationship
	* Two data lists must contain the same number of values
	* For each item in one list there's a corresponding item in the other


# 3. Summarising data: location
Stage **A** of the PCAI cycle - analysing data that have been collected.
**Location** of a dataset is:
* Single number that represents
	* average value
	* typical value
	* central value
* Sets of data can be compared by their locations 

## 3.2 Measuring location
There's no single and universally most appropriate measure of location. Measures can be chosen mased on the situation and the nature of the data.
The three most common measures of location are:
* Mean
* Mode
	* A value that occurs most frequently in the dataset
		* Won't be used in MU123
* Median

### Mean
(also arithmetic average)

> Strategy
> 
> * Add all the numbers together
> * Divide by however many numbers there are in the set.

### Median
Data value that is in the middle when the data are arranged in order

> Strategy
> 
> * Sort the data into increasing or decreasing order
> * If there is an odd number of data values, the median is the middle value
> * If there is an even number of data values, the median is defined as the mean of the middle two values

## 3.3 Mean versus median
When the values are highly symmetrical the values of mean and the median are very similar. Outlier on one side has big impact on mean but none on median, e.g.:
$$
[3,4,5,6,7,8,99] => \text{mean}: 18.9 ~\text{median}: 6
$$

# 3. Summarising data: spread 
How widely **spread** the values are.

E.g. following data set is relatively widely spread from 42 to 92:
$$
[42, 58, 60, 68, 78, 92]
$$

And following set is narrower, ranging from 60 to 80:
$$
[60, 65, 72, 74, 75, 80]
$$

## 4.1 Range
The difference between the smallest and largest value in the set.
$$
\text{range} = \text{max} - \text{min}
$$

Not adequate when there are extreme outliers in the dataset.

## 4.2 Quartiles and the interquartile range
Exclude top and bottom quarters of the values and create a new measure of spread that measures the range of the middle 50%.
Cutoff points are called **quartiles**
* **lower quartile** (Q1)
* **upper quartile** (Q1)

**Interquartile range** (IQR) is the difference between the upper and lower quartiles (Q3 - Q1)

> Strategy
> 
> * Arrange the dataset in increasing order.
> * Next
> 	* When even
> 		* Q1 is the median of the lower half of dataset
> 		* Q3 is the median of the upper half of dataset
> 	* When odd 
> 		* Throw out the middle value, median (one of the conventions)
> 		* Q1 is the median of the lower half of new dataset
> 		* Q3 is the median of the upper half of new dataset
> * IQR is Q3 - Q1

## 4.3 Standard deviation
> Strategy
> 
> * Find the mean of the dataset
> * Find the difference of each value from the mean - 'deviations', labelled as $d$ values
> * Square each deviation - $d^2$ values
> * Find the mean of these squared deviations - 'mean squared deviation' - **variance**
> * Find the square root of the variance - 'root mean squared deviation' - standard deviation

## Summaries of data
{% mermaid() %}
graph LR
    id[Summaries of data]
	id-->Location
	id-->Spread
	Location-->Mean
	Location-->Median
	Spread-->Range
	Spread-->iqr[Interquartile range]
	Spread-->std[Standard deviation]
{% end %}

# 5 Measuring with accuracy and precision
Repeated measurements to asses the quality of dataset.

## 5.2 Accuracy and precision
* **Accuracy** describes how close the average is to the true value
* **Precision** describes how close the measurements are to each other
