---
author: justin
comments: true
date: 2011-09-22 16:51:00+00:00
layout: post
link: http://www.justinbagley.org/120/statistical-phylogeography-tutorial-1-coalescent-simulations-in-mesquite-part-i
slug: statistical-phylogeography-tutorial-1-coalescent-simulations-in-mesquite-part-i
title: 'Statistical phylogeography tutorial #1: Coalescent simulations in Mesquite
  Part I'
wordpress_id: 120
categories:
- blog posts
- gene trees
- Mesquite
- Phylogenetics
- Phylogeography
- species trees
tags:
- coalescent
- gene tree
- Mesquite
- phylogeography
- simulations
- statistical phylogeography
- tutorial
---

**Part I. Draft 9/22/11**  

 WARNING: The following is based on my current understanding and use of [Mesquite](http://mesquiteproject.wikispaces.com) to perform coalescent simulations for phylogeographical hypotheses testing and is correct to the best of my knowledge, but I do not guarantee its accuracy. Also, you may not perform these analyses in the exact way or order that I have performed them. The following is based on a number of previously-published studies (e.g. Knowles 2001; Knowles & Maddison 2002; Carstens et al. 2004, 2005; Spellman & Klicka 2006; Shepard & Burbrink 2009). If you use my tutorial to conduct analyses, please (1) [email me](http://www.justinbagley.org/contact) or post to this blog and let me know (thanks!), (2) properly cite Mesquite documentation (see the new [wikispaces website](http://mesquiteproject.wikispaces.com)), and (3) report any errors you might find in my tutorial to me immediately, please. If you think you find a bug in Mesquite, report that to its developers.   

   

 **Data and getting started**  

 Assume sequences are each alleles, i.e. unique haplotypes, in a file with NEXUS format, with known locality information (preferably, including geographical coordinates) that you have mapped in space in relation to geography. Also assume your data are haploid and come from a non-recombining genome region (although multi-locus analyses are possible, published studies using reehe analyses described below have mostly worked with mtDNA; I am still learning the multi-locus approaches and I will post on them later, probably in a Part III). Now, open your DNA sequence matrix in Mesquite ("File > Open File").




_NOTE_: the version of Mesquite I am using as of this writing is 2.73, but many functions of the following simulations stem back to Mesquite 1.05; this also goes for the newer versions of the program.   

   

 **Import your gene tree**  

 Import a file with a tree representing your best estimate of the gene tree representing relationships among the localities/alleles in your sample. In many cases, this will be a 'best' tree with branch lengths from a [maximum likelihood](http://www.ihes.fr/~carbone/MaximumLikelihood2.pdf) search (e.g. using GARLI, PAUP*, PHYML, etc.) or [Bayesian inference analysis](https://en.wikipedia.org/wiki/Bayesian_inference_in_phylogeny). Make sure tip names along the tree match the taxon names in the data matrix and include contents while importing ("Taxa&Trees > Import File with Trees > Include Contents"). Change the Tree Window settings to show your branch lengths (Click the "Drawing" menu and choose "Branches Proportional to Lengths").  

   

 Remove outgroup taxa, if any, by opening the list of taxa (double click on it, or right click on the list name and select "List & Manage Taxa"), selecting unwanted taxa, and then choosing "delete selected taxa" from the "List" dropdown menu.  

   

 **Taxon blocks**  

 OK, now you have a block of taxa representing the genes in your original set of sequences. The default name will be Taxa. Change this to "genes". [NOTE: I use this name throughout, so be sure to follow this step to make this post easier reading.]  

   

 You need a block of taxa (or several such blocks) representing the populations or species containing your genes during the simulations. Make as many as you need. I have found it easiest to give each one a name starting with "species...". Name each species/population; usually I do this with acronyms for geographical areas or populations.  

   

 **Setting up your gene-species associations**  

 Now you need to specify an association between the genes and the species/populations blocks. To do this, click "Choose New Association"... from the Taxa&Trees menu. Usually, you would edit the taxa association after choosing the containing taxa (species/populations) as the first block and choosing the genes taxa block when prompted to select taxa a second time. After going through this series of two pop-up windows, you will be prompted to name the association. I often don the association with a simple name using the names of the blocks themselves, like "genes-species_2areas." Next, you would usually select to edit the new association from the perspective of the containing taxa.   

   

 **Set up your hypotheses, conduct the simulations, and look at the output/trees**  

 Now that you have your ML tree (or Bayesian tree) and your species/population blocks and their associations worked out, you can create user-defined trees for Mesquite to use during your coalescent simulations. Mesquite is flexible for this task, allowing users to manipulate default or imported trees in a number of ways. For example, you can insert nodes, change tree depth, prune branches, alter branch lengths by different kinds of transformations, specify branch widths (e.g. different effective population sizes through time, for modeling population expansions or bottlenecks), and more.




However, as exciting as this prospect may be, you must first decide which type of coalescent simulation(s) you would like to run. There are at least two options, again highlighting the flexibility of the simulation framework provided by Mesquite. You can (A) simulate gene trees and measure their discord in relation to species/population trees, then compare this discord (over all simulated trees, i.e. creating a distribution) to the observed discord between the same species/population trees and your gene tree topology (following the above, I am thinking of an ML tree). Alternatively, you can (B) simulate data sets that have the same characteristics as your data (i.e. under the same substitution model that you might select for the data using a program like [jModelTest 2](https://github.com/ddarriba/jmodeltest2), DT_ModSel, or [PartitionFinder](http://www.robertlanfear.com/partitionfinder/)), constrain them with your species/population trees, and use them to generate gene trees for computing a test statistic distribution similar to that in (A) to be compared to the value of the test statistic computed when comparing the observed data (gene tree) against the species/population trees. In this tutorial, I cover procedure (A). I will tackle (B) later (in a future Part II post). OK, so to accomplish (A) you need to:  

   

 (A1) generate your population trees,  

 (A2) evaluate the fit between your gene tree (here on, I am assuming you are using an ML tree) and each population tree using the test statistic,  

 (A3) generate sets of simulated trees along the population tree representing individual collection localities ('populations'),  

 and (A4) then fit your simulated trees within each population tree and compare the observed test statistic from (A1) with the distribution of test statistic values calculated for each simulated tree with respect to each population tree. There are several different ways to do this, but the following is suggested.   

   

 (A1) Pick one block of species/population taxa and create a new block of trees for those taxa from "Default Trees" ("Taxa&Trees > Make New Trees Block from > Default Trees"... then choose the corresponding species taxa block for the tips). Rearrange the branches to the desired species/population tree for those taxa. Don't necessarily worry about branch lengths.  

   

 (A2) Go ahead and fit your ML tree (gene tree) into this population tree. Have the population tree of interest open in a Tree Window by selecting "Analysis > Visual Tree Analysis > Contained Gene (or Other) Trees." Because the ML tree was the first tree imported, it is the first in the list Mesquite keeps for the current project and will automatically be chosen and fit into the population tree. Thisyields an awesome looking diagram where the population tree has thick blue branches, the gene tree has green branches, and a scale bar is provided in units of your tree's branch lengths. Click on "File > Save Tree as PDF" and specify a place to save an editable file of your nice new diagram (you can manually edit this file in Adobe Illustrator e.g. for changing the scale bar values).   

   

 (A3) Now, generate your simulated gene trees over the Fragmented Ancestor model. If the species/population tree you just worked with in the paragraph above didn't have tips representing each sampled population, then create a species/population tree representing the Framented Ancestor model by creating a new block of taxa representing each population (name it "species_2areas" or something like that), specifying a genes-species association between this new block and your genes (haplotypes; e.g. named "genes-species_2areas"), and creating a new block of trees with a default bush topology for this species taxa block. Choose to view the new tree block in a Tree Window. [On to simulating the trees we want...] Now create a new block of trees from simulation. Click Taxa&Trees > Make New Trees Block from > Simulated Trees > Coalescence in Current Tree with Migration.... Then, when prompted (Mesquite asks "Select taxa (for new trees block)"), select "genes" (the block of taxa containing your tips/haplotypes)... The next thing you will be prompted to provide is the taxa association that will be used to generate the simulated trees. Choose the association you created between genes and the Fragmented Ancestor model (e.g. "genes-species_15pops"). The next decisions will be made through a simulation window (in our case, headed: "Coalescence With Migration"). Here, you will need to specify the gene tree depth at which you will be simulating the trees, the probability of migration per individual per generation (e.g. 7.7753E-07, which I computed using several steps following analyses of one data set in [MIGRATE-N](http://popgen.sc.fsu.edu/Migrate/Migrate-n.html)), and (if you want; this is not required) the generation at which to produce a burst of migration during the simulation (i.e. at which generation to begin factoring migration among populations into the simulation; in my case, I specified 22000 generations, corresponding to the Last Glacial Maximum [LGM], assuming a generation time of 1 year for Alfaro cultratus and two other poeciliid fish species). You will then need to specify the number of trees to simulate (I used 500 recently, and so did Shepard & Burbrink 2009; Spellman & Klicka 2006 used 1000 simulated trees). Start the simulation. A window will pop up and update you on the program's progress ("Adding tree to trees block 234"). This could take a few minutes or an hour, depending on how large your data matrix is and whether you allow the program to do an exponential approximation or not. Wait patiently... go get a snack... call your mom... surf Netflix... etc. When the simulation is over, Mesquite will say, "The trees are now ready [Simulated Trees; name of tree block: "Simulated Trees"]. Would you like to open a tree window to display them?" The answer is Yes. Click Yes.   

   

 Mesquite will open a new Tree Window that you can take a look at your simulated trees within. Click Drawing > Branches Proportional to Lengths. Leave the tree form on Square tree (rectangular), or if you are adventurous click Drawing > Tree Form > Curvogram (Maddison and Knowles' favorite). Click the arrow button to go to the next tree... and repeat several times to look at the variation in your trees. They're really different right? This is because each individual gene tree reflects an independent, individual realization of a stochastic process of lineage sorting and the level of migration you input into the model. This simulation assumes constant population size from root to tips, and random mating.  

   

 OK, now to (A4). You need to fit your simulated trees into a population tree of interest that is NOT the Fragmented Ancestor model, in order to calculate some statistics of fit. So, if you don't have one, follow the steps above to generate a population tree (taxa block, association with "genes", and tree block) that fits this criterion. [pause] OK, now make sure your population tree is open in a Tree Window. Use the Visual Tree Analysis procedure mentioned above to fit the new block of simulated gene trees (Default name: "Simulated Trees") into the population tree (i.e. call visual tree analysis and specify "Simulated Trees" block). This will produce the awesome blue and gree gene tree-species/population tree diagram again. You may want to save this as a PDF. Now all of your simulated gene trees can be viewed within the population tree. Surf through a few of them to see what they look like in this orientation.   

   

 To finalize step (A4), we need to create a histogram chart representing the distribution of a statistic-of-fit calculated for all of the simulated gene trees with respect to the population tree and save the results. Pick a statistic, either Slatkin's "s" or the number of deep coalescences (nDC). I like nDC. Click "Analysis > New Bar & Line Chart for > Trees" and specify that you want to show a chart of values for the "genes" block. Click on "Stored Trees" when you see the "Source of trees (Tree chart)" window. Then choose "Deep Coalescences (gene tree)" for the "Value to calculate for trees." For "Contained (gene) tree interpretation", click "OK" to use the defaults. Mesquite will ask you which tree block to use. Now, at the "Use which tree block?" window, select "Simulated Trees." Then the last thing Mesquite will ask you is which association to use. Select the association between "genes" and your population tree (e.g. "genes-species_2areas") and create the chart from the block of Simulated Trees.  

   

 **The last step**  

 The final step in the analysis is to compare your observed test statistic to the distribution you just generated and derive a p-value (analogous to a one-tailed t-test). We are interested in whether the observed value falls below 95% of the null distribution. You could generate the p-value in a statistics software program using a normal distribution with the mean and variance (output by Mesquite) of the given distribution, or use percentiles.  

   

 More later...




Best, ~ J




**References**




Knowles (2001); Knowles & Maddison (2002); Carstens et al. (2004, 2005); Spellman & Klicka (2006); Shepard & Burbrink (2009); ...I'll add these references one day when I have time.
