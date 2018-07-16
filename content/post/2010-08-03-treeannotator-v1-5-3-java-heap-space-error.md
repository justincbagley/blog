---
author: justin
comments: true
date: 2010-08-03 15:13:00+00:00
layout: post
link: http://www.justinbagley.org/143/treeannotator-v1-5-3-java-heap-space-error
slug: treeannotator-v1-5-3-java-heap-space-error
title: TreeAnnotator v1.5.3 java heap space error
wordpress_id: 143
categories:
- bash
- BEAST
- blog posts
- command line
- Java
- Linux
- Mac
- Programming
- Software
- TreeAnnotator
- Windows
tags:
- bash script
- java
- Linux
- memory
- TreeAnnotator
- windows
---

##### Solving TreeAnnotator Memory Issues




So, apparently if you have 100,000 trees or more from your BEAST run (e.g., if you sampled every 1,000 trees and ran for an MCMC of 200 x 10^6 generations), then you will likely run out of memory if you try and annotate all the trees generated using TreeAnnotator v1.5.3 (current at time of writing; may also apply to earlier or later versions). To solve this problem, do one of two things... 1) (best) use LogCombiner to reduce your number of trees down to a smaller number... Rambaut and Drummond have stated that more than 10,000 trees is probably more than enough (open your big ass trees file in LogCombiner, then say you're going to reduce sampling frequency to 1000 and tell the program a file name in order to send the new trees to a new tree file); 2) increase the memory available to TreeAnnotator... a. by running a high memory version on a cluster or b. by increasing the memory to the program manually.







I used the following codes from Rambaut ([reference1](http://groups.google.com/group/beast-users/browse_thread/thread/f622d47b84878b10/af6de616c68fc5a7), [reference2](http://markmail.org/message/civhrqnevnrqxu26), [reference3](http://beast.bio.ed.ac.uk/Increasing_Memory_Usage)) or from my friend Matthew Bendall to do this recently from the command line (cmd):










**A. on my old Windows laptop...**












[code language="bash"]cd C:\Users\Public\Documents\Evolutionary Applications\BEAST 1.5.3\BEAST v1.5.3
java -Xmx1024M -cp lib/beast.jar dr.app.tools.TreeAnnotator ## Gives 1GB[/code]












OR











[code language="bash"]java -Xmx6144M -cp lib/beast.jar dr.app.tools.TreeAnnotator ## Gives 6GB[/code]











**B. From the BYU cluster/supercomputer...**




Using a shell script:










[code language="bash"]#!/bin/bash
#------------------------------------------------------------------------------#
#---BEAST shell script template
#---by matthew.bendall
#---For questions, please email matthew.bendall@gmail.com
#------------------------------------------------------------------------------#

#PBS -l nodes=1:ppn=1,walltime=24:00:00
#PBS -N long4new
#PBS -m abe
#PBS -M justin.bagley@byu.edu
#PBS -k oe

cd $PBS_O_WORKDIR

treeannotator_himem -burnin 10000 long4_long4newLogcombiner.trees long4_long4new_treeannotator_OUT

exit 0[/code]







