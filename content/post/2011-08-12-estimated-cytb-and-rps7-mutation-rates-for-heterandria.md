---
author: justin
comments: true
date: 2011-08-12 15:01:00+00:00
layout: post
link: http://www.justinbagley.org/125/estimated-cytb-and-rps7-mutation-rates-for-heterandria
slug: estimated-cytb-and-rps7-mutation-rates-for-heterandria
title: Estimated cytb and RPS7 mutation rates for Heterandria
wordpress_id: 125
categories:
- blog posts
---

Today, I looked at results of some runs I have been doing in BEAST to estimate divergence times and other parameters for my project on Least Killifish, _Heterandria formosa_ (Poeciliidae).  These analyses were multi-locus, based on cyt_b _and _RPS7_ sequence data (based on a small number of subsamples of our phylogeographic sampling).  Essentially, no one knows the S7 mutation rate for freshwater fishes.  In other words, it is poorly understood.  However, by unlinking the rates of these two loci I was able to arrive at some estimates of the mutation rate of unexpressed portions of this nuclear gene based on variation in S7 intron 1 and intron 2.  In this analysis, I used a strict clock (a relaxed clock is inappropriate for genealogical data like the data we have) and a broad uniform 'fish clock' rate prior (0.08-0.028% Myr-1) for cyt_b_; I partitioned by gene and used a codon model for cyt_b _(1+2, 3) and I ran the MCMC for 10^8 generations, linking the tree models but not the clock models.  Based on my experience reading the literature, nDNA rates in vertebrates are usually between  0.0005% and 0.005% Myr-1, so this was the prior for S7 in the  analysis (like the cyt_b _prior, this is very broad, thus more conservative and honest than a thinner interval).  BEAST estimated the mean cyt_b _rate to be somewhat high at 0.0198% Myr-1, and the mean S7 rate was 0.00282% Myr-1 (95% CIs were broad though).  I think we will report these values in our _Heterandria _manuscript (in prep.), but I'm going ahead and throwing the preliminary results up here in case someone is interested in S7 mutation rates.    
  
~ J
