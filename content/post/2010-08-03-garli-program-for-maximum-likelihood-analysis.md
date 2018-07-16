---
author: justin
comments: true
date: 2010-08-03 15:17:00+00:00
layout: post
link: http://www.justinbagley.org/141/garli-program-for-maximum-likelihood-analysis
slug: garli-program-for-maximum-likelihood-analysis
title: GARLI - program for maximum likelihood phylogenetic analysis
wordpress_id: 141
categories:
- blog posts
- GARLI
- Maximum likelihood
- Phylogenetics
- Software
tags:
- bootstrap
- GARLI
- ML
- phylogeny
- software
---

##### Introduction 

I have been using the program GARLI (Zwickl 2006) for several years now, both all during my master's and now during my PhD work, for maximum likelihood analysis. Here are some links for the program and some tips / info about how I use it for partitioned analyses (more later).  
  


##### GARLI

Get the program (be prepared to give your name, email and institution information):  [GARLI download request](http://www.nescent.org/informatics/download.php?software_id=4)

 

[GARLI manual website with option to link to download manual in pdf format](https://www.nescent.org/wg_garli/Manual)

 

Model specification and configuration settings:

[https://www.nescent.org/wg_garli/GARLI_Configuration_Settings#Model_specification_settings](https://www.nescent.org/wg_garli/GARLI_Configuration_Settings#Model_specification_settings)

 

FAQ - my favorite frequently asked questions link for this software:

[https://www.nescent.org/wg_garli/FAQ#MODELTEST_told_me_to_use_model_X.__How_do_I_set_that_up_in_GARLI.3](https://www.nescent.org/wg_garli/FAQ#MODELTEST_told_me_to_use_model_X.__How_do_I_set_that_up_in_GARLI.3F)

 

##### How I use GARLI

GARLI has a number of very useful features.  For example, it can run a number of different models, it can estimate all model parameters (you can specify a user tree or not), its runs are usually very fast and efficient, and its bootstrapping method is thorough (for time limitations I suggest running this on a supercomputer, since this analysis takes much longer usually than the normal runs).  Others have taken advantage of GARLI in several ways.  One that I hope to benefit from and cite is Kurt Galbreath's GARLI scripts, e.g. using GARLI to perform parametric bootstrapping (SOWH test).  

 

To specify character sets in GARLI i.e. for multi-locus or partitioned analyses, add the following lines to the end of your NEXUS file:

 
    
    begin sets;
     charset cytb = 1-601;
     charset coi = 602-1253;
     charpartition byGene = chunk1:cytb, chunk2:coi; 
    
    END;

This is an *example* and things may change with different data sets  Anyway..._THEN..._in the garli.conf file you may want or need to add model specification information for each character set.  Do it like this: 

 
    
    [model0]
    datatype = nucleotide
    ratematrix = 6rate
    statefrequencies = estimate
    ratehetmodel = gamma
    numratecats = 4
    invariantsites = estimate
    
    [model1]
    datatype = nucleotide
    ratematrix = 6rate
    statefrequencies = estimate
    ratehetmodel = gamma
    numratecats = 4
    invariantsites = estimate
    
    [partition]
    linkmodels = 0
    subsetspecificrates = 1

 

****BEWARE: This script is an example for two genes.  This script also will not work if you change the model names in brackets.  All of the settings can be changed but be careful... e.g. there is no "equal" option for "ratehetmodel" as you might think (if you don't think enough like me sometimes!).  The partition portion of this script allows the models to be unlinked so that parameters are estimated separately for each gene.  See manual for more information. 

 

I usually run GARLI with a .conf file specifying up to 5 x 10^6 generations, but for simple data sets GARLI often finishes (see manual) much sooner than this.

 

~J

 

**References**

Zwickl 2006.
