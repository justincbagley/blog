---
author: Justin Bagley
comments: true
date: 2011-08-05 18:50:00+00:00
layout: post
link: http://justinbagley.rbind.io/2011/08/05/evolution-phylogenetics-and-phylogenetic-model-selection-jmodeltest-vs-dt_modsel/
slug: evolution-phylogenetics-and-phylogenetic-model-selection-jmodeltest-vs-dt_modsel
title: 'Evolution, phylogenetics, and phylogenetic model selection: jmodeltest vs. DT_ModSel'
categories:
- blog posts
- model selection
- jmodeltest
- phylogeny
---

Evolution is the central unifying theme in all biology--"Nothing makes sense in biology except in the light of evolution," said Dobzhansky. Two of the most important contributions of Darwin to this field were (1) acceptance and priority of the reality and importance of individual variation (selection acts on individuals, evolutionary changes surface in populations...) and (2) the first phylogenetic tree with the accompanying hypothesis that all organisms share a common ancestry that can be visualized as a hierarchical branching design. Since Darwin drew the first phylogeny, phylogenetics has risen to a pivotal position in the study of organic evolution. From phylogenies, we can determine interrelationships among species and higher taxa, reconstructing patterns of macroevolution; we can study the rates and statistical properties of changes that occur in organisms during trait evolution; we can use phylogenies to model different evolutionary processes; and we can use phylogenies to understand the history of population genetic patterns and lineages, and to estimate population-level parameters and processes. Phylogenies also form a basis for taxonomic decisions and groupings, which form a basis for naming organisms and entities (e.g. viruses), thus a basis for the way we talk about living things, the way we use them, and the way we conserve them.  Not surprisingly, it has also been said, "Nothing in evolution makes sense, except in the light of phylogeny" (me.... and probably people you know, or other anonymous people).  
  
Thus, a central pursuit of evolutionary biologists is to reconstruct the phylogeny, or tree, of life. This has the consequence of phylogenetics and systematic biology assuming an important role in evolutionary studies. The evolution of this field itself, including an exploding methods base, increased statistical rigor of tools used (e.g. bioinformatics software), and rapid accumulation of DNA sequence data and genomes, has been discussed in detail many times and places. The growth of the field has also been accompanied by a tremendous effort of self-criticism, research and debate, which continues to improve the field.    
  
There are many steps in phylogenetic analysis. Common steps include:  
  
>1. Study design (spatial sampling design, target sample number (e.g. per site), target genes, desirable outcomes of sequencing...etc.)  
>2. Sample collection and curation  
>3. DNA extraction  
>4. DNA amplification  
>5. DNA sequencing  
>6. DNA editing  
>7. DNA sequence variation and miscellaneous data maneuvering / infile prep.  
>8. Model selection  
>9. Phylogeny reconstruction  
>10. Nodal support analyses  
>11. Final tree/data curation  
>12. Figure design and preparation for publication  
  
There also is a massive number of possible ways to conduct individual steps in this chain; e.g. take phylogenetic reconstruction analyses: many are methodologically and philosophically very different, they require different software and make different assumptions about the data and products of analysis.    
  
However, one important step that many biologists agree is a necessary step in phylogenetic analysis is phylogenetic model selection.  There are currently, in my opinion, two excellent and up-to-date programs for model selection here: `jmodeltest` and `DT_ModSel`.  `jmodeltest` was written by David Posada and stems from a line of "modeltest" programs forged by Posada and his PhD advisor Keith Crandall, as well as the related program MrModelTest by Jon Nylander. `DT_ModSel` is a perl script-based method that was developed in Jack Sullivan's laboratory. There are several reasons to use or avoid each of these programs. I am experimenting with both, and here is what I have found so far:  
  
`jmodeltest` is the only model selection program that implements all 88 current models. This includes 56 models found in `DT_ModSel` plus several other variants, some of which Posada came up with himself. `jmodeltest` is highly flexible, offering several information-theoretic (often, ultimately, likelihood-based) statistical methods for determining the appropriate model of DNA sequence evolution: Akaike's information criterion (AIC; also including the small sample size correction, AICc), Bayesian information criterion (BIC), and decision theory (DT; which I have not gotten to work yet). There are good reasons I think for preferring AIC out of these possible methods (described elsewhere), and most people in the field tend to use AIC here instead of the other choices. `jmodeltest` works on mac and windows machines and has a nice GUI for the user to load their data, compute likelihoods, and do further model selection analyses.  For example, it is possible to always produce a model-averaged estimate of the phylogeny of the sequences being analyzed, under each of the methods (AIC, etc.).  There are **_four_** down-sides to `jmodeltest`.    
  
