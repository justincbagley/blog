---
author: Justin Bagley
comments: true
date: 2011-08-06 14:20:00+00:00
layout: post
link: http://justinbagley.rbind.io/2011/08/06/jmodeltest-will-not-run-with-single-quotes-around-tip-names/
slug: jmodeltest-will-not-run-with-single-quotes-around-tip-names
title: jmodeltest will not run with single quotes around tip names
categories:
- blog posts
- jmodeltest
- software
tags:
- jmodeltest
- model selection
- software
---

A little while ago, I discovered a common error in `jmodeltest` is the error message that the number of sites appears to be wrong.  I recently encountered this issue again. This is caused by single quotation marks on either side of tip names in a NEXUS file, which is a common form of the output/exported NEXUS file from `DnaSP`.  

So, once you export a NEXUS from `DnaSP`, say after doing some population level genetic analyses or after defining sequence groups for setting up structure in ARLEQUIN, you should simply open your NEXUS file in a word processor or text editor and use the "Replace" command to remove all quotation marks from your file. Dots aren't usually a problem, but spaces should probably also be avoided within sequence names. I never put spaces, only letters, numbers, dots, or underscores. And this has worked for me so far. Hope this helps.  
  
~ J
