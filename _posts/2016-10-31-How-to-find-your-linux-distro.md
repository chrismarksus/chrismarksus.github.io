---
layout: post
title:  "How to find your linux distro?"
date:   2016-10-31 22:45:51
categories: linux
tags: linux
---

Sometimes I work on a terminal over network and I need to update or investigate a packet, software etc... What Packet manager do I use *apt-get*, *rpm*, or *yum*? What linux distro am I on anyway, *Fedora*, *Ubuntu*? Who's driving this boat? Well after some research I discovered ways to find out the information I needed.

<!--more-->

I need to run acceptance tests on a project. I also need to run these tests in different versions of Firefox, Like when a newer browser is released. So I have a local folder with versions of firefox from 18 to 43. I downloaded Firefox 49.0.2 locally then tried to run it from the folder ```$ 49.0.2/./firefox``` *(This may look strange but its valid on the distro used)* and I got an error ```libgtk-3.so.0: cannot open shared object file: No such file or directory```.  Firefox versions 44 and 45 work fine.

Now what?

## Linux distro

To find out the distribution information after the machine you are on:
```
$ lsb_release -a
```

It will print the following information in the terminal.

```

LSB Version:    
Distributor ID:
Description:    
Release:        
Codename:

```

I find this to be the most useful for tracking down dependencies or software updates that are needed, Search Google, do a little reading etc...


## Kernal release number

If you need to find the kernal release number


```
$ uname -r
```

## Find installed packets like SSH or GTK+


If you are using a fedroa-based distribution *(Think Red Hat flavored linux)*:

```
$ rpm -qa | grep 'gtk'
```

If you are using a Debian-based distribution *(Think Ubuntu flavored linux)*:

```
$ dpkg -l openSSH

```
## Final
It turns out that Firefox 46-49 will not work because I have an older version  of the gtk+ library *(2.0)* and the newer versions need *(3.0)* to work. The distro is using *yum* as a packet manager and I don't have permission to install any software or updates at this level. Editing the environmental variable *PATH* will not cut it this time.

Oh well, guess you can't win them all! But now I know who talk too and what I need updated.
