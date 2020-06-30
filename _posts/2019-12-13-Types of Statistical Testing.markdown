---
layout: post
title:  "Types of Statistical Testing"
date:   2019-12-13 09:44:32
categories: technical, data science
paginator: Types of Statistical Testing
---

First this topic must be addressed with how statistical testing works. It's a process that lives and breathes. There's always another test that can be done, so how do you know for sure that the conclusion is the most appropriate one? First, ensure that all variables to be addressed are being addressed appropriately. Then, once the variables have been isolated appropriately for testing, issues of variance in the data must be evaluated and managed accordingly. Next, is running the first test. This test is then followed by a confirmatory test and/or a non-parametric testing equivalent. Once this information has been ascertained it's time to give that information power by evaluating the volume and nature of the original data through effect sizes and power studies. Then, evaluation of error might be necessary. At this point, a conclusion might be reached, but more often, something has been illuminated that starts the questioning process all over again, and a new testing cycle is started.

I like to think about statistical testing in a couple of different ways. First, is the data continuous or categorical in nature? Second, is the data parametric or not? The answers to these two questions give a pretty big indication of what type of statistical testing will be appropriate for the obtained data.

# P-value

All statistical tests in the following categories, up to confirmation testing, are evaluated against something called a p-value. The p-value is calculated during each test, and the person running the test must decide what level of significance is acceptable for the hypothesis. For something like, what a population's favorite color is, the risk of being wrong is low, so a p-value of 0.2, or 80% significance, might be acceptable. For the question, does this medicine work, a p-value of 0.02, or 98% significance, would be more acceptable.

# Continuous / Parametric

If your data meets these two criteria and has relationships within the variables present, then it's likely that a regression analysis, used with a true independent variable, or a Pearson's R test, used with related variables that might have interdependence, is appropriate. However, if there are differences between variables present in the data, it is more appropriate to use a Student's T-Test for two groups and for an ANOVA for more than two groups.

# Continuous / Non-Parametric

Sometimes non-parametric testing can affirm the discoveries in parametric testing, or can supplement when a data transform fails to help the distribution normalize. For relationships within the data, you can use a Spearman's Rank Correlation. If there are differences present in the dataset, you can use a Mann-Whitney U for two treatment groups and a Kruskal-Wallis for multiple treatment groups.

# Categorical / Parametric

In this use case, the diverse Chi Squared test is advantageous.

# Categorical / Non-Parametric

For this particular circumstance, a Fisher's Exact test can be used if the samples are unrelated and in two groups. If the samples are paired, then a McNemar's test can be used.

# Confirmation Testing

To confirm the null hypothesis rejections in the four categories of testing above, various tests that match each category may be run to support the findings.

For continuous and parametric, if you used a regression analysis, there is an associated r-squared value. This value determines how close the generated line is close to a perfect line, which would perfectly represent a relationship. The maximum value for r-squared is 1.0. The closer r-squared is to 1.0, the more representative the generated equation represents the relationship. R-squared values can be used to determine how much of a 'good fit' is present. The r-squared value is the Pearson's Correlation coefficient squared. If you used a Pearson's R test originally, checking out the z-score might not be a bad idea. Finding out what an acceptable correlation coefficient is based on a normal distribution and the number or variables present, also known as degrees of freedom, and comparing that value to the calculated correlation coefficient can be an indicator or confirmation of rejecting the null hypothesis.

# Interpretation Tools

## Cohen's D

## Power
