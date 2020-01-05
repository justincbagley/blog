---
title: How to check Java version and JDK version on Mac
author: Justin Bagley
date: '2020-01-05'
slug: how-to-check-java-version-on-mac
categories:
  - Mac
  - Java
  - software
tags:
  - Mac
  - Java
  - Terminal
  - command line
  - software
  - UNIX
  - computing
---

[Java](https://www.java.com/) is a class-based, object-oriented programming language that is fast and powerful and runs many important computing programs and platforms. When you are about to download new software on Mac, developers may have generated multiple app containers (`.dmg` files) that install the software program in different ways depending on the operating system (macOS) and Java versions on your machine. In these situations, and others, it is very important to be able to quickly find out your Java and JDK versions on Mac.

In recent versions of [Java](https://www.java.com/) for macOS, the default install location for some files has changed and the places to look to determine your Java version, or Java JDK ("Java Development Kit"; technically, now Java SE Development Kit, which stands for "Java Platform, Standard Edition Development Kit"; downloads [here](https://www.oracle.com/technetwork/java/javase/overview/index.html)) version, have also changed accordingly. 

There are two ways that I recommend checking your Java version, and there is one procedure that I like to use to check which JDK is currently in use on my MacBook Pro. 

#### Checking Java version on macOS

**1. System Preferences**

This one is the easiest option for most users that like using the traditional, visual approach to computing on macOS. Simply open System Preferences ("Apple > System Preferences"), and then click "Java" (you will see the Java icon). The Java preferences open in a separate window, called "Java Control Panel." In Java Control Panel, do either
- a) click on the "General" tab, followed by the "About" button, to display Java version information, 

or 

- b) click on the "Update" tab in the control panel to display Java version information.

The version that is presented in the Java Control Panel is the currently running (=usually recommended) version of Java on your Mac machine.


**2. Command line (Terminal) procedure**

This is the method preferred by most users who are more familiar with personal computing and the command line interface. Simply open a shell interpreter (command line interface) such as the Terminal application, and type

```
java --version
```

The Java executable on your local machine will output the appropriate Java versioning information. And voilà, you're done!

On my machine, the sanitized version of this procedure looks like:

```
$ java --version
openjdk 11.0.1 2018-10-16 LTS
OpenJDK Runtime Environment Zulu11.2+3 (build 11.0.1+13-LTS)
OpenJDK 64-Bit Server VM Zulu11.2+3 (build 11.0.1+13-LTS, mixed mode)
```

#### Checking JDK version on macOS

**1. Command line (Terminal) procedures**

Similar to #2 under the "Checking Java version on macOS" section _above_, this is a command line procedure, which in my example will use Mac Terminal. Here, it's important to know that on recent versions of Java, the JDK is located at absolute path `/Library/Java/JavaVirtualMachines/`. Armed with this information, we can simply open Terminal and list the contents of this directory on our machine to find the JDK version, as follows:

```
ls /Library/Java/JavaVirtualMachines
```
 
The only potential issue here would be if you had multiple JDK versions installed. In that case, I recommend that users check their `$JAVA_HOME` bash environmental variable from within Terminal to make a JDK determination, as follows:

```
$ echo $JAVA_HOME
/Library/Java/JavaVirtualMachines/jdk1.8.0_101.jdk/Contents/Home
```

This, output on my machine, tells me that I am using JDK version 1.8.0\_101. Done!

I hope this helps someone who quickly needs to find information on Mac about their Java install before making other software install or updating decisions! 

~J
