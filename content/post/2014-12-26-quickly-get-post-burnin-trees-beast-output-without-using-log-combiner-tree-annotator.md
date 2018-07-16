---
author: justin
comments: true
date: 2014-12-26 11:06:40+00:00
layout: post
link: http://www.justinbagley.org/509/quickly-get-post-burnin-trees-beast-output-without-using-log-combiner-tree-annotator
slug: quickly-get-post-burnin-trees-beast-output-without-using-log-combiner-tree-annotator
title: Alternative ways to quickly get post-burnin trees from BEAST output from the
  command line
wordpress_id: 509
categories:
- bash
- BEAST
- blog posts
- command line
- shell scripts
tags:
- BEAST
- command line
- phylogeny
- Terminal
- tutorial
---

Evolutionary biologists generally use nice java-written utility programs that come in the standard [BEAST](http://www.beast2.org) distribution to obtain post-burnin trees for summarizing the results of a converged BEAST run (or *BEAST run) that reached stationarity.  Usually, only 5,000 to 20,000 trees are necessary for this, and these are typically obtained by cutting out 'burnin' trees and then "thinning" trees from ".trees" output files using LogCombiner until the desired number of trees is reached.  These post-burnin trees can then be input into TreeAnnotator, where they can be summarized to reveal the topology that is best supported by the posterior distribution of trees, often by creating a maximum clade credibility (MCC) topology with posterior probabilities along each node.  Then, FigTree is used to visualize this MCC tree and parameter estimates output by the program (e.g. divergence time intervals).




However, one alternative method for quickly getting post-burnin trees from BEAST output without using LogCombiner or TreeAnnotator would be to do so directly from the [command line](http://en.wikipedia.org/wiki/Command-line_interface) (e.g. in [Terminal](http://guides.macrumors.com/Terminal) on my MacBook).  I'll be exploring some command-line possibilities for doing this here in this post.




Once the resulting treefile from a BEAST analysis is checked in Tracer to confirm that the MCMC has converged and reached stationarity, the file can be manipulated in several ways as follows to grab a random subset of post-burnin trees.  In the examples below, we'll extract 5,000 random trees from the last 20,000 trees from the run (from a treefile called "cytb_gene.trees") or grab 10k random trees from an entire file, but you can change the size of the chunk of trees that you obtain your random trees from to any size you wish.




Trick #1 - using the "tail", "sort", and "head" commands to randomize the contents of a post-burnin set of trees from the end of the file and output them to a new file:






    
    cd /PATH/TO/DIR/WITH/cytb_gene.trees
    tail -n 20000 cytb_gene.trees > 20k_trees_use.tre
    sort -R 20k_trees_use.tre | head -n 5000 > 5k_random_trees.trees
    #
    ## Check the length of the resulting file...
    wc -l 5k_random_trees.trees










Trick #2 - using the "tail" and "awk" commands to randomize the contents of a post-burnin set of trees from the end of the file and output them to a new file:






    
    tail -n 20000 cytb_gene.trees > 20k_trees_use.tre
    awk 'NR>5000' 20k_trees_use.tre > 5k_random_trees.trees










Trick #3 - using several commands in one string to do something like the above, but only randomize the contents of the original file (so you can extract random trees afterward):



    
    for i in `cat cytb_gene.trees`; do echo "$RANDOM $i"; done | sort | sed -E 's/^[0-9]+ //' > cytb_randorder.trees







Have fun with this!  Let me know if it works for you.  Also, I'm sure that we can come up with a lot more ways to do this or improving on the above code, and I'd love to hear more...




~J
