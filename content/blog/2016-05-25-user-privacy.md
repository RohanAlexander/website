---
title: User privacy
author: Rohan
date: '2016-05-25'
slug: user-privacy
categories: []
tags: []
---

# Introduction

Maintaining the trust of people who participate in Petit Poll is a critical aspect of operating Petit Poll. I would prefer to shut down Petit Poll than undermine that trust. Please point out any mistakes that I am making or areas that I could improve.

# Response collection

The primary way that Petit Poll collects responses is via forms that are hosted on our website (https://www.petitpoll.com/initial-poll and https://www.petitpoll.com/intention-poll). The website is now served over HTTPS meaning that responses should be encrypted in transit. The forms save to Google spreadsheets. (In the past we used Google forms for survey responses, and again those went into Google spreadsheets). Google spreadsheets should be secure, so long as they are set up properly, but if anyone knows differently then please let me know.

# Initial Poll

When we want to analyze the responses I download the Google spreadsheet to my computer as a CSV. Let's call this the ‘raw database’. I run a script in R that first isolates the email addresses and first names (when they were asked for; they are no longer asked for), randomizes their order, and then saves them into a separate 'emails database' that is then used to send email invitations to future surveys, but contains no other information.

At this point the first names are deleted from the raw database. (Again, first names are no longer asked for in the Initial Form so this step is not needed). Email addresses in the raw database are then salted and hashed. We have to keep the hashed version of them because we need them to link responses from the Initial Poll with the Intention Poll, but we don't need to keep them as email addresses in the raw database.

A hash means that the emails are transformed in a way that the output is the same if the input is the same i.e. ‘rohan@example.com’ is always transformed into 1234abcd5678, but the transformation is one-way only - if our raw database leaks and you know that 1234abcd5678 would vote for Daenerys Targaryen, you shouldn’t be able to know that 1234abcd5678 is rohan@example.com. Adding salt means that is someone gets our list of emails they can't simply hash them and compare the hash outputs to associate responses with email addresses.

# Intention Poll

At this point the raw database has a hash of each email address (not the actual email address), along with the responses to the questions that were asked in the Initial Poll. When a person responds to the Intention Poll they submit their email address and their intention. This email address is hashed and the hash is used to match their current intention their existing data in the raw database (both previous intentions as well as demographic and political history).

It is only now that the raw database is used for analysis, and the model is run on it.

# Weaknesses

At this point, respondents need to trust that I don’t look at their responses. I’m not sure how to get around this. Also I’m not sure whether salting and hashing the emails is the best way to preserve anonymity if the database leaks. There may be some best-practices from medical or psychology research that we can adopt and I'll be looking into these in the next few weeks.