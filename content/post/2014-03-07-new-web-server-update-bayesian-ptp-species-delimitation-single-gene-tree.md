---
author: justin
comments: true
date: 2014-03-07 16:05:31+00:00
layout: post
link: http://www.justinbagley.org/569/new-web-server-update-bayesian-ptp-species-delimitation-single-gene-tree
slug: new-web-server-update-bayesian-ptp-species-delimitation-single-gene-tree
title: New web server update for Bayesian PTP species delimitation on single-locus
  gene trees - and more!
wordpress_id: 569
categories:
- blog posts
- Species delimitation
tags:
- coalescent model
- coalescent-based species delimitation
- Exelixis Lab
- GMYC
- Jiajie Zhang
- phylogeny
- PTP
- software
- species delimitation
- web server
---

Recently, biologists have been developing statistically more rigorous methods that 'put the teeth into' species delimitation, including species discovery approaches, and provide what appears to be new steps towards more automated means of taking advantage of DNA sequence data for these purposes.  This is critical given the current biodiversity crisis.

Among the new methods, two sets of methods take similar approaches to delimit species from one or multiple phylogenetic trees.  These methods, the general mixed Yule-coalescent (GMYC) model and the Poisson tree process (PTP) model, were initially developed to use coalescent or non-coalescent statistical algorithms to delimit species on single-locus gene trees, e.g. usually generated from mtDNA including 'barcode' data gathered in systems where nuclear gene sequencing has not been conducted or is not feasible.  Both methods were also initially developed using maximum-likelihood (ML) approaches, and now have been extended with Bayesian implementations capable of using one tree or many trees (e.g. from bootstrapping or from the posterior distribution of trees output by a Bayesian inference analysis).  One difference between them that you'll be interested in is that GMYC requires an ultrametric time tree and was developed to handle single-locus trees, whereas PTP does not require an ultrametric topology but instead looks at the pattern of substitutions along the branches of a non-ultrametric tree.  For many people, this will make one or the other method more attractive (e.g. if you think developing time trees is difficult or arbitrary, you'll want to use PTP).

As much as I'd like to go on about these methods, you can read about them yourself or I can explain them later; the point of this post is to highlight the fact that Jiajie Zhang of the [Exelixis Lab](http://sco.h-its.org/exelixis/index.html) (="Evolution" Lab), Heidelberg Institute for Theoretical Studies, has recently updated the Species delimitation server (or PTP web server) to allow free online runs with the Bayesian PTP implementation.  [Link to the PTP web server here](http://species.h-its.org/ptp/).  This web server previously ran the ML version of PTP, but now runs Bayesian PTP (bPTP).  In addition to the PTP models, Jiajie has also provided us with a web server to run ML GMYC models on the data as well, for comparison.  [Link to the GMYC web server here](http://species.h-its.org/gmyc/).

That said, you do not _have to run _your analyses on the Exelixis web Species delimitation server.  The web server links above will take you to pages containing external links to download the standalone versions of  PTP and bPTP, which run in python.  These are maintained by Jiajie on his Github page.

Both methods--GMYC an PTP--provide confidence intervals on species delimitations.  And bPTP will output Bayesian support values for each delimited species (along each branch).

Of course, you should take the time (as I have) to read the original papers on each of these models before you run them (probably all of them, regardless of which one you present in your final analysis or publication).  This is to be stressed.  Here are links to the papers corresponding to each method:

GMYC - original ML implementation, single-threshold model - [Pons et al. (2006)](http://sco.h-its.org/exelixis/index.html)

GMYC - ML implementation with multiple-threshold model - [Monaghan et al. (2009)](http://sysbio.oxfordjournals.org/content/58/3/298.short)

GMYC - v2 of splits and modified version (newest GMYC citation/model) - [Fujisawa and Barraclough (2013)](http://sysbio.oxfordjournals.org/content/62/5/707.short)

bGMYC - new Bayesian implementation of single- and multiple-threshold GMYC models using single or multiple gene trees and accounting for phylogenetic error (e.g. using Bayesian MCMC) - [Reid and Carstens (2012)](http://www.biomedcentral.com/1471-2148/12/196)

PTP - original ML implementation, both models (serves as citation for bPTP as well, since there is no one paper on this method yet) - [Zhang et al. (2013)](http://bioinformatics.oxfordjournals.org/content/29/22/2869.short)

Note we are getting close to submitting a paper on species delimitation in Central American "mollies" (Poeciliidae; 'livebearing fishes') so you can look to our paper one day and cite it as an example of using these methods with other coalescent-based species delimitation methods.  Check back for more news about that pub this year. Happy species delimiting!

~J
