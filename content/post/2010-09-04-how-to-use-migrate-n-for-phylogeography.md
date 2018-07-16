---
author: justin
comments: true
date: 2010-09-04 00:38:00+00:00
layout: post
link: http://www.justinbagley.org/136/how-to-use-migrate-n-for-phylogeography
slug: how-to-use-migrate-n-for-phylogeography
title: How to use MIGRATE-N for phylogeography
wordpress_id: 136
categories:
- blog posts
- MIGRATE-N
- Phylogeography
tags:
- gene flow
- MIGRATE-N
- Peter Beerli
- phylogeography
- theta
---

##### Introduction to MIGRATE-N



One thing that makes this a great time to be involved in phylogeography is the exploding amount of data and quantitative methods available to workers.  An important advance in the past 10 years has been the introduction of likelihood- and Bayesian inference-based methods for modeling gene flow, and for comparing models of gene flow, in population genetics.  In particular, model-based coalescent methods are highly attractive.  A method (or class of methods) that stems from statistical population genetics and is useful in phylogeography involves using coalescent gene genealogy samplers to estimate parameters based on variation across a huge number of gene trees representing estimates of probable ancestral patterns.  One of the best coalescent samplers, esp. when models are simple and involve small numbers of populations or regions, is [MIGRATE-N](http://popgen.sc.fsu.edu/Migrate/Migrate-n.html) by Peter Beerli (I make the little caveat there because calculations are basically untenable with >10 populations under some models, but one reason for this appears to be due to a thorough search method).  During the past six months or so, I have been using MIGRATE-N 3.13 on and off to analyze data for three species of freshwater fishes.  Here, I'd like to discuss how to analyze phylogeographic data with MIGRATE-N (hereafter 'MIGRATE')... and incorporate the analyses into phylogeography studies. [Updated May 19, 2016: Note, the most recent version of MIGRATE-N is v3.6, but the manual has not changed since v3.2.1 in 2012.]  
  
Up front, I'd like to pose two issues and address them.  First, why be interested in migration models?  Migration modeling can be used to estimate population sizes (i.e. theta; from which we can calculate effective sizes, _N_e) and gene flow parameters in a flexible coalescent-based setting using maximum likelihood or Bayesian methods.  This is useful for phylogeography for several reasons.  For example, we can use MIGRATE to understand whether population divergence has been accompanied by symmetric or asymmetrical gene flow between lineages/populations; we can use MIGRATE to infer the relative magnitude and direction of dispersal between populations or areas during population expansion, bottlenecks, or stasis.  This might be useful to have a statistical basis for identifying source populations for recolonizations following extinction/extirpation during glaciation periods.  There are a number of other situations when we might want to use MIGRATE.  For example, if we want to know which gene flow model fits our data the best, we can use likelihood ratio tests or Bayes factors to select the 'best-fit' model(s), and this can also be used for choosing between biogeographically diverse models.  
  
Second, why use MIGRATE?  There are several coalescent programs for estimating population sizes, divergence times, or gene flow parameters, including [BEAST](http://beast.bio.ed.ac.uk) and [BEAST2](http://beast2.org), MIGRATE, the related program [LAMARC](http://evolution.genetics.washington.edu/lamarc/index.html), GENETREE, and [the IM family](https://bio.cst.temple.edu/~hey/software/software.htm) of programs.  Mary Kuhner recently wrote an excellent review of all of these programs ([get a PDF of that article by clicking here](http://web.natur.cuni.cz/~muncling/Kuhner%2008%20coalescent.pdf)).  Based on her article and my experiences, MIGRATE is preferred when you are willing to make the assumptions of this program (e.g. constant population size), when you want the flexibility to model ML or Bayesian approaches (or compare them), when you have multiple data types, when you are willing to make a larger number of assumptions than the number you would using other methods (e.g. BEAST), when you want to rid yourself of the infinite sites model and its assumptions (a good idea), and when you have reason to believe the populations being analyzed may have had long-term population structure rather than recent divergences.  
  






##### 12 Steps/Tips for Running MIGRATE-N



OK, here are some steps and tips for running MIGRATE-N for phylogeography studies:  
  
**1. Download the program.  Get the manual and READ it!**  
Use the migrate-n website ([here](http://popgen.sc.fsu.edu/Migrate/Migrate-n.html)).**  
**  
  
**2. Get your sequence data in the right format.**    
  
DNASEQUENCE type data in this program should be placed in an input file in phylip format.  See the manual for other input formats and specific examples.  Most of what follows assumes you are working with sequence data.  However, MIGRATE can run other forms of data, e.g. microsatellites and SNPs...  
  
**3. Run jModelTest to determine the appropriate model of sequence evolution.**    
  
[Updated May 19, 2016:] Currently, the state-of-the-art in evolutionary model selection is basically to run PartitionFinder or jModelTest on DNA sequence data prior to other analyses. If you are trying to add a MIGRATE analysis to a phylogeography project, then you've probably already done this to identify the appropriate models to use in phylogenetic analyses to make trees using your data.  Prior to running MIGRATE on mtDNA sequence data, I suggest that you take a look at your transition:transversion (titv) ratio estimate output by from jModelTest.  The default for this parameter in MIGRATE (ttratio) is 2.0, which is a great starting point for nuclear DNA genes; however, this is not a sensible value for mtDNA.  Odds are, the model you have selected will have a higher value estimate for this parameter... so use that number instead.  Elsewhere, it has been suggested that a means of dealing with this is to set ttratio=20 for mtDNA.  However, in a recent analysis, one of my mtDNA data sets had a titv estimate of ttratio=5.0353.  I also recently obtained a titv estimate of ttratio=11.8 for a different mtDNA data set.  
  
The ttratio setting can also be estimated by running ML tree inference multiple times under different ttratio settings, in order to find the value that maximizes the likelihood (see PHYLIP documentation for tips on doing this in DNAML, for example). Likewise, you can estimate this parameter using ML methods in PAUP*.  
  
**4. Find a supercomputer!!!**  
  
Chances are, if you want to get low estimates of autocorrelation, high effective sample sizes (ESS), etc., you are going to need to run MIGRATE for a looooooonnnnng time--especially if you're using a standard desktop computer!  One reason for this is that using heated chains is probably a good way to go, and using more chains really increases run time.  The best way to deal with this issue and generally long run times needed for convergence and chain mixing is to take advantage of a supercomputing cluster near you.  Several private facilities are available which run MIGRATE, and while the Cornell Computational Biology Service Unit used to run the only public server they recently closed this service off to Cornell faculty and staff (oh well...).  Be aware that one of the problems with public servers is that they (as Cornell used to do) often set limits (e.g., 72 h) on the wall time for each run so that longer runs will automatically be cut short.  This means you'll need to figure out whether such services are useful to you, as well as the conditions under which your runs will be of sufficient length _and _finish on these servers.  I am lucky to have access to an excellent supercomputing cluster at BYU, and MIGRATE runs that would probably take 2-3 weeks on my laptop or desktop usually only take 2-3 days.  
  
**5. Determine if you want to use ML or Bayesian inference.**  
  
OK, you need to decide which type of analysis you want to do.  Elsewhere, it has been shown using simulations that ML and Bayesian analyses in MIGRATE often yield similar results (Beerli, 2006).  This is somewhat unsurprising given that in both cases MIGRATE uses the same DNA/RNA sequence model.  However, the Bayesian approach apparently is preferred for users with only a single locus of data, or somewhat uninformative data, because you can obtain reliable results with less effort than ML analysis (Beerli, 2006).  
  
Both ML runs and Bayesian runs give you likelihood scores that you can use for model comparison and testing.  In Bayesian runs, you get a couple different approximations of marginal likelihoods.  But the thermodynamic integration method is superior to the harmonic mean.  In fact, my preliminary results and the results shown in Beerli's tutorial (link below) both provide examples of the harmonic mean picking model(s) other than the best model (often the second best model).  You get likelihood scores that will be negative.  Out of a set of candidate models, simply find the difference in log marginal likelihood of the best model (highest likelihood) versus all others.  This is a log Bayes factor (LBF).  The LBF for the best model will be zero.  See Kass & Raftery (1995) for an in depth description of these methods and LBF interpretation.  Peter Beerli also has provided an excellent resource for people learning MIGRATE-N ([this learning activity](http://www.molecularevolution.org/resources/activities/migrate_activity)) on the molecularevolution.org website.    
  
**6a. If ML inference.... do several runs and read the LAMARC manual too!**  
To set the search strategy to the maximum likelihood method, use the syntax "bayes-update=NO" in your parmfile.  One method for ML inference that I have seen published in several papers using MIGRATE-N is to run MLE runs multiple times (3-5 times for each data set) and then report averages and upper and lower 95% confidence intervals in your results section.  Information on LAMARC is also available from molecularevolution.org, and from the [Felsenstein/Kuhner lab website](http://evolution.genetics.washington.edu) and [Peter Beerli's websites](http://popgen.sc.fsu.edu/Migrate/Migrate-n.html).** **  
  
**6b. If Bayesian inference...**  
To make the search strategy the Bayesian method, use the syntax "bayes-update=YES" in your parmfile.  
Set your priors correctly!  It is more honest in Bayesian inference to set your priors wide open if you don't have a priori information about Ne estimates (e.g. population census reports), mutation rates/calibration points, historical changes in population size, mark-recapture data, etc.  For example, in my own work on freshwater-limited teleost fishes, I am focusing primarily on Neotropical members of the family Poeciliidae subfamily Poeciliinae which have no known fossils in the Neotropics.  Also very little information exists on rate calibrations for the family.  However, we have begun to grasp the range of life history variation and the fishes I study are highly abundant at some sites, suggesting a possibly large Ne.  To deal with the calibration issue in cases such as this when dealing with mtDNA sequence data, you can use a generic 2% Myr-1 mtDNA rate and make the likely wrong assumption that this is a 'global' rate of DNA substitution e.g. in vertebrates.  However, in my case we have information on the rate of DNA evolution not in Poeciliidae but in several groups of teleosts.  The published mtDNA (COI, control region, Cyt_b_, etc.) rates have different ranges for different genes but range from about 0.008-0.0034 to 0.022-0.028 Myr-1.  So, in my work I usually set a uniform rate prior using these bookends and allow the coalescent sampler/MCMC to estimate the rate for the data.  
  
Setting priors for _N_e, _M_, and theta (only the latter two in most of my MIGRATE-N runs) is more difficult.  But there are several ways to run the analyses.  One 'empirical Bayes' (someone check this term...) method involves looking at the data twice.  First, you would run MIGRATE-N set to maximum likelihood inference, with Fst as your (default) prior for generating MLE of theta (estimates).  This would, if you specify, output a several parameter estimates and 95% confidence intervals.  The 95% bounds can then be used as priors for subsequent Bayesian runs.  This has probably been criticized, but it yields relative rates of M and theta in the same units and, to me, this is still an honest and publishable way of determining priors when no other prior information exists.  For example, in my case of studying freshwater fishes, fish population dynamics are often not well known and surveys of census population sizes of fishes in the wild are probably often inaccurate in estimating _N_e or _N_.  Of course, an alternative method for setting your priors is to use survey data, if you have some for your focal taxa; or you could use survey information from related species.  Still, because of the issues of setting these priors under Bayesian inference, you may be interested in simply using MLE; but remember Bayesian inference might be preferred for low-information data.   
  
**7. Learn to tell MIGRATE to generate multiple output types**  
Like I mentioned above MIGRATE-N can give you several types of output.  My favorite modification to make to the parmfile is to force Migrate to do a Bayesian skyline analysis and report parameter values through time.  This gives a great graph set to possibly include in your paper and yields a perspective on historical demography, not just spatially oriented (e.g. pairwise, by population or region) parameter estimates.  
  
  
**8. Do not make silly mistakes in your input files.**  
For example, if you are running MIGRATE on a supercomputer, like the one at BYU, then don't forget little details that might otherwise be overlooked.  For example, I like to set up my parmfiles in a word processor rather than going through the program menus, then I run in batch mode on the cluster.  This means that I need to set menu=NO, or it will not work.    
  
**9. Learn to analyze / interpret MIGRATE output files.**  
Migrate gives a beautiful .pdf file of output information that reflects the output you called in your inputfile "parmfile."  Again, stay away from the harmonic mean likelihood approximation.  Use thermodynamic integration (TI) instead.  
  
**10. Learn to optimize conditions of your runs.**  
Based on my understanding, the best way to do this is to do multiple runs and determine how sensitive parameters are to initial conditions.  To more fully understand your runs and the thoroughness of your sampling, you will need to look at the trees and data output in each run (and specify that they are output) in a program like AWTY or TRACER.** **  
  
**11. Don't forget to create a logfile.**  
Use the command logfile=YES:logfile, where the second "logfile" happens to be the name specified for the logfile.  
  
**12. Always conduct multiple runs.**  
One thing that I have done when implementing the ML then Bayesian runs method mentioned above is that I a have run Bayesian runs several times in sequence after I have the ML-generated priors.  In this method, I use the results from each run to inform the subsequent run as priors.  Theoretically, we should get better searches of tree space, and results (we hope), this way.    
  
**REFERENCES**  
  
Beerli, P. (2006) Comparison of Bayesian and maximum likelihood inference of population genetic parameters. _Bioinformatics_, 22: 341.  
  
~ J