- First, sometimes you have to restart your computer for it to accept files.  
- Second, it can be tricky to get it to take your files in the first place, especially when you are first starting to use the program.  To avoid the first issue, always restart your computer directly after updates, e.g. windows/HP updates.  To avoid the second issue, regretably, about the only thing I have found to do is to always transform your NEXUS file into a 'simplified NEXUS', which can be done using the 'File'>'Export' commands from the drop-down menu in `Mesquite`.  
- Another down-side of jmodeltest is that unfortunately the program can take several hours to run a single analysis, depending which settings you use.  When you begin computations, you can choose for likelihoods to be generated from ML-optimized analysis, BIONJ analysis or using fixed tree topologies (probably not recommended? not sure...). The former option is the slowest in my experience.  It is also the most thorough, and it should be used when possible.  
- Last, but not least, the fourth issue with `jmodeltest` is that you can only open one `jmodeltest` GUI/application at a time!!  It is impossible, as far as I can tell, to run multiple data sets in simul on one machine.  

On the bright side, no scripting is necessary.  _But good luck!_  
  
My newest interest has been learning to use `DT_ModSel`. `DT_ModSel`, like jmodeltest, can be used on UNIX, Windows and Macintosh machines. The major differences between this program and jmodeltest is that it is based explicitly on a decision theory algorithm and it is run from a Perl script, so downloading Perl on your Mac OS9 (classic) and UNIX/Windows platform will be necessary (however, you are ready to go if you're running Mac OSX, e.g. on an intel macbook pro). Minin et al. (2003; manuscript available in PDF format from the authors; get it by clicking here) explain in detail the advantages of using this method over something like jmodeltest.  To summarize two main points, DT_ModSel is advantageous because it often selects slightly more simple models than other methods (jmodeltest) and this will have a consequence for phylogenetic inference i.e. minimizing branch lengths, faster runs, etc. Practically, there are some major differences here as well.  First, because it is run using a couple of text files, there is no GUI. There is nothing "nice" to look at.  Instead, this method requires (for UNIX/Windows machines, like my Sony Vaio) placing a set of `PAUP*` commands (model commands) below your data matrix within your NEXUS file, running the data matrix in PAUP* (required) to get the scores and likelihood trees (two output files generated by each run), and then a final step or set of steps to get your "answer" of which is the best model based on your analysis by using a simple command(s) in Perl.  Here, the advantage seems to be that PAUP* does a thorough ML analysis (but is it more thorough than the phyml-based analyses in jmodeltest?) that is faster in my experience. The disadvantages are real, though. First, you have to do more data management i.e. you have to keep track of all the files produced, which for several data sets can add up quickly; meanwhile, in jmodeltest, you simply run your data matrix through the GUI and copy and paste the log to a text file or whatever, and you're done.  Second, and more taxing, if you don't know Perl you are out of luck finalizing your analysis, conducting the final step of the instructions.  This is a big problem at first; at least, it was for me because I didn't know how to use Perl. But once you figure out this issue, the analysis is a breeze although somewhat more complex than using jmodeltest. And this down-side, for me, was balanced out by the cheerful result that, assuming you can open multiple PaupUp or `PAUP* applications on your machine at once, multiple data files can be run through the first script (at least) simultaneously!  
  
In the end, these methods are not comparable and we should choose which one to use based on the available evidence.  I have now used jmodeltest for several projects; however, currently I am reading more about DT_ModSel and playing with the program more to determine whether or not it is a better program to use.  If you have a leaning on this one, please chime in.  
One thing I _can say_ in closing is that these guys put a lot of effort into producing these methods, and I am grateful to all of them for this and for their help using these programs.  To David Posada, thank you so much for an excellent program and nice documentation that basically made life easier for me.  I have learned some tricks to use your program, but it is straightforward.  To Jack Sullivan and Zaid Abdo, thanks for an awesome script set.  Thanks.  
  
~ J
