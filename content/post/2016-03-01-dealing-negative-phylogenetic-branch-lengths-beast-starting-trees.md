---
author: justin
comments: true
date: 2016-03-01 21:43:35+00:00
layout: post
link: http://www.justinbagley.org/2099/dealing-negative-phylogenetic-branch-lengths-beast-starting-trees
slug: dealing-negative-phylogenetic-branch-lengths-beast-starting-trees
title: Dealing with negative phylogenetic branch lengths in BEAST starting trees
wordpress_id: 2099
categories:
- BEAST
- blog posts
- R
tags:
- ape
- BEAST
- branch lengths
- command line
- grep
- phylogeny
- R
---

##### Negative branch lengths and the BEAST




[![beast](http://www.justinbagley.org/wp-content/uploads/2016/02/beast.png)](http://www.justinbagley.org/wp-content/uploads/2016/02/beast.png)When conducting phylogenetic analyses, you will from time to time encounter negative branch lengths. Negative branch lengths are a nuisance because they can cause substantial visualization problems or keep analyses (e.g. downstream analyses in other programs) from running.




For example, it will be desirable in many cases to add a starting tree to input files for datasets with phylogeographical sampling (e.g. multiple individuals in a standard BEAST analysis, or a *BEAST species tree analysis with multiple individuals sampled per species/population modeled). However, intraspecific sampling has the downside that it lends itself to negative phylogenetic branch lengths in maximum clade credibility (MCC) trees (final annotated tree resulting from BEAST analysis). This can happen when a clade in the MCC tree [occurs at low frequency](http://beast.bio.ed.ac.uk/faq#Why_does_my_tree_produced_by_TreeAnnotator_have_negative_branch_lengths.3F) relative to many other trees that are being summarized. But watch out!! TreeAnnotator _will not_ _alert you_ that negative branches are present in the MCC tree output. You are unlikely to catch this issue unless you visualize your MCC tree in FigTree, which in more conspicuous cases will show some really funky looking branches running the opposite direction!




This is problematic because when you take a tree that unbeknownst to you has negative branch lengths and try to use it as a starting tree, BEAST will hang up and return the following error message:




[code language="bash"]java.lang.RuntimeException: Negative branch length: -0.0036835877071336926 at beast.evolution.likelihood.BeagleTreeLikelihood.traverse(Unknown Source).[/code]




##### Solutions




You can deal with this problem by manipulating the branch lengths of your tree so that small/negative branch lengths are converted to zero in one of several ways:





	
  1. manually, e.g. in a text editor,

	
  2. using regular expressions i.e. grep (=super search and replace!)

	
  3. manipulating tree edge lengths in R without relying on a specific function but taking advantage of phylo structure,

	
  4. using the R collapse multichotomy function in APE.




In one of his Boopsboops [blog posts](http://boopsboops.blogspot.com.br/2010/10/negative-branch-lengths-in-neighbour.html), Rupert Collins provides an example of this from a COI neighbor-joining phylogeny of cypriniform fishes, and he also gives two examples of how to change the negative branch lengths to zero branch lengths using regular expressions and R code to change tree edge lengths (branch lengths) less than zero to zero. So, you can simply check out his blog post for info on #2 and #3 in the list above. However, when modifying edge lengths in R, it's worth considering non-negative values less than zero; I mean, a branch length of 0.01 still extends back to 10 thousand years prior, and you may not want to convert it to zero. Searching around online, I also found the following solution using sed posted by [Andreas](https://www.biostars.org/u/245/) on [biostars.org](https://www.biostars.org/p/45597/):




[code language="bash"]sed -e 's,:-[0-9\.]\+,:0.0,g' in.tree &amp;gt; out.tree[/code]  

  

So, that's another way to use the command line to solve the negative branch length problem! In the sed example, "in.tree" is the input tree name and "out.tree" is an output tree name; both can obviously be changed to fit your preferences.




For #4 in the list above (in R), you would use




[code language="r"]di2multi(phy, tol = 1e-08)[/code]




which according to APE documentation "deletes all branches smaller than `tol` and collapses the corresponding dichotomies into a multichotomy." This will take internal zero- or negative-length branches and collapse them. Here, phy is a class "phylo" object containing your tree.




As a slight side note, the APE function multi2di, which is a [companion function](http://finzi.psych.upenn.edu/library/ape/html/multi2di.html) to di2multi, can be used to accomplish the opposite task--arbitrarily resolving multichotomies into series of dichotomous branches. The general usage of multi2di is as follows:




[code language="r"]multi2di(phy, random = TRUE)[/code]




If random is set to FALSE, then polytomies will be resolved in their order of appearance in the tree.




##### Known issues




'Purists' will likely notice that there are some issues with the above suggestions. In particular, when you collapse branches or convert small/negative branch lengths to zero-length branches, this has the effect of shortening the tip-to-node distance for the adjacent branch. The difference doesn't get added back in. So, if you are working with an ultrametric time tree (e.g. output from a previous BEAST analysis), the above manipulations will yield a final tree that is technically, and by an ever so slight margin, non-ultrametric. If the tree of interest wasn't ultrametric to begin with (e.g. it was from RAxML), then the resulting tree simply will not preserve the overall branch lengths.




_The good news _is that, after you fix negative branch lengths in your BEAST starting tree, and assuming that you 1) have your starting tree properly specified in your xml input file and 2) the tree fits any calibration priors, your BEAST analysis should start without being impeded by these kinds of errors. Of course, the manipulations I've discussed above will also fix graphical errors caused by negative branch lengths. OK, I hope the above helps you get your BEAST analyses running full speed ahead when you encounter negative branch length issues.




~J
