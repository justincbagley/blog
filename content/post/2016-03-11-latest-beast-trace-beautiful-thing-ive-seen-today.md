---
author: justin
comments: true
date: 2016-03-11 12:00:01+00:00
layout: post
link: http://www.justinbagley.org/2183/latest-beast-trace-beautiful-thing-ive-seen-today
slug: latest-beast-trace-beautiful-thing-ive-seen-today
title: 'Latest *BEAST trace: Most beautiful thing I''ve seen today'
wordpress_id: 2183
categories:
- Bayesian
- BEAST
- blog posts
- Species delimitation
- species trees
tags:
- Bayes factor
- Bayes factor species delimitation
- BEAST
- BFD
- likelihood
- marginal likelihood estimate
- trace
- Tracer
---

My new *BEAST (starbeast) species tree runs are converging wonderfully in BEAST v1.8.3, so I am off to a great start this morning. Here, I'm including a screenshot of the results of one of these runs, which I ran for 200 million generations using 3 normally distributed calibration points, as visualized in Tracer. Note the good posterior trace, very high ESS scores for all parameter estimates, and good use of burn-in (default 10% value works quite well in this case).

This is the most beautiful thing I've seen in my research today, or even this week![![38_STARBEAST_PSmle_post_trace_Mar10](http://www.justinbagley.org/wp-content/uploads/2016/03/38_STARBEAST_PSmle_post_trace_Mar10-e1457623813213.png)](http://www.justinbagley.org/wp-content/uploads/2016/03/38_STARBEAST_PSmle_post_trace_Mar10-e1457623813213.png) 

I am now checking and processing the results from multiple such runs using different species schemes (trait mapping schemes/files). They seem like they are going to give me a nice estimate of the species tree for this dataset.

Currently, the second steps of these runs are still running, using path sampling/stepping-stone sampling to calculate marginal likelihood estimates (MLE) for each model. When this is completed, I will calculate Bayes factors for each model and use them for Bayes factor species delimitation (BFD) _sensu_ Grummer et al. (2014). 

Is anyone else working on BFD analyses like this right now? Would love to hear from you.

~J

**References**

Grummer JA, Bryson RW Jr., Reeder TW. 2014. Species delimitation using Bayes factors: simulations and application to the Sceloporus scalaris species group (Squamata: Phrynosomatidae). Systematic Biology 63(2): 119-133.
