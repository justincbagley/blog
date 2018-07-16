---
author: justin
comments: true
date: 2015-09-01 02:41:34+00:00
layout: post
link: http://www.justinbagley.org/1032/funny-thing-ima2-output
slug: funny-thing-ima2-output
title: A funny thing about IMa2 output (a lost 2011 blog post)
wordpress_id: 1032
categories:
- blog posts
- IMa2
- Phylogeography
tags:
- Bayesian
- IM
- IMa2
- Jody Hey
- output
- parameters
- PhD student
- posterior distribution
---

Recently, I discovered something that I wrote about four years ago during the first part of my PhD, just 2 years or so after IMa2 had come out [around a year or so after Hey (2010)]. Back then, I was a little unhappy about the way parameters were coded, but now looking back, it's actually kind of funny, so I decided to post this as a blog entry. I mean, I've published with this method and have a much better understanding of it now. But this old scrap conveys how difficult and frustrating it can be to learn new software programs, as well as the propensity for early PhD students to freak out when having to learn the bewildering array of software one should master when preparing to become a professional in ecology, evolution, and systematics. It also does point out how difficult it can be to track the parameters in models, or adapt to changes in the input file format for different software.

<blockquote>July, 2011
> 
> So you go to the trouble to run the isolation-with-migration model in IMa2 (Hey & Nielsen, 2004, 2007; Hey, 2010; e.g. specifying correct im input files and correct priors, including correct per-gene mutation rate calculations), then you succeeded in getting the program to run with your data and your runs have finished?  Congratulations!  Now, you are looking at the output.  It is a pretty plain looking ASCII file called "somename.out" and it contains text output of histograms with numbers that are as good as gold to you if you can interpret them.
> 
> The funny thing is... neither the manual for IM nor IMa2, nor any of the publications for this algorithm, clearly explains what the parameters mean.  Jody Hey's publications and manuals are simply awesome!  And I mean that.  I _really_ like this program and have read all of the papers associated with it.  So my critique here is very very minimal, but rests on an important little deficit: different parameter names are used in different publications and manuals for the IM family of software!  And different programs give different output.  The problem is, it's never spelled out which population sizes and hence mutation rates correspond to which population pairs.  Never, not even in the simple, two-population case.
> 
> So, you look at the ".out" file you get back from your run, which took days to weeks depending on whether you have access to a supercomputing facility like the one we have at BYU. You look down at "HISTOGRAM GROUP 2: MARGINAL DISTRIBUTION VALUES AND HISTOGRAMS OF POPULATION SIZE AND MIGRATION PARAMETERS" section of the output, which contains results for the posterior distributions of population size and migration parameters from your run.  Now, you see the parameter names as you expected... q0, q1, q2, m0>1, m1>0.  But your interpretation of all of these depends on "what" q0, q1, and q2 mean.  You realize you need this information, so you go to Hey & Nielsen (2004; the updated IM reference over the 2001 Hey and Nielsen paper that doesn't describe the current software algorithms), and you find populations are listed in the nice Fig. 1 with the IM speciation/vicariance model as "N1", "N2", and "NA", moving from the two daughter populations (tips) of the tree pointing to the top of the page down to the ancestral lineage.  
> 
> Then you go to the more up-to-date Hey (2010) paper extending IM models to multiple ancestral and extant populations.  The seeming comprehensiveness, power, and flexibility of the model comes at the cost of having to specify the population tree a priori, but you love this paper.  Yet, to your dismay, parameter names have changed and are now "theta1", "theta2", and so forth down to the ancestral lineage, which is now renamed "theta5".  That's funny, because the program says these are q0, q1, and q2 in the output.  But where does this notation start, at the tips of the tree or the ancestor, and at the left tip of the tree (your first population in your im file), and then go over to the second one (your second population top-to-bottom in your im file)???  WTH?
> 
> So, this is a little bit annoying.  But, then again, this is a minor issue.  You just need to trust your logic to sort this out.
> 
> Fortunately, you notice that the diagrams in the software manual and all of the IM-family publications always start numbering the lineages/populations with the lowest number at the upper left daughter population (tip) of the topology and that the numbers increase as you move down and to the right through the population trees.  Logically, you now expect that the upper left tip is q0, the upper right tip is q1, and the ancestral population size is q2.  But this still drives you crazy because searching for "q0" in the 2007 "Introduction to IM and IMa 3 5 2007.pdf" manual you have gives the error message reading "Reader has finished searching the document.  No matches were found."  You then go over to the newer "Using IMa2 8 24 2011.pdf" version of the manual for IMa2 and do the same search, only to get a similar message and no "q0" to be found.  You frantically search through all of the IM and IMa2 publications again thinking surely this must be in there because you will use the wrong parameter estimates or ignore the wrong (not because of the program, because of the notation) and probably meaningless ancestral population size estimate if you can't figure this out because you don't know where the author of the software program started numbering when he wrote the manual!
> 
> You take a deep breath, then remember your inference from the IM-family papers.  You set the following rules: that you should let q0 = q1 or N1 or theta1; let q1=q2 or N2 or theta2; and that the remaining parameter q2=qA or NA or thetaA.  Then you reason that, therefore, m0>1 is m1 and m1>0 is m2, and you go on with your life.
> 
> That's the funny thing about IMa2 output.
> 
> ~J
> 
> </blockquote>

While completing the IMa2 analyses I was doing at the time I wrote this, I realized I was correct about the parameter names. At first, I inferred this from the manuscripts and the results: IMa2 often struggles the most to estimate ancestral population size parameters (not the daughter population thetas) and migration parameters, so it made sense for the q2 value to be the ancestral theta because it's posterior distribution was being estimated as a very diffuse distribution when I was using just mtDNA. That left q0 and q1 to be the two daughter populations, and it made the most sense for the population with the lower subscript/number to be the first population in the data file, which indeed is the case.

However, later I found that, to my chagrin _and making it even funnier now_, I had forgotten that in IMa2 I was adding a little line of code to the input file. This little line of code was relatively new and had not been required in the original IM input file format, and it specified the population tree in newick format. I had also forgotten that the IMa2 manuals from 2009 and 2011 had shown examples of how to input the population tree in the input file, and that while their descriptions had involved more complex scenarios with four daughter populations and multiple ancestral populations they also showed that ancestral populations were always preceded by a colon in the notation. As per the example tree on p. 30 of the 2011 manual, given as "(0,1) :2," this would always be the newick tree for a model with two daughter populations. This gave the indirect evidence for matching the corresponding population size parameter names, which would of course be q0, q1 and q2. So, all along, the evidence I needed to figure out the parameter names and feel 100% confident about them was _in the manuals to begin with._

I highly recommend that you use IMa2. Just make sure you 1) read the papers and manuals very carefully and 2) correctly specify your population tree and interpret the parameter names! Also, if you write a manual for a software program, I highly recommend that you provide a graphic containing the actual parameter names you require in the input file, not a different set of names, so that it is easy to see the connection between the model and the syntax for arguments fed to the program.

~J

**_References_**

Hey, J. 2010. Isolation with migration models for more than two populations. Mol. Biol. Evol. 27: 905-920.

Hey, J. & Nielsen, R. 2004. Multilocus methods for estimating population sizes, migration rates and divergence time, with applications to the divergence of Drosophila pseudoobscura and D. persimilis. Genetics 167: 747-760.

Hey, J. & Nielsen, R. 2007. Integration within the Felsenstein equation for improved Markov chain Monte Carlo methods in population genetics. Proc. Natl Acad. Sci. USA 104: 2785-2790.
