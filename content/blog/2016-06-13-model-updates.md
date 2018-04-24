---
title: Model updates
author: Monica
date: '2016-06-13'
slug: model-updates
categories: []
tags: []
---
We use a multilevel regression and post-stratification (MRP) approach to obtain estimates of voting intent. Our approach closely follows the approach used by Ghitza and Gelman (2013). However, this week we made some changes to the underlying model, to better make use of the information obtained from the weekly polls. 

A brief description of the model framework: First, we split up the sample of respondents into subgroups based on sex, age and education. We have four age groups (18-29, 30-44, 45-64 and 65+) and four education groups (high school or less, certificate, bachelors, postgraduate). The main idea is to estimate the probability that a person in a particular subgroup (of a particular sex, age and education level) will vote for party X. This is the multilevel regression part of the approach. 

Once the probabilities for each sub-group are estimated, they are re-weighted and combined to give an overall population estimate. The weights in this process are based on the percent of the total population in each of the subgroups. It is this re-weighting (post-stratification) process that allows us to use a non-representative sample to get a representative estimate. 

The change to the model we made this week was related to how estimates were made in the multilevel regression part of the approach. Previously, we had been estimating the model for each week separately. However, this ignores the fact that we have information from other weeks that is useful for estimation. Thus, we made a change to the model so that the parameters estimated for a particular week are partially informed by data collected in previous weeks. This change better utilizes all information available and also makes our parameter estimates more robust from week to week.

