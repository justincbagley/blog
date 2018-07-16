---
author: justin
comments: true
date: 2011-09-01 23:38:00+00:00
layout: post
link: http://www.justinbagley.org/123/beast-and-the-beast-basics-molecular-clocks-and-how-to-input-rates-into-beast
slug: beast-and-the-beast-basics-molecular-clocks-and-how-to-input-rates-into-beast
title: 'BEAST and the BEAST basics: molecular clocks and how to input rates into BEAST'
wordpress_id: 123
categories:
- BEAST
- blog posts
- Molecular clocks
- Software
tags:
- Bayesian phylogenetics
- BEAST
- molecular clocks
- software
- substitution rate
- tutorial
---

#### **BEAST basics**




##### **A brief introduction to BEAST **




  

 BEAST is a powerful computer program for evolutionary analysis developed by Andrew Rambaut and Alexei Drummond, as well as Marc Suchard, Simon Ho, Joseph Heled, and others. BEAST was originally designed to provide a [Bayesian](https://en.wikipedia.org/wiki/Bayesian_inference) [Markov chain Monte Carlo (MCMC)](https://en.wikipedia.org/wiki/Markov_chain_Monte_Carlo) method for simultaneously co-estimating phylogenies and divergence times (times to the most recent common ancestor, TMRCAs) from DNA sequence data (or amino acids) for one or multiple loci. However, it has now been extended to trait data and provides means of testing for correlated trait evolution. It currently implements a wide variety of evolutionary models. For those interested in studying phylogenetics, phylogeography and demography in a Bayesian framework, BEAST is a choice option for analysis, being among the premier tools in each of these fields.  

   

 Before reading the rest of this post, make sure you have downloaded BEAST. You can get the latest version at the BEAST website, which can be accessed by clicking [here](http://beast.bio.ed.ac.uk/Main_Page) [_Updated May 2016:_ or you can download BEAST2 [here](http://beast2.org)]. I'd also point out that BEAST developers have provided a very useful set of [tutorials](http://beast.bio.ed.ac.uk/Tutorials) as well as a frequently-visited [google group](http://groups.google.com/group/beast-users?pli=1) for discussing and dealing with issues related to BEAST analysis.  Like other programs common to molecular ecology and evolutionary genetic analysis, e.g. migrate, first learning to use BEAST can be challenging. Fortunately, the program has grown quite a bit since earlier versions, with more flexibility (options) and a more user-friendly interface in BEAUTi for generating input files (less direct [XML](https://en.wikipedia.org/wiki/XML) file editing).   

   

 ****




##### **Molecular clocks in BEAST**




[Molecular clocks](https://en.wikipedia.org/wiki/Molecular_clock) play a key role in all of the models implemented in BEAST. Despite the good documentation and support mentioned above, however, a frequently asked question regarding setting up BEAST runs is, "I have an idea of what rate I would like to use in my analysis, but how do I input it into the program?" In response to such questions, the purpose of this post is to practically introduce readers to the way strict molecular clocks are used in BEAST. Although BEAST implements three different molecular clock models (strict, relaxed, and random), I focus on strict clock analyses where users will want to set mutation rate priors. Assuming a strict or "global" molecular clock will often be a poor assumption for interspecific molecular data, because rates vary among lineages; however, in programs such as BEAST that are based on the coalescent (which is usually assumed to tick at a strict pace), when users analyze large intraspecific datasets, relaxed clocks are almost always inappropriate. Thus for intraspecific phylogeography of a single mtDNA locus, for example, a strict clock will usually be preferred.   

   

 **Clock setting in BEAST**  

 To set up a strict clock run in BEAST, the user must specify a strict molecular clock in their input (.xml) file. This is accomplished when creating the input file in the utility program BEAUti, which is part of the BEAST installation. After importing your NEXUS-formatted DNA seq data into BEAUti, select the desired taxon sets and site model(s) for the analysis.  Next, click on the "Clocks" tab (this applies to BEAUti 1.7.4; older versions of this software may have a tab named "Clock Models"). The strict clock model is the default setting.  Importantly, clock rates if constant can be spread across a range of values (e.g. uniform prior); however, a constant mutation rate is not necessary, and mutation can be modeled using several distributions.  For simplicity, let's set the clock first; we will discuss these distributions a little later.  

   

 In BEAST, we input the mutation rate using the 'clock.rate' parameter, which is in units of substitutions/site/unit time (default). The default value for this parameter is 1.0. If you leave the clock.rate parameter set to 1.0 and do not check "estimate," then you are going to get a resulting phylogeny or demographic model with units of substitutions/site, the same as if you were just reconstructing a phylogeny using standard maximum likelihood or Bayesian inference analysis methods. However, when analyzing multilocus datasets using strict molecular clocks on each locus in *BEAST, you can leave the "estimate" box unchecked for one locus (e.g. imagine the first locus you sampled/entered was a chunk of mtDNA sequence) leave the clock.rate parameter set to 1.0, while checking "estimate" for the others. In this case, BEAST will estimate rates of every other locus relative to the one whose rate was set to 1.0.  For the present tutorial, leave the strict clock model selected.  

   

 Now that you have specified the strict clock model, you will need to place a prior on the clock.rate parameter. You now need to set up code in the input file that will supply the program with your rate or rates. How you do this will depend on what your rate/data is and your desired outcome.  Here are three potential situations you might be in:  

   

 **_(1) "I have a pairwise rate.  How do I go from pairwise to per-lineage rates and input them into BEAST?"_**  

 Usually, when we discuss evolutionary rates, or mutation rates, it is understood that we are talking about 'per-lineage' rates.  This is not surprising given evolution occurs along individual branches/lineages in the tree of life. Thus, BEAST works with per-lineage rates. However, pairwise rates of evolution are commonly reported and thus of interest as candidate priors.  When we talk about divergence as a percentage, x% pairwise divergence between two lineages is equivalent to x%/2 divergence per lineage (along one branch of a two-tip phylogenetic tree).   

   

 Imagine you are interested in the standard 2% rate for vertebrate mtDNA evolution.  _This_ is a _pairwise_ rate (2%/million years, Myr). If you wanted to set the program (i.e. fix it) to exactly this rate (taking it as a mean rate across the phylogeny of your samples)... then the rate _must be converted to a per-lineage rate in units of substitutions/site_ before being input. To obtain a per-lineage rate from a pairwise rate, you simply divide the pairwise rate by 2. The above rate becomes 1% when expressed as a percentage, and we divide this value by 100 to get 0.01 expressed in substitutions/site/Myr. Once you have this value, you need to simply leave the "estimate" box unchecked, check the "Fix mean substitution rate" box, and enter your rate to set the mean clock.rate in your xml file. Here, we are assuming that you want your units (hence the scaling of your output) to be in millions of years (Myr).   

   

 But there are other options... and we can imagine other cases.  

   

 For example, you may want the _x_-axis of your BEAST output files (e.g. for your time tree or Bayesian skyline plot) to be in units of years. To accomplish this, you need to format the desired rate value appropriately. In the case of a pairwise rate such as the 2%/Myr rate in the example above, you would divide 0.01 by 10^6 (one million), leaving you with 1.0 x 10^-8 or 0.00000001. This is the value you would input into BEAUTi to achieve the result desired here. This assumes generation time = 1.0 yr (thus you could think of it as the output actually being in generations).   

 _  

 __Note_: if you had a fossil calibration point dated in Ma and you checked "estimate" for your rate under a model specifying a strict clock and input your fossil calibration, the resulting output would also be in Myr. So, if your fossil is 30 Ma +/- 2 Ma for a given node, you would input that into the program as a point estimate of 30.0 (fixed; also you could use a variety of calibration transformations/distributions; see below). And you would get output in units of Ma.  BEAST would also estimate the substitution rate in subs/site/Myr for you.  

   

 **_(2) "I have a per-lineage rate(s)."_**  

 If you have a per-lineage rate already... put it in the program as discussed above.  

   

 **_(3) "I don't have rates... (Or, what is a molecular clock anyway?)"_**  

 If this is your situation, then wow, maybe I should have started this post by explaining this!!  If rates are not available (i.e. published) for your taxa or nodes of interest, then you may want to roughly estimate a rate to use in your analysis. For this, you would need a justifiable calibration point (e.g. fossil data, or information on a biogeographical or paleogeographical event, etc.) and an in-hand estimate of _d_,_ _pairwise genetic divergence (i.e. DNA sequence divergence). Care must be taken in doing this and in setting the priors on the rate distribution (e.g. your outcome will depend on your choice and quality of _d _calculation and calibration point selection), but if you need to do this then you must first understand the basic molecular clock model.  

   

 To understand the molecular clock, let's imagine a two-taxon phylogenetic tree representing the relationship between two sister lineages. You have sequence data from these lineages and you calculate the pairwise divergence, _d_xy_ _(= mean # differences, i.e. mean # nucleotide substitutions/site), between the two sequences. This value is a product of mutation rate (mu) in substitutions/site/Myr and the amount of time since two unique lineages diverged (originated). Given this information, the simplest calculation of the time (_T_) of divergence in millions of years ago (Ma) for a given lineage is calculated by taking _d_xy and dividing by twice the substitution rate (mu; the mutation rate). In other words _T_ = _d_xy/2mu [this is commonly also written as _T = (d_xy/mu)/2, as in Nei (1987)]. Since you need to calculate a rate, you need prior information on the splitting time/event leading to the level of observed divergence.  So you need to re-arrange this equation.  To obtain a per-lineage rate (what we want!), you see that mu = _d_xy/2_T_ [which is the same as (_d_xy/_T_)/2]. If you have an estimate of 4% divergence between two lineages and you know that this _d_ is at least as old as a certain number, say 5 Ma (based on the geological date of a mountain chain uplifting rapidly or some other vicariate event), you could calculate a per-lineage rate as 4/(5*2) = 0.4%/My, assuming a global clock. This would be input into BEAST as 0.004, in units of substitutions/site/Myr.  But, again, you could input this number into BEAST in other ways.  As discussed in (1) above, if you want the results to be in years, take your 0.4%/Myr rate and divide it by a million, and this leaves you with 4 x 10^-9, or  "0.000000004", to enter into the program (assuming generation time = 1 yr).  

   

 _Prior distributions on clock.rate_  

 The most simple way of inputting an evolutionary rate is to leave clock.rate set to a point estimate; however, this is hardly realistic, and you will probably want to factor in some uncertainty in this estimate. When doing so, the most simple prior distribution that can be placed on the clock.rate parameter in BEAST is a uniform distribution.  _More coming soon_...  

   

 OK, that's all for now on this particular topic.  Hope this helps.  ~ J  

   

 **References**





Nei, M., 1987. Molecular Evolutionary Genetics. Columbia University Press, New York.



