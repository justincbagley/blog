---
author: justin
comments: true
date: 2018-03-06 03:49:42+00:00
layout: post
link: http://www.justinbagley.org/3365/command-line-trash-how-to-delete-trash-and-inspect-files-from-the-cli
slug: command-line-trash-how-to-delete-trash-and-inspect-files-from-the-cli
title: 'Command line trash: how to delete, trash, and inspect files from the CLI'
wordpress_id: 3365
categories:
- bash
- blog posts
- command line
- Mac
- UNIX
tags:
- command line
- delete
- inspect
- rm
- trash
---

As many of you know, I use a UNIX/Mac system, and I spend a great deal of time working from the command line on UNIX and LINUX. One thing that everyone learns when they're learning the UNIX/LINUX command line is that the "rm" command is a powerful and versatile option for deleting files. However, when we delete files with rm, they never come back, and thus they cannot be inspected afterward. Adding the "-i" flag (e.g. "rm -i ) is an extremely useful safety feature for regular or recursive (i.e. folder-and-everything-in-it) deleting that will cause you to be prompted for confirmation that you _really_ want to permanently delete the target file(s) or directory; however, this can be a bit of a nuisance.



One thing that I figured out a while back was that several people have been interested in this issue. And, as a result of their efforts, there is some free software out there that can provide an alternative to rm, by providing "trash" functions. One such software is called "trash", was written by Ali Rantakari (available [here](http://hasseg.org/trash/)), and is easily installed from [Homebrew](https://brew.sh) as follows:


[code language="bash"]$ brew install trash[/code]


The install is very fast, and you can immediately start using trash to send files or directories to the Trash bin on your Mac. The basic syntax is "trash <file>", or "trash <file> <file> <dir>" for multiple targets. For example,
[code]$ ## Trashing example:
$ echo "" > file.txt
$ trash ./file.txt
[/code]



After "trashing" files from the command line, you may want to inspect the Trash to make sure the files actually made it to the trash bin, or to see what's there before clearing the bin. Of course, this is trivial with point-and-click approach; but you can still often avoid several unnecessary clicks or trips back and forth to the Trash by using the following code, especially in the case that you're already working from the command line anyway:


[code language="bash"]
$ ## Inspecting the Trash:
$ ## cd into Trash and have a look (simple and detailed views) with ls command:
$ cd ~/.Trash/
$ ls .
$ ls -al .
[/code]

It's also a good idea to remove files from the Trash selectively when working from the command line, rather than deleting all of the files in the Trash. At least, it's possible to imagine scenarios where this would be a better idea than the default "Empty Trash" menu option. 

Here's how to delete a specific file:

[code language="bash"]
$ ## Delete a single file:
$ rm ~/.Trash/<file>
[/code]

Here's how to delete a specific directory:

[code language="bash"]
$ ## Delete single directory:
$ rm -rf ~/.Trash/<path/to/dir>
[/code]

And, finally, here's how you can use a wildcard to quickly delete *all* files from the Trash simultaneously (with no hope of recovery):

[code language="bash"]
$ ## Delete *all* files in the Trash:
$ rm -rf ~/.Trash/*
[/code]

I hope this helps someone improve their usage of the command line. However, remember that, "With great power comes great responsibility" ~ Uncle Ben ([_Spider-Man_](https://en.wikipedia.org/wiki/Spider-Man_(2002_film)), 2002). Always remember that inappropriate use of rm commands such as those above can wipe out 1) precious files you didn't mean to delete but that wound up in the Trash, or 2) whole sets of files inside a directory. This mainly applies to the "-r" and "-R" flags for recursive deletion, which will not only delete an entire folder and all of it's contents; but it's a good thing to keep in mind.

~J
