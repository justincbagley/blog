---
author: justin
comments: true
date: 2018-03-26 03:11:07+00:00
layout: post
link: http://www.justinbagley.org/4445/installing-r-for-user-on-a-centos-linux-supercomputer-account
slug: installing-r-for-user-on-a-centos-linux-supercomputer-account
title: R install for user on a CentOS Linux supercomputer
wordpress_id: 4445
categories:
- blog posts
- command line
- compiling software
- Linux
- R
- supercomputers
tags:
- APT
- bioconda
- command line
- conda
- error
- install
- libiconv
- library
- Linux
- R
- solution
- Supercomputer
- tar
- user
- wget
---

![R language for statistical computing](http://www.justinbagley.org/wp-content/uploads/2017/06/R-logo-image.png)An up-to-date R install is a key component of any biologist's bioinformatics toolkit. In this post, I will walk through some code that I used to solve the problem of installing the latest version of R, [R v3.4.4](https://cran.r-project.org) (the "2018-03-15, Someone to Lean On" release), at the user level on a Linux supercomputing cluster running [CentOS 5/6/7](https://www.centos.org). First, I'll give some background information that will be useful for following along. Then, I'll go into the basics of conducting a Linux R install when you do not have admin privileges. Thirdly, I'll point out a library/environment problem that I ran into with this method, and I'll show a low-stress solution for solving that problem. And, finally, I'll close with the successful install setup steps and illustrate that the newly installed version of R v3.4.4 worked and was available from my command line.





##### 1. Background: pre-install environment



On our cluster, I first used [`qrsh`](http://gridscheduler.sourceforge.net/howto/basic_usage.html) to log into a node and run or check the available R install, which gave me the following information:

[code language="bash"]
$ which R
/usr/global/R-3.3.2/bin/R
$
$ R

R version 3.3.2 (2016-10-31) -- "Sincere Pumpkin Patch"
Copyright (C) 2016 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

> q()
Save workspace image? [y/n/c]: n
[/code]

This told me that the system administrator currently had R v3.3.2 installed, and that it was made available to all users at /usr/global/R-3.3.2/bin/R. This version is from one or two years back, so I wanted to install my own updated version of R in my [home directory](http://www.linfo.org/home_directory.html) (you can get the path to your home dir by doing `echo $HOME`). 



##### 2. First steps: local R install within my user "$HOME"



To install R within my home directory, I started by following the standard install procedure for Linux, which involves downloading the source code as a tarball, unzipping that tarball, configuring the install, and performing the install. Note that you may see other biologists/scientists discussing tools such as `sudo`, `yum`, and `apt-get` for installing software on Linux. **It is important to _note_ that _none of these apply to the current case_**. The "super user do" command [`sudo`](https://linuxacademy.com/blog/linux/linux-commands-for-beginners-sudo/) is only used when you have admin privileges, and I am working as a user on an HPC cluster _without_ such privileges (not in sudoers list). Therefore, and in addition, since `yum` often requires `sudo`, it is also off limits. Want to use `apt-get`? Nope. Think again. The `apt-get` command calls [APT (Advanced Package Tool)](https://wiki.debian.org/Apt), which is a package tool manager that is only available on [Debian Linux](https://www.debian.org), and I am working on a cluster that runs CentOS. **So, the appropriate CentOS approach, without admin privileges, is to use [`wget`](https://www.gnu.org/software/wget/) as follows:**

[code language="bash"]
$ cd $HOME
$ wget http://cran.rstudio.com/src/base/R-3/R-3.4.4.tar.gz
$ tar xvf R-3.4.4.tar.gz
$ cd R-3.4.4
$ ./configure --prefix=$HOME/R
$ make && make install
[/code]



##### 3. The problem: libiconv configure error



Unfortunately, while running the standard install procedure above, I hit a snag in the form of the following configure error:

[code language="bash"]checking whether iconv accepts "UTF-8", "latin1", "ASCII" and "UCS-*"... no
     configure: error: a suitable iconv is essential
[/code]



##### 4. The solution: point to lib directory with libiconv library/module files



I reasoned that the underlying issue causing this problem was that the libiconv library/module files were simply not being found. I suspected this library was installed within Miniconda, but was not sure, so I first checked for its presence and location. It's always safe and pretty fast to do this using Bioconda [`install`](https://bioconda.github.io), which told me that libiconv was indeed already _installed_, and where it was located. So, I next looked to make sure libiconv files were in the Miniconda lib dir, and they were:

[code language="bash"]
$ ## Check/update libiconv:
$ conda install libiconv
Fetching package metadata .................
Solving package specifications: .

# All requested packages already installed.
# packages in environment at /gpfs_fs/home/jcbagley/miniconda2:
#
libiconv                  1.15                          0    conda-forge

$
$ which libiconv
$ cd ~/miniconda2/lib
$ ls ./libiconv*
./libiconv.a  ./libiconv.la  ./libiconv.so  ./libiconv.so.2  ./libiconv.so.2.6.0

[/code]

The above listed the corresponding/correct lib files, so... I decided that the best solution at this point would be to add the Miniconda lib directory (folder) to my "$LD_LIBRARY_PATH" environmental variable. I did this using standard practices, as follows:

[code language="bash"]
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/gpfs_fs/home/jcbagley/miniconda2/lib
[/code]



**I then went back and started a fresh R install, and configure as well as make and install worked!!**



**Still, a successful install is not a suitable stopping point in bioinformatics. The same applies to every R install.**

You must always make sure that the version of the software that you have installed is actually available from the command line, and not superseded by a previous install; and we want the appropriate R version to have priority. In my case, even after installing R v3.4.4 locally, I found that a call to R would open the system version, v3.3.2, which of course was suboptimal. One easy fix for this is to alias "R" to the newly installed version. Specifically, you could add the following line to your "~/.bashrc" file and then source it:

[code language="bash"]
alias R="$HOME/R/bin/R"
[/code]

Afterwards, a call to R would always direct to the correct version corresponding to your user R install.

However, I realized that **a better solution** would be to move the "R" script generated during the R install (which is actually a shell script) into the main binary folder located within my "$PATH", which for me is `~/local/bin`, and that's what I did: 

[code language="bash"]$ cp R Rscript ~/local/bin
$ cd ~
$ R

R version 3.4.4 (2018-03-15) -- "Someone to Lean On"
Copyright (C) 2018 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

> q()
Save workspace image? [y/n/c]: n
[/code]



**_Problem solved!!_ I hope this helps someone else overcome the libiconv configure error that I encountered and successfully add an updated R install to their Linux account. Let me know in the comments section below!**

~J
