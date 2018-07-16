---
author: justin
comments: true
date: 2011-11-22 08:15:00+00:00
layout: post
link: http://www.justinbagley.org/119/r-functions-for-working-with-phylogenetic-trees-in-packages-ape-geiger-and-caper-part-i
slug: r-functions-for-working-with-phylogenetic-trees-in-packages-ape-geiger-and-caper-part-i
title: 'R functions for working with phylogenetic trees in packages ape, geiger, and
  caper: Part I'
wordpress_id: 119
categories:
- blog posts
- command line
- R
tags:
- ape
- phylogenetic trees
- phylogenetics
- R
- trees
---

OK, in this post I will be reviewing some R functions for phylogenetics, walking you through some ways of working with phylogenies within the R environment. First, install R (http://cran.r-project.org/) on your computer. Also install the phylogenetics packages APE (http://cran.r-project.org/web/packages/ape/index.html), geiger (http://cran.r-project.org/web/packages/geiger/index.html) and caper (http://cran.r-project.org/web/packages/caper/index.html) on your machine using links at these URLs, or using the 'Install packages' option within the 'Packages' dropdown menu of the R gui), in the appropriate library folder (e.g., C:\Program Files\R 2.xx\library...). Within the 64-bit R console on my MacBook Pro, I just go to 'Packages & Data' and click on the 'Package Installer' to get new packages.  

   

 **First steps, and getting trees into R**   

 Now, let's do some stuff with phylogenetic trees in R. Our first step is to obtain trees of interest, then get them into R to play with them and to conduct analyses with them. If you have no tree, but you have a data matrix, you can construct phylogenetic trees using a variety of R packages (e.g. phangorn, bblme). For the rest of this particular post, I will assume you already have one or more phylogenies to work with.   

   

 I will also assume you understand some basic R commands (e.g. "gets," or = , and that you know bigdata[,x] is a column, etc.) already. Please read up on the basics beforehand if you haven't.   

   

 Before taking our first step and reading in a treefile, we need to make sure that the packages we will be using are ready. Type library(ape) library(geiger) library(caper) to load the appropriate packages. All code below will assume that you have loaded these packages; these codes will not work without them, thus this is an important point. Also put any tree files (newick text, .NEX, .tre formats, etc.) you are interested in into your current working directory. You can find out what your current working directory is by typing getwd(), and then you can change this using setwd() and filling in the parenthesis with the location of the desired directory location (note: use forward slashes, not backslashes when typing this in). Assuming the tree file of interest is called "bigtree.tre", type





[code language="r"]bigtree = read.tree(file='bigtree.tre')
#or you could also try:
bigtree = read.nexus(file='bigtree.tre')
#if you would like to read in a nexus file. [/code]







To view your phylogeny, type










[code language="r"]plot(bigtree) [/code]










Add an axis representing your branch lengths, after the tree graph shows up in a separate window within your R gui, by typing the following code:









[code language="r"]axisPhylo()
#...or add a small scale bar like this:
add.scale.bar() [/code]









Alternatively, to get a tree file in manually, you might insert your tree (copy and paste in standard newick format with or without branch lengths, and making sure that you have no spaces in your tip labels) in between the first set of quotation marks ("") that I have left blank here:









[code language="r"]cat('', file = 'treename.tre', sep = '\n')[/code]









This creates the tree file "treename.tre" in your working directory with your tree in it. Simply type treename , then plot(treename) to see your phylogeny. Now that your tree is in R, you probably will want to save it. To save your tree in NEXUS format, simply use the command write.nexus("treename", "treename.nexus"). To see a summary of the features of your tree type its name treename. To see a summary of tip labels along the phylogeny, type something like treename$tip.label. To see branch lengths, type treename$edge.length.   

   

 **More basic tree features, and changing how trees look**   

   

 Now that you have learned to input trees of object class "phylo" in R, it would be useful to know how to do some basic editing/tree handling procedures. First, you might like to know your node numbers. The fastest way to get this information any particular node is to use the following code then click near the node of interest, and watch as the value will be returned.









[code language="r"]## For a tree named x:
plot(x)
identify(x)
Click close to a node of the tree...
$nodes
[1] 108[/code]









However, you could also open your tree in Mesquite, open it in a tree window, then click on the text tab to see your tree in text format. That would also give you node numbers.  

   

To get all of the node numbers while visualizing your tree in R, try something like this (again for a tree named x):








[code language="r"]plot(x)
nodelabels(adj=c(0,-1), frame='n')[/code]








Another thing you might also be interested in would be plotting branch lengths along the branches, or looking at different branch length parameters. Try this (again for a tree named x):








[code language="r"]## This code gives all of the branch lengths:
x$edge.length
## This code plots branch lengths along the tree:
plot(x)
  
## Get the root branch length itself like this:
x$root.edge[/code]








  

  

  

**Branch length transformations**  

** **One of my favorite things to do with phylogenies in R is to play around with different branch length transformations. Changing the branch lengths of your phylogeny might be something you might would want to do in a number of different ways, at different times, and with several important consequences. For example, branch length transformations allow you to alter your phylogenetic hypothesis to reflect different relative rates of evolution. Trees with different branch lengths, hence representing different evolutionary models, can then be compared with likelihood ratios or AIC scores... or placed into statistical phylogenetic models of trait data (e.g. logistic regression models or different models of character evolution), which can also subsequently be compared using model selection techniques. You might also need a bank of trees with the same topology but different branch lengths to test which set of branch lengths is most appropriate for a given analysis, or test which tree has branch lengths that provide the best fit to a certain model of interest.  

   

   

 **References and links**  

 Here are some links to some content related to phylogenetics and R from the Berkeley Integrative Biology (IB) program and a couple other places, which I have drawn from and will continue to use as resources as I add more content to my blog about phylogenetics in R. I'm going to draw up a little bibliography on the best reading in phylogenetic comparative methods as well, as I develop these new sections of the blog further...  

   

   

 Berkeley resources, mostly developed by Nick Matzke (Thanks Nick!):  

 http://ib.berkeley.edu/courses/ib200b/IB200B_Readings.shtml#history  

 http://ib.berkeley.edu/courses/ib200a/lect/ib200a_lect14_Matzke_Bayesian_phylogenetics.pdf  

 http://phylo.wikidot.com/workshop:methodological-workshop-on-biodiversity-dynamics  

 http://ib.berkeley.edu/courses/ib200b/labs/_ib200b_lab4_R_continuous_characters_v1.R  

 http://ib.berkeley.edu/courses/ib200b/labs/lab10/ib200b_lab10_evodevo_v2.R  

 http://ib.berkeley.edu/courses/ib200b/labs/lab12/ib200b_lab12_lineages_thru_time.pdf  

 http://ib.berkeley.edu/courses/ib200b/labs/_dating_code_v1.R  

   

 Ape package installation issues: http://blog.gmane.org/gmane.comp.lang.r.phylo/month=20100601   

   

 phylo wikido stuff: http://phylo.wikidot.com/intro-to-r-continued:phylogenies-continuous-characters  

 http://phylo.wikidot.com/phylogenetically-independent-contrasts   

   

 Cutting a tree at a given time interval: https://stat.ethz.ch/pipermail/r-sig-phylo/2011-July/001495.html  

   

 Phylogenetic comparative methods wiki resource: http://www.r-phylo.org/wiki/Main_Page  

   

 Charles Nunn's AnthroTree website, phylo branch length transformations, evolutionary models, and detecting evolutionary trends: http://nunn.rc.fas.harvard.edu/groups/pica/wiki/a6fd9/Chapter_5Modeling_Evolutionary_Change.html, http://nunn.rc.fas.harvard.edu/groups/pica/wiki/ccf76/47_Detecting_Evolutionary_Trends_from_a_Dated_Phylogeny.html   

   

   

   

   

 ~ J
