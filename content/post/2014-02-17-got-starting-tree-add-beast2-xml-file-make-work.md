---
author: justin
comments: true
date: 2014-02-17 04:46:23+00:00
layout: post
link: http://www.justinbagley.org/511/got-starting-tree-add-beast2-xml-file-make-work
slug: got-starting-tree-add-beast2-xml-file-make-work
title: So you got a starting tree?  How to add it to your BEAST2 xml file and make
  it work for you
wordpress_id: 511
categories:
- BEAST
- blog posts
- XML
tags:
- BEAST
- starting tree
- tree
---

I have now for several months been happily using BEAST2 instead of Beast 1.7.5 or 1.8.x--I'm converted!  Thus far, datasets have run surprisingly smoothly, but for some recent analyses I have tried to jump-start things and ensure proper likelihood values at the onset of runs by including a starting tree in my xml input file.




[Previously, I blogged about just how you might create such a starting tree](http://www.justinbagley.org/113/off-to-a-good-start-how-to-generate-starting-trees-for-beast-or-beast-analyses-using-r) that fits one or multiple calibration points in a BEAST analysis, by using penalized likelihood analysis (r8s) in R.  However, another easy way to do this is to conduct a preliminary analysis using a short run specifying the full set of calibrations in BEAST2, and then to use the MCC tree from this run (or one post-burnin tree) as a starting tree for your final runs.  Either way, I have discussed how to generate starting trees.  Now, I'll round out this topic more with a brief post on how to _actually add_ the starting tree to an xml file for a BEAST2 analysis.




After you have an appropriate starting tree with no polytomies, you can add it to your BEAST2 xml file in three easy steps:




1. Search for the following code in your xml file output from BEAUti v2:



    
    init estimate="false" 




2. From the result of this search, identify the entire "init" command section, which looks something like this:



    
    <init taxa="@percichthyid_1,2" estimate="false" initial="@Tree.t:mtDNA_tree" id="RandomTree.t:mtDNA_tree" spec="beast.evolution.tree.RandomTree"> <populationmodel id="ConstantPopulation0.t:mtDNA_tree" spec="ConstantPopulation"> <parameter id="randomPopSize.t:mtDNA_tree" value="1" name="popSize"></parameter> </populationmodel> </init>




This code specifies a random starting tree and you'll notice that the relevant ID for the tree model looks the same throughout the xml (in this case stating "mtDNA_tree" after ".t").




3. Replace the init section with a few lines of code that look like this and contain a newick tree that you'd like to start with (which you must make sure has node ages that fit within the hard bounds of any calibration points in your priors, and again has no polytomies), which might look something like this in general form:



    
    <init islabellednewick="true" initial="@Tree.t:x" id="StartingTree.t:x" spec="beast.util.TreeParser"> <input name="newick"> (newick tree); </input> </init>




…but more like this with the correct information (x) filled in:



    
    <init islabellednewick="true" initial="@Tree.t:mtDNA_tree" id="StartingTree.t:mtDNA_tree" spec="beast.util.TreeParser"> <input name="newick"> (Bovine:0.69395,(Hylobates:0.36079,(Pongo:0.33636,(G._Gorilla:0.17147, (P._paniscus:0.19268,H._sapiens:0.11927):0.08386):0.06124):0.15057):0.54939, Rodent:1.21460); </input> </init> 




Note that we actually specify ("spec=") the starting tree with the "beast.util.TreeParser" class.  Now, check to make sure your xml file runs, indicating that your tree is a good fit to your priors and produces a good starting likelihood.  If you observe the xml with the starting tree specified running and correctly calculating likelihoods, then you've gone from just having a starting tree to making it work for you!




~J




**References**




[http://www.beast2.org/wiki](http://www.beast2.org/wiki)




[Beast book](http://beast2.org/book.html)







PS: A slightly more simple way to do step three would be to use this instead (because I think "spec" is sufficient to initialize the starting tree, i.e. "initial=" may not be needed):



    
    <init islabellednewick="true" initial="@Tree.t:mtDNA_tree" spec="beast.util.TreeParser" id="StartingTree.t:mtDNA_tree"> <input name="newick"> (Bovine:0.69395,(Hylobates:0.36079,(Pongo:0.33636,(G._Gorilla:0.17147, (P._paniscus:0.19268,H._sapiens:0.11927):0.08386):0.06124):0.15057):0.54939, Rodent:1.21460); </input> </init> 




PS2: If you try the code in the starting tree section on the beast2 wiki (link above), you will probably get an error that stateNode is not a tag used used by the mcmc.  This is why I have stuck with "init" here.  Here is what said error message will look like:



    
    Error 130 parsing the xml input file 
    This plugin (mcmc) has no input with name stateNode. Choose one of these inputs:
    chainLength,state,storeEvery,preBurnin,distribution,operator,logger,init,sampleFromPrior,operatorschedule 
    Error detected about here: 
    <beast> 
    <run id="mcmc" spec="MCMC">
    
