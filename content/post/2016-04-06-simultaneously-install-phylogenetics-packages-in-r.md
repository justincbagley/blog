---
author: Justin Bagley
comments: true
date: 2016-04-06 15:43:16+00:00
layout: post
link: http://justinbagley.rbind.io/2016/04/06/simultaneously-install-phylogenetics-packages-in-r/
slug: simultaneously-install-phylogenetics-packages-in-r
title: Automatically install or update all phylogenetics packages in R
categories:
- blog posts
- Phylogenetics
- R
tags:
- Brian O'Meara
- CRAN
- ctv
- install
- packages
- phylogenetics
- R
- views
---

In case you are unaware of this trick, it is possible to simultaneously install or update all of the phylogenetics packages available in R in one fail swoop.

A number of different CRAN Task Views have been created summarizing R packages and utilities for different fields of analysis or research. Luckily, there is not only a compilation of these located on the CRAN-R website [here](https://cran.r-project.org/web/views/), but also [Brian O'Meara](https://twitter.com/omearabrian) (@omearabrian #omearabrian) has developed a nice CRAN Task View entitled "Phylogenetics, Especially Comparative Methods." This means that you can view all of the software for phylogenetics and phylogenetic comparative methods in R at one time from the corresponding [Phylogenetics website](https://cran.r-project.org/web/views/Phylogenetics.html). Here is what these websites look like:

[![CRAN_Task_Views_screenshot](/images/CRAN_Task_Views_screenshot-768x407.png)](/images/CRAN_Task_Views_screenshot-1024x542.png)
[![Omeara_Phylogenetics_ctv](/images/Omeara_Phylogenetics_ctv-768x407.png)](/images/Omeara_Phylogenetics_ctv-1024x543.png)

The most important thing, though, is that you can automatically install the entire Phylogenetics, Especially Comparative Methods view! Here's how you do it! First, open R, download the [ctv package](https://cran.r-project.org/web/packages/ctv/index.html)(ctv stands for "CRAN Task Views"), then load the ctv library by typing:

```
library(ctv)
```


Next, you can install the Phylogenetics, Especially Comparative Methods view using the 'install.views' function, and later you can update this view using the 'update.views' function. If this is your first time using R for phylogenetics, you will not have any of the phylogenetics software, so you will do the following to install the view:

```
install.views('Phylogenetics')
```

If you have already been working with phylogenies in R and have some of the related packages installed, you will want to use update.views as follows:

```
update.views('Phylogenetics')
```

This will check through all of the packages in the Phylogenetics, Especially Comparative Methods view and update packages you already have installed, while also installing for the first time any packages that are missing. Here, an important note to make is that you must 1) be connected to the internet to do this, and 2) realize that this could take a substantial amount of time to install all of the packages. So, only do this when you have time!!

~J
