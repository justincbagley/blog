---
author: justin
comments: true
date: 2016-04-06 15:22:18+00:00
layout: post
link: http://www.justinbagley.org/2262/kill-r-process-without-forcing-r-quit-mac
slug: kill-r-process-without-forcing-r-quit-mac
title: How to kill an R process without forcing R to quit on mac
wordpress_id: 2262
categories:
- blog posts
- command line
- Mac
- R
tags:
- command line
- CPU
- force quit
- kill
- mac
- R
---

From time to time, we make mistakes in programming or testing a new R script or function, only to find that R "freezes" and appears to be stuck, or working but giving the impression that it will take an eternity to complete the computation. What could be happening is that the process is based on an maximum-likelihood estimation of a parameter that requires convergence, you could have accidentally (e.g. by default) run a function that needs to visit the total number of models possible for your dataset or a certain amount of parameter space. Alternatively, there might be an issue with FORTRAN coding. Or, the function you're using might require a maximum number of iterations to be specified, or else it will use an exhaustive search. R can "hang" for these and many other reasons.




Today, I'm doing a short post to show you how to get out of this situation by killing the process in R from outside the R environment. Specifically, I'll show you how to do this from mac [Terminal](https://en.wikipedia.org/wiki/Terminal_(OS_X)), i.e. the command line.




First do the following at the command line to obtain a list of processes including R:


  

[code language="bash"]ps aux | grep R[/code]


Look through the resulting list of PIDs (process IDs, which are unique identifiers for each process) and info for the R process, which will likely be using a great deal of CPU (%CPU; eg. %CPU >90%), and thus will be near the top of the list (which will be in decreasing order). Here is an example of the results of running this code from my terminal to ongoing processes, including an R analysis (this is just an excerpt, the output was much longer):


  

[code language="bash"]Last login: Sun Apr 3 23:45:14 on ttys000 Justin-Bagleys-MacBook-Pro-3:~ justinbagley$ ps aux | grep R USER PID %CPU %MEM VSZ RSS TT STAT STARTED TIME COMMAND justinbagley 334 93.2 12.7 9618560 2122612 ?? R Tue05PM 317:07.03 /Applications/R.app/Contents/MacOS/R -psn_0_57358 justinbagley 339 7.2 2.1 4949212 355924 ?? R Tue05PM 47:05.88 /System/Library/CoreServices/Finder.app/Contents/MacOS/Finder _windowserver 200 1.7 1.4 14600476 231856 ?? Ss Tue05PM 113:19.80 /System/Library/Frameworks/ApplicationServices.framework/Frameworks/CoreGraphics.framework/Resources/WindowServer -daemon _mdnsresponder 94 0.2 0.0 2544976 3864 ?? Ss Tue05PM 0:39.06 /usr/sbin/mDNSResponder justinbagley 491 0.1 0.2 3713764 33524 ?? S Tue05PM 11:19.43 /System/Library/CoreServices/Dock.app/Contents/Resources/DashboardClient.app/Contents/MacOS/DashboardClient justinbagley 23663 0.0 0.0 3358044 6476 ?? S Fri10AM 0:02.38 /Applications/Adobe Acrobat Reader DC.app/Contents/Frameworks/RdrCEF helper.app/Contents/MacOS/RdrCEF helper --type=renderer --disable-3d-apis --disable-databases --disable-direct-npapi-requests --disable-file-system --disable-notifications --disable-shared-workers --no-sandbox --lang=en-US --lang=en-US --log-severity=disable --product-version=ReaderServices/15.10.20056 Chrome/45.0.2454.85 --enable-delegated-renderer --num-raster-threads=4 --gpu-rasterization-msaa-sample-count=8 --content-image-texture-target=3553 --video-image-texture-target=3553 --channel=23661.1.1456228839[/code]


An alternative way of getting this information on mac is to use the [Activity Monitor app](https://support.apple.com/en-us/HT201464), but we're not covering that here. OK, now armed with this information you can use the kill command to identify and stop the analysis. In my example above, the process ID for the R process is 334, and this process is consuming 93.2% of the CPU and 12.7% of the computer's memory, so we can stop this analysis by entering the following command at the command line:


  

[code language="bash"]kill -s INT 334[/code]


Two great things about this are 1) that this is easily accomplished at the command line, and 2) that you don't have to call R or alter R, or do "force quit" (e.g. by pressing option + command + Esc), you only have to stop the offending process. So, this means that R will not be closed as a result of these actions, but will be "liberated" from the hung prodess. As a result, your log of commands and output will not be lost.




Just as a tip, if you are worried about losing your command history at any time, you can usually save this from R even if the R environment/GUI hangs on an analytical process by first clicking the "Show/Hide R command history" button at the top of the R GUI, and then clicking "Save History."




~J
