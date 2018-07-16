---
author: justin
comments: true
date: 2011-08-05 19:41:00+00:00
layout: post
link: http://www.justinbagley.org/127/new-garli-web-server-for-runs-in-the-cloud
slug: new-garli-web-server-for-runs-in-the-cloud
title: New GARLI web server for runs in the cloud
wordpress_id: 127
categories:
- blog posts
---

I just noticed that molecularevolution.org has provided, with Derrick Zwickl, a new online server for running phylogenetic maximum likelihood analyses using GARLI.  The server for putting up new jobs (runs) can be found at:  
  
[http://molecularevolution.org/software/phylogenetics/garli/garli_create_job](http://molecularevolution.org/software/phylogenetics/garli/garli_create_job)  
  
A starting tree can be specified (although this doesn't save time in GARLI like it does in PAUP*) and up to 2000 bootstrap reps can be performed.  
  
This will prove a useful resource for anyone who doesn't want to take time to put their jobs up on a supercomputer using some form of scripting (e.g. Perl), and for anyone who finds it disadvantageous to run phylogenetic algorithms on their personal desktop or laptop computers.  I don't know what this server is running or how fast the runs are, but GARLI (0.97) is very fast on the BYU supercomputer ("Mary Lou"), usually terminating in a matter of minutes when runs are placed on a single node.  So, I'm expecting this service to be pretty quick; of course, the length of runs will depend on the number of taxa and characters, as well as usage.  Note the option to generate site likelihoods, as in PAUP*, which will be useful for running analyses in CONSEL (although you may want to see the GARLI manual/web sites before generating these "site-likes" ... [click here for my previous post on GARLI with the appropriate links](http://ievofish.blogspot.com/2010/08/garli-program-for-maximum-likelihood.html)).  
  
~ J
