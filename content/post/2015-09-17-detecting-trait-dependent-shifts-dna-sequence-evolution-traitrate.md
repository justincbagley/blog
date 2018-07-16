---
author: justin
comments: true
date: 2015-09-17 15:06:20+00:00
layout: post
link: http://www.justinbagley.org/1361/detecting-trait-dependent-shifts-dna-sequence-evolution-traitrate
slug: detecting-trait-dependent-shifts-dna-sequence-evolution-traitrate
title: Detecting trait-dependent shifts in DNA sequence evolution with traitRate
wordpress_id: 1361
categories:
- blog posts
- Molecular evolution
tags:
- comparative methods
- DNA sequences
- macroevolution
- maximum likelihood
- molecular evolution
- rate shifts
- software
- traitRate
---

These days, we evo-biologists studying macroevolution tend to be interested in riding different waves of research and methods, and one of these is focused on understanding shifts in diversification rates as inferred from phylogenies and trait data. This is a hot topic in my opinion, and the focus is on understanding the causes and rates of spectacular adaptive and non-adaptive radiations of species in different systems across the glob. But did you know it was possible to test for trait-dependent shifts in evolution of species DNA sequences or genomes?

A method published a few years ago, but that I had never heard of until now, provides a means to do this, as described in the paper by Mayrose and Otto (2011). Mayrose and Otto's method is implemented in a program called traitRate. For more information, and to download the traitRate software program, follow this [link](http://www.tau.ac.il/~itaymay/cp/traitRate/index.html) to the traitRate website. Also, here is [link](http://www.hindawi.com/journals/ijeb/2011/908735/abs/) to a paper by Wong (2011) discussing the outlook for using traitRate and similar methods to understand the molecular evolution of animal reproductive tract proteins.

The basic idea is that, if you input an ultrametric phylogeny and character data into traitRate, you can test whether variation at a given discrete (e.g. binary) trait influences the rate of sequence evolution in a set of taxa using maximum-likelihood modeling and comparisons of nested models through likelihood ratio tests (LRTs). traitRate facilitates comparing two models--one model evaluating the relative rate of sequence evolution for one or the other binary traits while assuming an association between traits and rates, and a null model assuming no association between the trait value and rate of sequence evolution. The LRTs test the significance of the relationship by comparing the goodness-of-fit of the models.

It seems it might be possible to evaluate trait-dependent shifts in sequence evolution as well as multiplication of species within the same research program. For example, you could combine these two perspectives in order to address whether the evolution of a given trait has altered rates of molecular evolution and speciation, or just one or the other, in a given clade. Some evolutionary biologists that study speciation and molecular evolution are probably already doing this, but I haven't read papers that used traitRate, or that combined diversification and molecular evolution studies. Good idea or bad idea? Given molecular evolution is not really my field, I would be interested in hearing from people who are doing this type of thing, working on this topic. Also, since traitRate has not been used in many publications (the Wong paper has more citations than the original Mayrose and Otto paper!!), is there another method that is better, and thus more widely implemented, OR are these studies just rare? 

~J

**References**

Mayrose I and Otto SP. 2011. A Likelihood Method for Detecting Trait-Dependent Shifts in the Rate of Molecular Evolution. Mol Biol Evol. 28:781-791. 

Wong, A. 2011. TheMolecular Evolution of Animal Reproductive Tract Proteins: What HaveWe Learned fromMating-System Comparisons? Intl. J. Evol. Biol. 2011 Article ID 908735: 1-9.
