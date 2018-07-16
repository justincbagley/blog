---
author: justin
comments: true
date: 2011-07-19 04:20:00+00:00
layout: post
link: http://www.justinbagley.org/130/one-way-to-evaluate-incomplete-lineage-sorting-in-your-phylogenetic-or-phylogeographic-data
slug: one-way-to-evaluate-incomplete-lineage-sorting-in-your-phylogenetic-or-phylogeographic-data
title: One way to evaluate incomplete lineage sorting in your phylogenetic or phylogeographic
  data
wordpress_id: 130
categories:
- blog posts
---

There aren't many ways to quantitatively evaluate incomplete lineage sorting (ILS) or ancestral polymorphism in molecular data in a statistically rigorous way.  One means of gauging relative amounts of lineage sorting is the gsi, which I will be working on later.  But, right here I wanted to note that I recently saw Ian Wang & Brad Shaffer using Wayne Maddison and Lacey Knowles method to evaluate ILS in a paper they wrote on dendrobatid frogs of Costa Rica, which is one of the main areas I am studying in my dissertation research.  Here is an excerpt from their paper:  
  
"Because incomplete lineage sorting has the potential to confound  
phylogenetic analyses of recently diverged populations, we  
also performed the “minimize deep coalescences method” following  
the procedure of Maddison and Knowles (2006). This method  
takes into account the process of lineage sorting by genetic drift  
and information on the genealogical relationships among alleles  
(Maddison and Knowles 2006) and has been shown to improve the  
probability of recovering an accurate population tree, even with a  
single locus (Knowles and Carstens 2007). We first performed a  
parsimony analysis in PAUP∗, using a heuristic search with 1000  
random addition sequence replicates and maxtrees = 100, and  
saved a majority-rule consensus tree from all equally parsimonious  
trees recovered in the search. We then used the tree search  
tool in Mesquite version 2.5 (Maddison and Maddison 2005) to  
find the population tree that minimized the total number of deep  
coalescences, using the saved majority-rule consensus tree and  
SPR branch swapping (Maddison and Knowles 2006)."  
  
Through this analysis, the authors were able to say that their phylogeny based on their mtDNA data was not different from a tree where ILS was minimized, suggesting the tree more likely reflected historical signal.   
  
This is a nifty little trick that I plan on using.  I am currently learning to implement gene tree modeling in MESQUITE, but I have a long way to go (feels like)....  my consolation is that I am already really familiar with the basics and with phylogenetic comparative analyses and trait evolution-related analyses in the program, so maybe my progress will be fast.   
  
Reference  
  
Ian J. Wang1,2 and H. Bradley Shaffer1 (2008) RAPID COLOR EVOLUTION IN AN APOSEMATIC SPECIES: A PHYLOGENETIC ANALYSIS OF COLOR VARIATION IN THE STRIKINGLY POLYMORPHIC STRAWBERRY POISON-DART FROG. _Evolution_, 62-11: 2742–2759.
