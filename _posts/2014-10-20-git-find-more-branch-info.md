---
layout: post
title: Find out more info on your branches
tags: git
---

*What branch was I tracking in the first place?* As my hands reach up, collect hands full of hair on the sides of my head. After I submitted a code change and it was not showing up in the branch I expected it to be in. I realized I must have delivered it too a different branch. My change had nowhere else to go in git.

<!--more-->

After the initial panic subsided I needed a way, an easy way, to find out what my local branches were tracking. After diving into the interweb and git documentation I found this little gem. 

```
$ git branch -vv
```

It reports the following table of information in your terminal.

```
* cssfix   8732h5j Fix the background of post 
  maint    3928131 [origin/maint: behind 2] Release 3.0.2
  master   399de12 [origin/master: ahead 1] Add new icon images
  slowfix  4a5c38b [origin/production: ahead 1, behind 3] Improve JavaScript DOM interaction
```

The \* of course is the branch that you have currently checked out. The *branch name* is next, then the *commit short hash* after the branch name. Now if this branch is *not* tracking a remote branch then you will see a short commit message. If the branch is tracking a remote then you will see *[]* bracket before the commit message. Inside the brackets will be the branch you are tracking. The number of commits the branch is behind or the number of commit the branch is ahead. If one is at *zero* then it doesn't print the stat. 

This has been helpful to quickly find out what a branch is tracking. If you are into renaming branches or leaving sketch code lay around and revisiting it later then this will help you get your git bearings. 

You can also report on all branches by adding the ```-a``` or remote branches only by adding the ```-r```. 


```
$ git branch -avv
  cssfix                   8732h5j Fix the background of post 
  maint                    3928131 [origin/maint: behind 2] Release 3.0.2
* master                   399de12 [origin/master: ahead 1] Add new icon images
  slowfix                  4a5c38b [origin/production: ahead 1, behind 3] Improve javascript DOM interaction
  remote/origin/maint      8923hs9 Revert padding that broke layout 
  remote/origin/master     d83234h Correct padding before release
  remote/origin/production k29d679 Release 3.0.1
```

I hope this helps out, Bye.
