---
author: justin
comments: true
date: 2013-10-10 20:35:00+00:00
layout: post
link: http://www.justinbagley.org/113/off-to-a-good-start-how-to-generate-starting-trees-for-beast-or-beast-analyses-using-r
slug: off-to-a-good-start-how-to-generate-starting-trees-for-beast-or-beast-analyses-using-r
title: 'Off to a good start: how to generate starting trees for BEAST or *BEAST analyses
  using R'
wordpress_id: 113
categories:
- blog posts
- Programming
- R
---

**BEAST and user trees**




The program BEAST (e.g. latest release version [v1.8.0](http://beast.bio.ed.ac.uk/Main_Page#BEAST_v1.8.0_has_been_released); or [v2.1.1](http://www.beast2.org/wiki/index.php/Main_Page#BEAST_Core_v2.1.1_has_been_released); Drummond et al. 2012) is increasingly more and more popular and important in the fields of evolutionary biology and the biology of infectious diseases. When conducting MCMC simulations to simultaneously make phylogenetic inference and estimate divergence times, and/or coalescent model parameters (summary statistics) in BEAST, it is usually necessary, and desirable, to provide some form of calibrated tree priors. Such calibrations are a critical aspect of Bayesian evolutionary analysis in the program, in both theory and practice.




However, calibrated tree priors can be problematic for several reasons. For example, there can be problems with setting these calibrations themselves. Data on biogeographical, geological or fossil calibrations may be unavailable, or alternately available calibration points may have large or ambiguous amounts of uncertainty. Researchers also face the problem of correctly inputting calibrations into the program, through the utility program BEAUti. I will cover this and suggest resources for dealing with these issues elsewhere. _In addition to these issues, a key practical issue is that when users impose tree priors this often means that they need to specify a starting tree topology for their BEAST analysis, which should be added to the xml input file. _This latter problem affects analyses in BEAST, or in the multispecies coalescent model implementation of *BEAST that is also run in BEAST for species tree estimation.




In this post, I show you how to get "off to a good start" by generating a starting tree for your BEAST or *BEAST analyses.




** ****Generate a starting tree that fits your calibration, using R**




There are several ways you can make starting trees for BEAST, including using programs as diverse as TreeEdit, Mesquite, r8s, etc. However, the idea is in general to take a Bayesian or ML tree topology inferred from a separate phylogenetic analysis in a program such as MrBayes or GARLI (respectively), and then to manipulate the branch lengths in some way to get to the right starting tree--with branch lengths in units of time matching the units specified in your xml file for your BEAST run.




In TreeEdit and Mesquite, you can basically import a starting tree topology with branch lengths output from the above programs in substitutions/site and move them around to fit your needs, and then use an iterative scaling and manual tree-editing approach to get the right time tree. I take a slightly different approach using some commands that allow me to run an algorithm from r8s in the R environment without having to manually alter the topology; for this, we are going to use the package ape (Analysis in Phylogenetics and Evolution), by Emmanuel Paradis, to make our starting tree.




Before starting, you might need to get familiar with the R basics, e.g. by reading my previous post [here](http://www.justinbagley.org/119/r-functions-for-working-with-phylogenetic-trees-in-packages-ape-geiger-and-caper-part-i), or using resources [like this one](http://cran.r-project.org/doc/manuals/R-intro.pdf) (R intro), or [this one](http://www.r-phylo.org/wiki/Main_Page) (R-Phylo phylogenetics wiki). OK, so do that if necessary. Then, here we go...




Open R and load the package we need by typing library(ape). Move the tree file or files (newick text, .NEX, .tre formats, etc.) you are interested in into your current R working directory. Assuming the file of interest is a newick format tree in a file called "fishes.tre", or a NEXUS style tree file named "fishes.NEX", type the following to read your tree in and plot it:





[code language="r"]## Read in Newick format tree file
fishtree = read.newick(file='fishes.tre')
## NEXUS style tree file
fishtree = read.tree('fishes.NEX')
## Here's the basic way to plot your tree:
plot(fishtree) 
## and here's a slightly more sophisticated way to plot a phylogeny using ape: 
plot.phylo(fishtree, cex=0.4, no.margin=TRUE)
#
## After plotting the tree, we can use a simple command to add an x-axis scale by typing… 
axisPhylo()
## however, ape allows more flexibility with the 'add.scale.bar' function, like this:
add.scale.bar(cex=0.4, font=4, col='red')[/code]





Now, we're up and running and your tree is looking pretty good (pretty cool).  The next step is to take your calibration information and identify which node of the phylogeny you are going to be applying it to. Look at the plot or another reference figure of your tree and determine two taxa for which this node represents their most recent common ancestor, or "MRCA." Write the names down in a text editor (I'm on mac, and I prefer TextWrangler). You can then copy and paste these into the editor window directly from your treefile or get them from R. So far so good, but you also need to know the number identifying the node of interest on your tree, which isn't readily apparent. Let's get this in R, as follows:



[code language="r"]mrca(fishtree)['taxon1', 'taxon2']
## Let's imagine for our example that you type the above... and
## you get the following output:
## [1] 75[/code]



This returns the number of the node, which is node number "75" in the example above. Armed with the information you get from this step, you will next pass a string to the program to alter your tree and generate a tree topology using penalized likelihood, and by specifying the constraints of our calibration for this node we will be able to ensure that the resulting tree will fit within the bounds of those constraints and thus work in BEAST! The subroutine we'll use is called chronopl, and while not supported by some versions of the package this function is _currently available_, which is good news for us. Here's the code for a basic implementation of the chronopl function:



[code language="r"]outputtreeNAME = chronopl(inputtreeNAME, lambda=lambda value,
    age.min=value, age.max=value, node=nodeNUMBER, S=No. DNA bp,
    tol=tolerance value)
[/code]



And here's how I'll run it for our example, which we'll say is starting from a topology generated by ML analysis of just over 5 kb of DNA sequence data, and which involves a calibration ranging between 30-10 Mya (million years ago) at node 75:



[code language="r"]fishtree.pl.cvl1 = chronopl(fishtree, lambda=1, age.min=10, age.max=30, node=75, S=5100, tol=1e-8)[/code]




If you want, you can also specify for a cross-validation procedure to be run with chronopl function, like this:






[code language="r"]fishtree.pl.cvl1 = chronopl(fishtree, lambda=1, age.min=10, age.max=30, node=75, S=5100, tol=1e-8, CV=TRUE, eval.max=500, iter.max=500)[/code]






This will iteratively drop each tip in the phylogeny and do some cross-validation steps on it (iter.max controls the number of iteration steps that will be run, and increasing this number will result in a longer time to completion), which you can figure out, but which are not part of the output of running a summary of the results. At any rate, after using either of the strategies for running chronopl above, you now have an appropriate starting tree for BEAST. The last thing you need to do is write this tree to a file that you can use, in newick format, and supply this tree in your xml input file. To write your penalized likelihood time tree output above, do something like this:






[code language="r"]write.tree(fishtree.pl.cvl1, file='fishtree.pl.cvl1.newick')[/code]






Now your tree is available in a newick file that has been written to your present R working directory. So, go get your tree and use it and you're done! Of course, we can imagine more complex cases with multiple calibration points, and these can also be accomodated using similar functions to those above. But more on that later, gotta run.







~ J







**References**







Drummond AJ, Suchard MA, Xie D, Rambaut A (2012) Bayesian Phylogenetics with BEAUti and the BEAST 1.7. _Molecular Biology and Evolution_ **29**:1969-1973.









