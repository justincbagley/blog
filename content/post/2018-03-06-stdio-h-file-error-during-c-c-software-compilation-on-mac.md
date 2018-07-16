---
author: justin
comments: true
date: 2018-03-06 04:14:15+00:00
layout: post
link: http://www.justinbagley.org/3386/stdio-h-file-error-during-c-c-software-compilation-on-mac
slug: stdio-h-file-error-during-c-c-software-compilation-on-mac
title: stdio.h file error during C/C++ software compilation on Mac
wordpress_id: 3386
categories:
- blog posts
- compiling software
- Mac
- Xcode
tags:
- C
- error
- file
- gcc
- header
- stdio.h
---

[![](http://www.justinbagley.org/wp-content/uploads/2018/03/errorstop-300x300-150x150.png)](http://www.justinbagley.org/wp-content/uploads/2018/03/errorstop-300x300.png)Recently, back in February of 2018, I updated [Xcode](https://developer.apple.com/xcode/) and installed the macOS High Sierra Supplemental Update as well. I was _quite_ unhappy to find out that, following these updates, compiling software written in C/C++ using gcc (which was up to date!) seemed to be failing with a "stdio.h" file not found error, as follows:



[code language="bash"]...fatal error: stdio.h: No such file or directory
#import<stdio.h>;
       ^
1 error generated.
...
[/code]

The missing file was the same in multiple cases, for multiple software programs that I think included both the species tree inference software [SVDquartets](https://www.asc.ohio-state.edu/kubatko.2/software/SVDquartets/) and the popgen/selection forward-time simulation program [SFS_CODE](http://sfscode.sourceforge.net/SFS_CODE/index/index.html). The ".h" extension indicates that the compiler could not find an important header file, a kind of file that provides declarations and macros for the main source code of C/C++ software. Luckily, after zooming around online threads, I found the following very straightforward solution [here](https://github.com/frida/frida/issues/338): simply reinstall Xcode Command Line Tools. I did this by typing the following into Terminal and hitting return...

[code language="bash"]$ xcode-select --install
[/code]

Next, I clicked "Install" and a window indicated when the install was complete. I then checked the install in Terminal by doing "$ xcode-select -p"...and voila! When I retried make in the software's distribution or src folder (e.g. the distribution folder in the case of SFS_CODE), I was at last able to get the software to build correctly and produce working executables. I hope this helps someone else who might run across the same or a similar problem.

~J
