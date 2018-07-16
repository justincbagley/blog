---
author: justin
comments: true
date: 2010-08-03 15:14:00+00:00
layout: post
link: http://www.justinbagley.org/142/unpacking-a-gzipped-tarball
slug: unpacking-a-gzipped-tarball
title: Unpacking a gzipped tarball!!!!
wordpress_id: 142
categories:
- bash
- blog posts
- command line
- UNIX
- Windows
tags:
- command line
- download
- Linux
- tarball
- UNIX
- UNIXutils
- unzip
- windows
---

Unpacking [gzipped tarballs](https://en.wikipedia.org/wiki/Tar_(computing)) and similar files is routine for molecular phylogeographers and molecular systematists. For example, it is a common and necessary step involved when downloading new programs and associated files (e.g., certain html documentation; CONSEL by Hidetoki Shimodaira) or certain analytical output files (e.g., those of MIGRATE-N by Peter Beerli, when output from Cornell cluster) that have been compressed.







Assuming the tarball is named "name_rslts.tgz", you can unpack a gzipped tarball using the following commands with the folder/directory your file is in as the current directory (use cd to get there on windows machines)...











[code language="bash"]gzip -d name_rslts.tgz
tar -xvf name_rslts.tar[/code]











This is all based in [UNIX](https://en.wikipedia.org/wiki/Unix), so if you are using a Windows machine you will need to get the full set of UNIX utilities to do this. Luckily those can be downloaded as UNIXutils.zip online from [sourceforge](http://unxutils.sourceforge.net/). Once you've got that done, you actually will execute











[code language="bash"]C:\UNIXutils\bin\gzip -d name_rslts.tgz
C:\UNIXutils\bin\tar -xvf name_rslts.tar[/code]










from the DOS prompt in Windows. You can put the file and UNIXutils in the same directory, which doesn't necessarily have to be C:\, it could be the Desktop or wherever.




~ JB







[Refs](http://cbsuapps.tc.cornell.edu/blast_s_helpwin.aspx?hid=ungzip&app=migrate)
