---
title: Problems with locate after Homebrew update on Mac
author: Justin Bagley
date: '2019-12-31'
slug: problems-with-locate-after-homebrew-update-on-mac
categories:
  - Mac
  - software
tags:
  - locate
  - Homebrew
  - brew
  - command line
  - software
  - UNIX
  - Mac
  - macos
  - sudo
  - computing
---

Recently, after updating <a href="https://brew.sh">Homebrew</a> on macOS High Sierra (v10.13.6), I began experiencing a `locate` error every time I logged into a mac Terminal window. The error message was as follows:

```
locate: locate database header corrupt, bigram char outside 0, 32-127: -1
```

I found some information on this error online, <a href="https://github.com/Homebrew/legacy-homebrew/issues/42922">here</a>, and decided to use it, first removing the locate database, as follows:

```
rm -rf /var/db/locate.database
```

but this created its own set of problems. Now, instead of loading correctly, I got a new error message stating that the locate database did not exist. The new error was as follows:

```
WARNING: The locate database (/var/db/locate.database) does not exist.
To create the database, run the following command:

  sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist

Please be aware that the database can take some time to generate; once
the database has been created, this message will no longer appear.


WARNING: The locate database (/var/db/locate.database) does not exist.
To create the database, run the following command:

  sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist

Please be aware that the database can take some time to generate; once
the database has been created, this message will no longer appear.
```

The usually recommended fix for this issue, I learned, was to regenerate the database, but the following common method for this also failed:

```
sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist
```
... giving the same "...does not exist..." error set as shown above.

What finally worked for me was to generate the `locate` database anew (it took a long time!) using the following command, recommended in <a href="http://osxdaily.com/2011/11/02/enable-and-use-the-locate-command-in-the-mac-os-x-terminal/">this post on OSXDaily</a>:

```
sudo /usr/libexec/locate.updatedb
```

After the new `locate`database was generated, Terminal loaded normally and all `locate`-related errors stopped, and I continue to have no issues with `locate`. I hope that this helps someone who runs across this problem in the future.

~J
