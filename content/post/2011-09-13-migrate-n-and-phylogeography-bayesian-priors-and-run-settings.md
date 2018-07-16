---
author: justin
comments: true
date: 2011-09-13 14:56:00+00:00
layout: post
link: http://www.justinbagley.org/121/migrate-n-and-phylogeography-bayesian-priors-and-run-settings
slug: migrate-n-and-phylogeography-bayesian-priors-and-run-settings
title: 'Migrate-N and phylogeography: Bayesian priors and run settings'
wordpress_id: 121
categories:
- Bayesian
- blog posts
- MIGRATE-N
tags:
- gene flow
- MIGRATE-N
- migration
- models
- prior selection
- priors
---

In a previous post I discussed using Migrate-N for phylogeography (e.g. migration model testing, run settings, general tips).  I mentioned that Migrate-N runs maximum likelihood (ML) and Bayesian algorithms and I discussed those a little bit, including how to run under different estimation modes.  While Bayesian analysis is likely to be preferred for several reasons, a common critique of Bayesian methods in statistical population genetics and elsewhere is that it is difficult to set the prior information for each run.  I pointed out that using _a priori_ information from ecology, for example, to set boundaries on migration or theta, or using broad/previously-published rate calibrations, can increase the objectivity of this step.  However, I also suggested that when information is essentially totally lacking, one method might be an empirical, step-wise approach using ML estimates of the run parameters and their 95% CIs to set the priors for subsequent Bayesian runs.  Although this might produce good results and has been published before, I did not stress enough that this form of analysis, while empirically based, actually runs counter to Bayesian theory and hypotheses testing methods.  
  
The reason for this is that in Bayesian analysis we draw our priors from external information, rather than from the data.  Then the goal is to allow the Markov Chain Monte Carlo (MCMC) simulations we do to find the best parameter estimates (peaks of the marginal densities of their posterior distributions i.e. likelihoods), without focusing on the starting parameters (priors) much themselves.  In other words, we use the priors to create distributions of values that the programs draw from during the analysis.  As I mentioned before, this means an ML-Bayes-stepwise approach requires "looking at the data twice" because we would have used the data to generate the priors.  This is opposed to Bayesian inference and creates an unnecessary step.  
  
After reading through the Migrate-N google group, it has become obvious to me, mainly from Peter Beerli's comments and criticisms, that the best way to start with Bayesian runs in Migrate-N with little _a priori _information is to use reasonable uniform priors for theta and _M_ and allow the program to do it's job.  For mtDNA, Beerli has suggested using a uniform theta prior between min = 0.0 and max = 0.1 and setting the prior for _M_ around means of 100 or 1000 with ranges from 0 to 1000 or 10000.  These may be broad, but they seem highly realistic i.e. likely to capture the values of these parameters from natural populations, and that is very desirable.  Personally, I feel that a theta-max of 0.1 is a bit high since I have never seen such a theta actually reported for a censused or indirect (e.g. popgen) estimate of this parameter in any published study.  That doesn't mean it has never happened, of course, and we should remember that "population" can be defined in multiple ways given different assumptions about the systems under study.  To illustrate why I think this is a high value, let's imagine a breeding population of vertebrates with (mtDNA-derived) theta = 0.1 and known generation time (2 years) and mutation parameter (mu = 1.0 x 10^-9).  We can convert theta theta to Ne simply by dividing theta by mu, which gives us Ne = 10^8!  This is scarcely a believable Ne value for any vertebrate at any level of biological organization of individuals that we would like to consider our population!  It even strains credulity for the most abundant vertebrates on the planet, including humans with a current population size of around 7 billion but an estimated Ne that is rather small as well as a historical Ne that is known to have been much smaller.  A lower more realistic set of values should be obtained for regional groupings (up to something like 0.001) or local communities (something more like 0.0001).  
  
Another important point is that these prior values of our Bayesian runs should also not influence the results.  If your prior "drives" your results towards a particular value, then the data can be considered uninformative (e.g. if your prior mean is your posterior mean).  However, there will still usually be a correlation between the prior and posterior, yet of course essentially no relationship between these values and the likelihood as viewed by the joint-marginal distributions.

~J
