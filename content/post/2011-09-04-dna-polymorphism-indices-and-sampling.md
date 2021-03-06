---
author: Justin Bagley
comments: true
date: 2011-09-04 06:53:00+00:00
layout: post
link: http://justinbagley.rbind.io/2011/09/04/dna-polymorphism-indices-and-sampling/
slug: dna-polymorphism-indices-and-sampling
title: DNA polymorphism indices and sampling
categories:
- blog posts
tags:
- DNA polymorphism
- genetic divergence
- DNA sequence
---

Today, I wanted to jot down something simple that I just realized for the first time... which is that DNA polymorphism indices usually reported in phylogeography and population genetics studies of fishes and other organisms vary in their degree of sensitivity to sampling (i.e. sample size). A number of these indices exist and are commonly--actually increasingly--reported, particularly since programs such as `Arlequin` and `DnaSP` provide excellent software resources for manipulating and analyzing data along these lines. 

The main such indices include the average number of nucleotide differences between two random sequences (&Pi;; commonly assumes infinite-sites model); nucleotide diversity (&pi;), the number of nucleotide differences per site between two sequences randomly drawn from a population; the number of segregating sites (<i>S</i>, also known as <i>K</i>), or variable sites across a sample; and the number of alleles or different sequences (e.g. haplotypes, <i>h</i>) in a sample. Dependence of <i>K</i> on sequence length (<i>L</i>) can be accounted for by dividing <i>K</i> by <i>L</i>, yielding <i>k</i> (<i>K</i>/<i>L</i> = <i>k</i>).    
  
An important point in the calculation of these metrics seems to be that while <i>k</i> depends on sample size, &pi; does not. Also, the number of alleles (haplotypes) is dependent on <i>L</i> and sample size. This means that when sampling is not sufficient (>10?) at a site, or across sites, it may be best to report/base conclusions about diversity on &pi; instead of <i>K</i>,<i> k</i>, or the number of alleles (or <i>h</i>), because it is less sensitive to sampling error/size.    
  
But what does a given value of &pi; actually mean?  Assuming <i>L</i> = 1000, a value of &pi; = 0.005 means that we expect two randomly selected sequences 1000 bp in length to differ on average by 5 nucleotide positions. Populations with higher &pi; values are (assuming neutral expectations, assumptions) expected to have diverged longer ago in time than populations with lower &pi; values, thus accumulated more mutations. &pi; values are commonly low in natural populations (e.g. maybe <0.005) and sometimes are multiplied by 100 before being reported (we're doing that in one of my projects now).  
  
More later... 

~ J  
  
**References**
  
Li, W.-H. (1997) _Molecular Evolution_. Sinauer & Associates, Sunderland, MA.
