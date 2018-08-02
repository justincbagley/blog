---
title: Installing gbs2ploidy and its rjags dependency in R on CentOS Linux
author: Justin Bagley
date: '2018-08-01'
slug: installing-gbs2ploidy-and-its-rjags-dependency-in-r-on-centos-linux
categories:
  - R
  - software
  - Linux
  - command line
  - code
  - blog posts
tags:
  - R
  - gbs2ploidy
  - jags
  - rjags
  - dependency
  - software
  - Linux
  - export
  - error
  - conda
  - miniconda
  - pkg-config
  - ploidy
  - plants
---

I am currently wrapping up a paper on GBS phylogeography of quaking aspen, _Populus tremuloides_ with several collaborators. See pic _below_:

![Quaking aspen](/images/2013-10-06_15_04_21_autumn_Aspens_ChangingCanyonNT_Lamoille_Canyon_NV.jpg)

_Quaking aspen (Populus tremuloides), Lamoille Canyon, NV_

Aspen are known to vary from diploid to triploid in natural populations, with many triploids (higher prevalence) in the Rockies. This is an issue with any population genomics study of aspen, or other forest trees with polyploidy. 

So, as a final touch on the manuscript, I need to estimate the occurrence of varying ploidy number across individuals in the dataset and see if ploidy is significantly affecting (e.g. correlated to) the results. Karen Mock at Utah State University is a collaborator on the current GBS project and has advised us to use the new [gbs2ploidy](https://cran.r-project.org/web/packages/gbs2ploidy/index.html) R package written by Zack Gompert in their [2017 paper](https://onlinelibrary.wiley.com/doi/abs/10.1111/1755-0998.12657) on the subject (Gompert and Mock 2017). 

I had some issues with the install, so to help others who might encounter similar issues, I am writing a post about what I ran into and how to overcome the problems (which will probably be general, not reflecting simply a user-specific case).

## Install Issues

_Environment: CentOS 6/7 Linux, R version 3.4.4 (2018-03-15) -- "Someone to Lean On"_ 

The specific issue I ran into was failure to install the 'rjags' ```R``` package, which is one of the two main dependencies of gbs2ploidy. A regular installation attempt with ```install.packages('gbs2ploidy', dependencies=TRUE)``` failed with the following error output to screen:

```
> 
> install.packages("gbs2ploidy", dependencies=TRUE)
also installing the dependency ‘rjags’

trying URL 'https://cran.rstudio.com/src/contrib/rjags_4-6.tar.gz'
Content type 'application/x-gzip' length 71719 bytes (70 KB)
==================================================
downloaded 70 KB

trying URL 'https://cran.rstudio.com/src/contrib/gbs2ploidy_1.0.tar.gz'
Content type 'application/x-gzip' length 1294606 bytes (1.2 MB)
==================================================
downloaded 1.2 MB

* installing *source* package ‘rjags’ ...
** package ‘rjags’ successfully unpacked and MD5 sums checked
checking for pkg-config... /usr/bin/pkg-config
configure: WARNING: pkg-config file for jags 4 unavailable
configure: WARNING: Consider adding the directory containing `jags.pc`
configure: WARNING: to the PKG_CONFIG_PATH environment variable
configure: Attempting legacy configuration of rjags
checking for jags... no
configure: error: "automatic detection of JAGS failed. Please use pkg-config to locate the JAGS library. See the INSTALL file for details."
ERROR: configuration failed for package ‘rjags’
* removing ‘/gpfs_fs/home/jcbagley/R/lib64/R/library/rjags’
ERROR: dependency ‘rjags’ is not available for package ‘gbs2ploidy’
* removing ‘/gpfs_fs/home/jcbagley/R/lib64/R/library/gbs2ploidy’

The downloaded source packages are in
	‘/gpfs_fs/home/jcbagley/tmp/RtmpkmTK42/downloaded_packages’
Updating HTML index of packages in '.Library'
Making 'packages.html' ... done
Warning messages:
1: In install.packages("gbs2ploidy", dependencies = TRUE) :
  installation of package ‘rjags’ had non-zero exit status
2: In install.packages("gbs2ploidy", dependencies = TRUE) :
  installation of package ‘gbs2ploidy’ had non-zero exit status
> 
> 
```

As the error stated, the issue was that the ```pkg-config``` file for jags ('jags.pc') was not available and so a "legacy" method of configuration of rjags was attempted and failed. The suggested solution set the ```$PKG_CONFIG_PATH``` environmental variable correctly. However, this did not solve the problem for me either. Downloading the rjags and gbs2ploidy source files respectively <a href="https://cran.r-project.org/src/contrib/rjags_4-6.tar.gz">here</a> and <a href="https://cran.r-project.org/src/contrib/gbs2ploidy_1.0.tar.gz">here</a>, e.g. by using 

```
$ curl -O -J -L https://cran.r-project.org/src/contrib/rjags_4-6.tar.gz
``` 

and attempting to install them manually from source (not a repo), e.g. by 

```
R CMD INSTALL rjags_4-6.tar.gz
```

_likewise failed_.


## Solution

It became clear to me that the solution here was going to involve multiple steps. First, I installed ```pkg-config``` and the original ```jags``` MCMC software locally, into my user account, using my Miniconda utility ```conda```:

```
$ conda install pkg-config jags ## Type this, then accept changes with a yes answer, 'y'
$                               ## This gets pkg-config v0.29.2 and jags v4.3.0
...
```

Now that these up-to-date versions of these important software programs were installed into my Miniconda directory, which for me is ~/miniconda2/, I could set the ```$PKG_CONFIG_PATH``` variable to point to my miniconda2 pkg-config folder:

```
export PKG_CONFIG_PATH="~/miniconda2/lib/pkgconfig"
```

Afterwards, all I needed to do was fire up ```R``` and install gbs2ploidy again, and _voila_!

```
> install.packages("gbs2ploidy", dependencies=TRUE)
also installing the dependency ‘rjags’

trying URL 'https://cran.rstudio.com/src/contrib/rjags_4-6.tar.gz'
Content type 'application/x-gzip' length 71719 bytes (70 KB)
==================================================
downloaded 70 KB

trying URL 'https://cran.rstudio.com/src/contrib/gbs2ploidy_1.0.tar.gz'
Content type 'application/x-gzip' length 1294606 bytes (1.2 MB)
==================================================
downloaded 1.2 MB

* installing *source* package ‘rjags’ ...
** package ‘rjags’ successfully unpacked and MD5 sums checked
checking for pkg-config... /gpfs_fs/home/jcbagley/miniconda2/bin/pkg-config
configure: Setting compile and link flags according to pkg-config
configure: Compile flags are -I/gpfs_fs/home/jcbagley/miniconda2/include/JAGS
configure: Link flags are -L/gpfs_fs/home/jcbagley/miniconda2/lib -ljags
checking for gcc... /gpfs_fs/home/jcbagley/miniconda2/bin/c++
checking whether we are using the GNU C compiler... no
checking whether /gpfs_fs/home/jcbagley/miniconda2/bin/c++ accepts -g... no
checking for /gpfs_fs/home/jcbagley/miniconda2/bin/c++ option to accept ISO C89... unsupported
checking for jags_version in -ljags... yes
checking version of JAGS library... OK
configure: creating ./config.status
config.status: creating src/Makevars
configure: creating ./config.status
config.status: creating src/Makevars
config.status: creating R/unix/zzz.R
** libs
g++  -I/gpfs_fs/home/jcbagley/R/lib64/R/include -DNDEBUG -I/gpfs_fs/home/jcbagley/miniconda2/include/JAGS   -I/usr/local/include   -fpic  -g -O2  -c jags.cc -o jags.o
g++  -I/gpfs_fs/home/jcbagley/R/lib64/R/include -DNDEBUG -I/gpfs_fs/home/jcbagley/miniconda2/include/JAGS   -I/usr/local/include   -fpic  -g -O2  -c parallel.cc -o parallel.o
/gpfs_fs/home/jcbagley/miniconda2/bin/g++ -shared -L/usr/local/lib64 -o rjags.so jags.o parallel.o -L/gpfs_fs/home/jcbagley/miniconda2/lib -ljags
installing to /gpfs_fs/home/jcbagley/R/lib64/R/library/rjags/libs
** R
** data
** preparing package for lazy loading
** help
*** installing help indices
** building package indices
** testing if installed package can be loaded
* DONE (rjags)
* installing *source* package ‘gbs2ploidy’ ...
** package ‘gbs2ploidy’ successfully unpacked and MD5 sums checked
** R
** data
** preparing package for lazy loading
** help
*** installing help indices
** building package indices
** testing if installed package can be loaded
* DONE (gbs2ploidy)

The downloaded source packages are in
	‘/gpfs_fs/home/jcbagley/tmp/RtmpLladKh/downloaded_packages’
Updating HTML index of packages in '.Library'
Making 'packages.html' ... done
> 
> 
> 
> library(gbs2ploidy)
Loading required package: MASS
Loading required package: rjags
Loading required package: coda
Linked to JAGS 4.3.0
Loaded modules: basemod,bugs
```

That's all folks.

~J

## References

Gompert, Z., & Mock, K. E. (2017). Detection of individual ploidy levels with genotyping‐by‐sequencing (GBS) analysis. _Molecular Ecology Resources_, 17(6), 1156–1167.
