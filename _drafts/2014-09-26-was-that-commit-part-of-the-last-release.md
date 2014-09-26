---
layout: post
title: "Was that commit part of the last release?"
category: source control
tags: git 
---

You're sitting at your desk when someone comes down and asks if that code change that you said you were going to deliver made it into the lastest release. Due to organizational or long build/deployment times you not sure if it made it into this or that version. If your team/company/organiztion is tagging your releases (and they should be) then it should be pretty easy.

<!--more-->

>Tagging in git has 2 version *lightweight* and *annotated* in this case we are working with *annotated*.

To find the last commit and the tag it is part of type the following in the command line.

```
$git describe
v1.0.0.0
```

This is what you will see if the there are no commits since the last tagging.

In order to find what tag that a commit is grouped with you need to know the commit hash for the commit that is in your production branch.

```
$git describe 1234567
v1.0.0.0-1-g1234567
```

What does all these mean? Well the first part is the tag label. This can be anything but most create a convention for labeling project. The *-1-* is the index of this commit since the tag was created. So if creating the tag is commit 0 then this is the first commit after the branch was tagged. Next is the *g*. This tripped me up for the longest time. The *g* is not part of the hash. It refers to *git*. This is in case you are automating bash scripts and need to know the difference in version control. Last is the commit hash. 

I find it easier to read it right to left, me or a bash script. This is in case you have a crazy convention like *company-project-version1.0.0.0-36-g1234567*. The dashes in the name will through me off on occation.

This has saved me a lot of time in find if a commit is part of a release or not. But you may need to modifiy this if your team/company/organization uses annotated tags for additional infomation.
