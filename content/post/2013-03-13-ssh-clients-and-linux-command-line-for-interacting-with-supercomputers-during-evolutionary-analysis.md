---
author: justin
comments: true
date: 2013-03-13 14:05:00+00:00
layout: post
link: http://www.justinbagley.org/116/ssh-clients-and-linux-command-line-for-interacting-with-supercomputers-during-evolutionary-analysis
slug: ssh-clients-and-linux-command-line-for-interacting-with-supercomputers-during-evolutionary-analysis
title: SSH clients and Linux command line for interacting with supercomputers during
  evolutionary analysis
wordpress_id: 116
categories:
- blog posts
- Linux
- Software
- SSH
- supercomputers
tags:
- cluster
- command line
- compute
- Linux
- nodes
- resource management
- SSH
- supercomputers
---

At the time of this writing, I am fortunate to be doing my PhD at [BYU](https://home.byu.edu/home/), which is a great environment to work on biogeography, systematics and evolution mainly because of the great people with similar interests that seem to always be attracted to the place.  However, I am also very fortunate that at my institution we have excellent infrastructure and internal resources for conducting the highest quality research in molecular evolution and ecology.  In particular, students and faculty have access to a cutting edge DNA Sequencing Center (accessed here) as well as high-power supercomputers for running computationally burdensome algorithms and software during statistical analyses (think you of phylogenetic and population genetics software, where inference is increasingly based on explicit modeling), through BYU's Fulton Supercomputing Lab (for more information visit their webpage at [http://marylou.byu.edu/](http://marylou.byu.edu/)).   

  

While the supercomputer is a great resource, I have found that life interacting with the supercomputer can be wonderful at times or seemingly-eternally frustrating at others (e.g. if things run slow, download/exchange capabilities are limited for some reason, the supercomputer is broken, or things don't run at all)!  And there have been plenty of "if I only knew then what I know now" moments as I have mastered the basics of putting these resources to work for me.  Nevertheless, an integral part of successfully using supercomputing resources for evolutionary analyses is having the most flexible means of communicating securely and rapidly with the available computing resources.  In this regard, among your greatest friends in data management and analysis become platform-format [SSH clients](https://en.wikipedia.org/wiki/Comparison_of_SSH_clients) (e.g. software programs that use [secure shell](https://en.wikipedia.org/wiki/Secure_Shell) protocols) and command-line knowledge.  That's what I want to discuss today, especially what I've found playing around with different SSH platforms and command line tricks.  The supercomputer we use is Linux based and so I will also get into Linux-specific issues that I have learned a little about.  

  

[SFTP](https://en.wikipedia.org/wiki/SSH_File_Transfer_Protocol) (Secure File Transfer Protocol) software programs are necessary to conduct file transfers between computers, networks, etc., by sending data through secure information tunnels known as [secure shells](https://en.wikipedia.org/wiki/Secure_Shell) (SSH).  The (terminal emulator or terminal, or other) software for this purpose and for related functions will contain files, menus or buttons  (or perhaps even names) with the word "protocol" in them.  In other words, as you learn about SSH, this word will keep popping up.  Uninitiated users will probably note this as strange.  However, "protocol" in this sense simply refers to a set of message formats and rules for exchanging digital message information.  SFTP software programs have a range of capabilities, but all the main ones are true OpenSSH software or are open source multi-clients that specialize in cryptographic communication sessions between devices/people.  

  

Although many SSH client software exist, a common and excellent choice for Windows machines is [WinSCP](https://winscp.net/eng/index.php).  I have now made the switch from Windows to Mac-almost-full-time.  And during this change I came across the problem of needing to (a) find capability to run WinSCP on my Mac (which didn't really interest me) or (b) find the best SSH client software available for mac users.  In making this change, I first went online to mac forums and discovered the program [Fugu](http://rsug.itd.umich.edu/software/fugu/).  I quickly downloaded it and it ran fine, but was a nightmare on two important counts: Fugu does not have the capability of transferring directories! and Fugu also can be slow at best.  After several days using Fugu, I broke down and realized I needed a new software.  I went back online and searched for other software, and I finally found what I had been wanting: [Cyberduck](https://cyberduck.io/?l=en).  This program is hands-down the best SSH client software for mac that I have found and I recommend that you use it also (although [Filezilla](https://filezilla-project.org) is a close second).   

  

Later, I will discuss other SFTP software to avoid, and the many features that [Cyberduck](https://cyberduck.io/?l=en) has that will help you interact with your supercomputer with ease.  Also I will review the command line interface and how to use other SSH client software to run interact with supercomputers to run programs during analyses.  

  

~J
