---
author: justin
comments: true
date: 2018-03-10 23:17:05+00:00
layout: post
link: http://www.justinbagley.org/3482/ddocent-install-successes-failures-on-linux-supercomputers
slug: ddocent-install-successes-failures-on-linux-supercomputers
title: dDocent install successes & failures on Linux supercomputers
wordpress_id: 3482
categories:
- bash
- blog posts
- dDocent
- ddRAD-seq
- Linux
- Samtools
- SNPs
tags:
- bioconda
- condarc
- configuration
- dDocent
- file
- install
- Linux
- memory
- rainbow
- samtools
- Supercomputer
---

[![](http://www.justinbagley.org/wp-content/uploads/2018/03/Screen-Shot-2018-03-10-at-3.00.13-PM.png)](http://dDocent.com/)

Jon Puritz and some other developers have hacked out a nice pipeline, named [dDocent](http://ddocent.com) (pronounced "docent"), for genomic assembly, read mapping, and SNP calling using NGS data from the RAD-seq family of sequencing strategies. dDocent is nice because it pulls together several top-of-the-line existing tools, and because it provides reference-based and _de novo_ assembly options.

Instructions for installing dDocent are given at the pipeline's Bioconda Download and Install page, and are claimed to be "So easy your grandfather could do this...." I've recently made attempts at installing dDocent on two different Linux-based high performance computing clusters, or "supercomputers," one at VCU's CHiPC facility, and one at BYU's FSL facility. Below, I discuss some successes and problems I've run into with installing this software, and the limited but generally successful set of solutions that I have found.




## **Perfect install on Centos Linux**



[![](http://www.justinbagley.org/wp-content/uploads/2018/03/conda-300x81.png)](http://www.justinbagley.org/wp-content/uploads/2018/03/conda.png)First, I'm **very happy** to say that, after correctly installing [Miniconda](https://conda.io/miniconda.html) (for Python 2.7 in my case) and setting up my ".condarc" conda configuration file to search the Bioconda channel first, a regular install of dDocent and all depdencies worked flawlessly "out-of-the-box" on the VCU supercomputer! 

Please click [on this link](http://www.justinbagley.org/wp-content/uploads/2018/03/Bagley_dDocent_godel_install_Terminal_log.txt) to obtain a copy of my Terminal log from the install, which I have sanitized. The full procedure involved 1) checking for, then installing Miniconda (=Python); 2) updating Miniconda; and 3) installing dDocent, and it worked like a charm when I tested the resulting executable. The only _trick_ here was that **I had to start my interactive session by using the "qrsh" [command](http://arc.leeds.ac.uk/using-the-systems/why-have-a-scheduler/qsub-qrsh-usage/) to log into a compute node with an updated Centos 6/7 environment** in order for this install procedure to work. I also had to allow sufficient time for the dDocent part of the conda install, which can take a couple of minutes and make your Terminal screen look "frozen"; but, whatever you do, don't stop it before it finishes--take a coffee break and let it do its work.



## **Errors during Red Hat Linux install**



Despite the many positives, users may have trouble installing dDocent on Linux (where it is really made to be installed) or UNIX/Mac systems (generally not recommended). At such times, remember that issues on the developer's side are uncommon with major-version, widely used software programs that are usually updated within the last two to three months. More commonly, these problems can arise due to errors on the user side of things. On Linux and Mac there could be some common problems, but on Mac I'm almost certain that the roadblock will be installing [rainbow](https://sourceforge.net/projects/bio-rainbow/files/?source=navbar), which is currently distributed as source, but in a v2.0.4 that despite being supposedly updated for Mac, appears only to install correctly on Linux based on my experience. The latest rainbow executable is pretty old by software standards, updated three years ago in August  of 2015, so I wouldn't place high hopes for a Mac friendly update any time soon.

On FSL's SLURM-based system, which is a Red Hat Linux system on which I have installed lots of software over the years, I ran into errors similar to those discussed in this dDocent [user's group thread](https://groups.google.com/forum/#!topic/ddocent/aRFiClKTsqk). The install appeared to finish just fine, but then upon executing dDocent, I received a samtools-related error message stating that my version of [Samtools](http://www.htslib.org) was "optimized" (i.e. sufficiently updated), as follows:

[code language="bash"]
-bash-4.1$ dDocent
dDocent 2.2.25 

Contact jpuritz@gmail.com with any problems 

Checking for required software
/path/to/envs/ddocent_env/bin/dDocent: line 46: [: : integer expression expected
The version of Samtools installed in your $PATH is not optimized for dDocent.
Please install at least version 1.3.0
[/code]

For more on Samtools, read [here](http://biobits.org/samtools_primer.html). **I had this issue in my regular environment (above) and the virtual environment I set up for dDocent during the install.** The abbreviated solution given in the user group thread I linked to above is that you simply need to fix your conda configuration, uninstall bzip2 and dDocent, and then reinstall dDocent. However, there are two problems with this: 
**




**
  1. my Samtools version is wayyyy more recent than 1.3.0** (think 1.7+, in my regular environment and my dDocent virtual environment),
**
  2. the proposed uninstall-reinstall procedure for the dDocent virtual environment did not work for me, and may not work for other users either!**


**



<blockquote>So what did I do? What solves the problem here? 
> 
> </blockquote>





**First, update your Miniconda configuration file, which is called ".condarc".** The conda configuration file .condarc should have channels defined in the proper order. Below is an example, which I got by looking into my own .condarc file on my FSL account:

[code language="bash"]-bash-4.1$ cat ~/.condarc
channels:
  - bioconda
  - conda-forge
  - defaults
  - r
[/code]

**Second, forget the dDocent virtualenv idea.** Deactivate your dDocent environment, suggested in the [install instructions](http://ddocent.com/manual/), and install dDocent in your regular environment. For this, you need to _first_ deactivate the virtual environment by doing: 

[code language="bash"](ddocent_env) -bash-4.1$ source deactivate"[/code]

**Third, once dDocent is installed in your regular environment (install/reinstall if necessary), update your version of Samtools.** I already had dDocent installed in my regular environment, and the code for that is just "conda install ddocent". But, for example, I got the following to screen out when using the update command in Miniconda to update Samtools:

[code language="bash"]
-bash-4.1$ conda update samtools
Solving environment: done

## Package Plan ##

  environment location: /path/to/miniconda2

  added / updated specs: 
    - samtools


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    conda-4.3.34               |           py27_0         507 KB  conda-forge
    certifi-2018.1.18          |           py27_0         143 KB  conda-forge
    ------------------------------------------------------------
                                           Total:         650 KB

The following packages will be UPDATED:

    ca-certificates: 2017.08.26-h1d4fec5_0 --> 2018.1.18-0      conda-forge
    certifi:         2018.1.18-py27_0      --> 2018.1.18-py27_0 conda-forge
    openssl:         1.0.2n-hb7f436b_0     --> 1.0.2n-0         conda-forge

The following packages will be DOWNGRADED:

    conda:           4.4.11-py27_0         --> 4.3.34-py27_0    conda-forge

Proceed ([y]/n)? y

Downloading and Extracting Packages
conda 4.3.34: ##################################################################################################################################################### | 100% 
certifi 2018.1.18: ################################################################################################################################################ | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
[/code]

After following these steps, if you type "dDocent" into the command line and press return, the program should try to run. If you do this like I did while within your home directory or compute directory, where there are no gzipped fastq input files, and you type something other than "yes" or "no" at the first prompt (e.g. "xyz"), then dDocent will run properly but find 0 sequences and finish with an "Incorrect input" error, as follows:

[code language="bash"]
-bash-4.1$ dDocent
dDocent 2.2.25 

Contact jpuritz@gmail.com with any problems 

Checking for required software

All required software is installed!
ls: cannot access *.F.fq.gz: No such file or directory
ls: cannot access *.F.fq.gz: No such file or directory

dDocent run started Wed Mar 7 15:24:32 MST 2018 

0 individuals are detected. Is this correct? Enter yes or no and press [ENTER] 
xyz
Incorrect Input
[/code]

This is what I got, and it confirmed to me that the dDocent install was working properly, and that all dependencies were available to the program. I can say this about dependencies, because the program always checks this. Unfortunately, you could still have problems with dependencies that I have not accounted for here, for example if you have trouble installing rainbow. But I didn't run into any such issues, so don't worry about those until you see them.

~J


