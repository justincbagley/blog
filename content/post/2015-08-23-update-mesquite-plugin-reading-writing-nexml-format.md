---
author: justin
comments: true
date: 2015-08-23 13:58:21+00:00
layout: post
link: http://www.justinbagley.org/1224/update-mesquite-plugin-reading-writing-nexml-format
slug: update-mesquite-plugin-reading-writing-nexml-format
title: Update Mesquite with plugin for reading and writing NeXML format
wordpress_id: 1224
categories:
- blog posts
tags:
- DAMBE
- Mesquite
- NeXML
- NEXUS
---

In case you were unaware, there is a community-driven "NeXML" movement in computational phylogenetics, led by several bioinformaticians including Rutger Vos who are attempting to harness technologies and advantages of the XML format for transforming NEXUS flat files (an older standard for storing systematic data) into a format that is more easily processed and manipulated. See [NeXML.org](http://nexml.org) for more info on this technology and for softwares that allow reading and writing NeXML etc. Another good resource to consult is the [NeXML manual on GitHub](https://github.com/nexml/nexml/wiki/NeXML-Manual#Guide_to_Resources).

However, given NEXUS format was popularized by the Maddison brothers (see for example [Maddison et al. 1997](http://sysbio.oxfordjournals.org/content/46/4/590.short)), it is telling that they are 1) still on the cusp of things and 2) see the value of NeXML format that they have been open to helping implement a recent plugin for their modular software Mesquite, allowing the program to read and write NeXMLs. Vos is currently responsible for maintaining the plugin, which was initially developed by Wayne Maddison and Peter Midford.

Here, I'm going to briefly tell you how to install the "nexml Mesquite plugin." Before proceeding, however, make sure you've read about NeXML and familiarized yourself with the format a bit, by looking into the links above.

1. Make sure you have the newest version of Mesquite, which is v3.0.4! Get it from the [Download and Installation ](http://mesquiteproject.wikispaces.com/Installation)section of the new [Mesquite Project wikispaces](http://mesquiteproject.wikispaces.com) website if you don't have it already. Make sure Mesquite is in your Applications folder (on mac), or wherever you want it to be; note the location; and make sure Mesquite downloads into a folder named "Mesquite_Folder."

2. Download the nexml Mesquite plugin from direct FTP/Dropbox, by clicking here: [nexml_Mesquite_plugin download](https://www.dropbox.com/sh/yp8t4jvb5id879m/S7ERRMkUpw). 

3. The plugin downloads to a single folder, within which you will find two subfolders labeled "mesquite" and "org." In turn, each of these subfolders has its own "nexml" folder. You need to copy each of these "nexml" folders and paste them into the subfolder with the _same names _in the "Mesquite_Folder" that contains Mesquite. 

  1. Copy and paste the .../mesquite/nexml folder into the folder located at .../Mesquite_Folder/mesquite.
  2. Copy and paste the .../org/nexml folder into the folder located at .../Mesquite_Folder/org.

OK, now you're done, so give it a try! Open Mesquite v3.0.4 and test it. See if you can read and write NeXML files. 

In case you don't have one, here is a link to a test NeXML [labroids test NeXML file](http://treebase.org/treebase-web/search/downloadATree.html?id=12889&format=nexml&treeid=53749) to try. This file is from a paper on the evolution of pharyngeal jaw key innovation in labroid fishes (wrasses) by Wainwright et al. (2012). I got their NeXML from their [Wainwright et al. 2012 Treebase submission](http://treebase.org/treebase-web/search/study/summary.html?id=12889) submission.

PS Another program that reads and writes NeXML format is DAMBE, but I tried using it for this purpose with a test file and DAMBE crashed on me. I think it was because DAMBE had trouble handling the particular properties of my test file. Still, as it may be a bit more finicky to use DAMBE for interacting with NeXMLs, I'll recommend sticking with Mesquite (or downloading the java libraries from the NeXML GitHub, etc).

Cheers!

~J

**_References_**

Wainwright P.C., Smith W.L., Price S.A., Tang K.L., Sparks J.S., Ferry L.A., Kuhn K.L., Eytan R.I., & Near T.J. 2012. The evolution of pharyngognathy: a phylogenetic and functional appraisal of the pharyngeal jaw key innovation in labroid fishes and beyond. Systematic Biology, .
