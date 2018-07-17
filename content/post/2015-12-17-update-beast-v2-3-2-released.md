---
author: Justin Bagley
comments: true
date: 2015-12-17 13:04:58+00:00
layout: post
link: http://justinbagley.rbind.io/2015/12/17/update-beast-v2-3-2-released/
slug: update-beast-v2-3-2-released
title: 'Update: BEAST v2.3.2 released!'
categories:
- BEAST
- blog posts
- Software
tags:
- BEAST
- BEAUti
- error reporting
- software
- update
---

![BEAST2 logo](/images/cropped-beast2-logo-2-1024x118.png)  
_BEAST2 logo_

Hi guys, OK, in case you haven't heard, there is a new version of [BEAST2](http://beast2.org), so make sure that you go get that [update on GitHub](https://github.com/CompEvol/beast2/releases). According to Remco Bouckaert, the new version, v2.3.2, improves the ability of the user to interact with data in BEAUti, and it also improves the efficiency of some BEAST functions, particularly the MRCAPrior. Moreover, LogCombiner has been fixed to ensure logcombiner burn in editing finished properly, and LogAnalyser now has one line per file mode. Supposedly, BEAST now has "more sensible error messages" in several packages.

However, I find that BEAST is still plagued with problematic error reporting in some cases. Take for example this infamous error: "Parsing error - the input file is not a valid XML file". The program developers have made [good suggestions](http://beast.community/errors.html) for dealing with such vague errors. But hopefully the guys will continue to improve error reporting and related issues much more in future versions.

~J
