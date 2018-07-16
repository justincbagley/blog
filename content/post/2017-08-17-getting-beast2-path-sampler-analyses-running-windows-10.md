---
author: justin
comments: true
date: 2017-08-17 18:18:35+00:00
layout: post
link: http://www.justinbagley.org/3009/getting-beast2-path-sampler-analyses-running-windows-10
slug: getting-beast2-path-sampler-analyses-running-windows-10
title: Getting BEAST2 Path Sampler analyses running on Windows 10
wordpress_id: 3009
categories:
- BEAGLE
- BEAST
- blog posts
- Java
- Mac
- UNIX
- Windows
tags:
- Beagle
- BEAST
- BEAST2
- java
- Path Sampler
- path sampling
---

[![](http://www.justinbagley.org/wp-content/uploads/2017/08/BEAST2_PathSampler_logo_inAppStore.png)](http://www.justinbagley.org/wp-content/uploads/2017/08/BEAST2_PathSampler_logo_inAppStore.png)**I am a relatively big Mac (UNIX) and Linux fan, as many of you know.** So, my standard approach to running [BEAST](http://beast.community) or [BEAST2](http://beast2.org/) is to use my Mac for local setup and testing and then employ shell scripts (effective wrappers) that I've developed to automate final run setup and queuing on a Linux supercomputing cluster. However, there are times, especially when running path sampling (PS) analysis (Larillot and Phillipe 2006; Baele et al. 2012; [Baele 2016 lecture](https://www.biostat.washington.edu/sites/default/files/modules//2016_SISMID_13_10.pdf)) to estimate log-marginal likelihoods of BEAST models, when I tend to run into issues on the supercomputer. These are often memory problems (e.g. step memory limits), input XML reading errors, and other issues, and oddly they can happen when attempting to run PS XML files that pass local run tests. In these times (but only with small numbers of models, to date), **I turn to running PS analysis locally using the [Path Sampler](https://www.beast2.org/2014/07/14/path-sampling-with-a-gui/) GUI version (image _at upper left_), and I use as many computers as I have at my disposal!**




Today, I wanted to speed up parallel PS runs by adding a **2.2 GHz [Lenovo Windows 10 laptop](https://www.google.com/search?client=safari&rls=en&q=lenovo+windows+10+laptop&ie=UTF-8&oe=UTF-8)** that came available, but which did not have BEAST or [BEAGLE](https://github.com/beagle-dev/beagle-lib) installed! So, I eased back into the waters of (1) Windows BEAST setup, and more generally (2) setting up Windows for analyzing scientific data, in general--two things that I essentially hadn't done since the early/mid part of my PhD, before I switched to Mac.




_This post briefly explains how I got BEAST Path Sampler working with the BEAGLE API/scientific computing library on [Windows 10](https://www.microsoft.com/en-us/windows/)._




##### **Steps**




**The 7 steps I followed to setup BEAST2 and BEAGLE on Windows:**





	
  1. [![](http://www.justinbagley.org/wp-content/uploads/2017/08/BEAGLE_2.1_dropbox_installer_file.png)](http://www.dropbox.com/s/61z48jvruzkwkku/BEAGLE-2.1.msi)Install/update Oracle Java [1.7](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html) and [1.8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) runtime environments.

	
  2. Install BEAGLE v2.1 using [binary installer](http://www.dropbox.com/s/61z48jvruzkwkku/BEAGLE-2.1.msi) (.msi file, image/link _at left_) from the [beagle-dev GitHub account](https://github.com/beagle-dev/).

	
  3. Install BEAST2 v2.4.7 for Windows by downloading and saving .zip file [here](https://github.com/CompEvol/beast2/releases/download/v2.4.7/BEAST.v2.4.7.Windows.zip).

	
  4. Install latest [Java SE Development Kit](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) (jdk8) for 64bit Windows.

	
  5. Set global, and user, Path environmental variables to include libhmsbeagle and the path to an appropriate Java bin folder (recommended starting point: JRE bin; _see below_).

	
  6. Open BEAUti v2.4.7 and manage packages (adding most available packages), then closing and reopening BEAUti to check.

	
  7. Test the installs by conducting runs with BEAST and Path Sampler!




##### **Details**




**Steps #1-4**




Steps #1–4 were accomplished using standard methods, for example following installer prompts to designate a drive and agree to the license, etc. For BEAST + BEAGLE install alone, step #4 above might not be considered obligatory by others. In any event, we subsequently set the path to the latest JRE. However, there are indications from discussions in online forums that using JDK may have helped some users overcome issues. And, in my experience it seems it is always better to install the JDKs as well, so that you can point to them if needed. Thus, I consider step #4 to be recommended (just to be on the safe side).




**Step #5**




[caption id="attachment_3017" align="alignleft" width="326"][![](http://www.justinbagley.org/wp-content/uploads/2017/08/Windows10_control_panel.png)](http://www.justinbagley.org/wp-content/uploads/2017/08/Windows10_control_panel.png) _Windows 10 Control Panel_[/caption]




The only part of this procedure that really required any extra thinking and work at all was step #5. Here, all you have to remember is _that much can be done on Windows through _[_Control Panel_](https://support.microsoft.com/en-us/help/13764/windows-where-is-control-panel)! You simply





	
  1. Go to Advanced system settings by navigating to [Control Panel](https://support.microsoft.com/en-us/help/13764/windows-where-is-control-panel) > System and Settings > System > Advanced system settings (on left pane)

	
  2. Click on "Environmental Variables" at the bottom of the pop-up window that is displayed.

	
  3. Set the User and System "Path" variables in the list so that libhmsbeagle (BEAGLE directory; where BEAGLE was installed) is part of the path.



	
    1. Do this by selecting Path, then adding "; C:\path\to\libhmsbeagle" to the end of the current/default Path (that is, separate the original path from the libhmsbeagle path you are adding, by using a semicolon).

	
    2. Do this under User variables and under System variables.







On the machine that I used, the BEAGLE path was




[code language="bash"]C:\Program Files (x86)\Common Files\libhmsbeagle\ [/code]




and the Java bin path was




[code language="bash"]C:\Program Files (x86)\Java\jre1.8.0_144\bin [/code]




(corresponding to the very latest JRE available (follow link given under Step #1 above). If you follow my steps now, and do a standard install of this software, check me on this, but you should be able to use the same path settings as these.




**Steps #6 and #7**




The final two steps are quite easy. For step #6, you can easily accomplish this from within the BEAUti v2.4.7 GUI by





	
  1. Opening the GUI,

	
  2. Clicking on File > Manage Packages,

	
  3. Choosing and installing packages of interest,

	
  4. Then closing and reopening (look back in the package manager) to check that everything was in fact installed or updated.




Step #7 also is quite easy, because it just involves playing with example files and making sure everything runs fine. However, you want to make sure to do two things here--check that BEAST software and utilities are opening and running fine, and _also _make sure that BEAGLE is found and utilized by BEAST and its packages.




##### **Troubleshooting**




If you get an error that says, "Failed to load BEAGLE library: no hmsbeagle-jni in java.library.path," then you are potentially about to _go down the rabbit hole_ to fix that issue!! Your best bet is to follow my general procedure above, update Java, and make sure you set a path variable for Java _in addition _to BEAGLE lib. If this doesn't work, uninstall and reinstall BEAGLE, then reset the path. In the event of any issue with BEAST, I always recommend consulting recent discussions on the beast-users group discussion boards for additional information. In this case, it may help to see [this relevant post](https://groups.google.com/forum/#!searchin/beast-users/-Djava.library.path$20beagle%7Csort:relevance/beast-users/GdBaFiJq1QA/cMq9h3XnBpAJ)* on the [beast-users](https://groups.google.com/forum/#!forum/beast-users) Google Group (*full disclosure: I have not tested the suggestions there).




**I hope that someone finds this useful! Cheers, and good luck with BEAST! Also, thanks to the developers for working hard to provide great BEAST software that works on Mac, Linux, _and_ Windows!**




~J




##### References




Baele G, Lemey P, Vansteelandt S (2013) Make the most of your samples: Bayes factor estimators for high-dimensional models of sequence evolution. _BMC __Evol. Biol._ 14, 85.
















Lartillot N, Philippe H (2006) Computing Bayes factors using thermodynamic integration. _Syst. Biol._ 55, 195-207.












