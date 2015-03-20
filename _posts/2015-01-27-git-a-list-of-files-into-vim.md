---
layout: post
title: "Git a list of files into Vim"
date: 2015-01-27 22:45:51
tags: vim git java xml bash pom
---

You have to merge a branch down to a feature branch. Maybe it's the master branch. Oh! it's using maven and java so you have these xml files the contain the dependencies in files called pom's. They always needing to be fixed/changed. Delete a snapshot here and change a number there, you get the idea. Wouldn't it be great if you could load the unstaged git modified files from a merge into Vim. Well, you can!

<!--more-->

I have to do this and I hate it. Changing files like these pom's is a real pain so I was trying to find an easier way to do it. I started to play with this command ```ls-files``` and when I combined it with Vim and so bash tricks I found I could do some pretty cool updates.

After merging a branch if you use the ```git ls-files --modified``` property you get a list of updated files that the merge changed.

```
git ls-files --modified
```

if you toss in a pipe to a unique sort then the you get a pretty list of those files.
```
git ls-files --modified | sort -u
```

If you wrap that in a ```$()``` that dump the results into vi then you with open all the files in vi.

```
vi $(git ls-files --modified | sort -u)
```

Now record a macro ```ctrl-q``` then pick a buffer to record it under ```a-z``` and when you are done ```q```. Now you can apply the macro to all of the open files using ```:argdo```. In the sample below I used ```a``` as the buffer to record.

```
:argdo execute 'normal! @a' | update
```

Hope this helps, Thanks.
