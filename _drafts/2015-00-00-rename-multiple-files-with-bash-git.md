---
layout: post
title: "Rename multiple files with bash and git mv"
date: 2015-00-00 10:00:00
tags: bash git
---

I did a search for the different file extensions in a project to see what I was dealing with and I see a number of problems. One is that there are misspelled or mis-named extensions. 

<!--more-->

Here is an example filename.foo-bar and filename.foo_bar. Now this drives me crazy so I have to do something but the project is in git so I want to use ```git mv``` instead of bash's ```mv``` so git knows that the file is being renamed and not deleted and a new file added.

So this is what I found on the web. 

```
find . -name '*foo-bar' -exec sh -c 'file={}; mv $file ${file/foo-bar/foo_bar}' \;
```
I change ```mv``` to ```git mv``` and it worked fine.

I will be honest in that I don't understand some of this but I will explain what I do know and point out the part I don't understand.

Find any file with "foo-bar at the end of the path and file name. Then exec the following.

```
find . -name '*foo-bar' -exec
```

Create a variable to store the output.

```
file={};
```

Then execute a ```git mv``` on each file and move what is in ```$file```. Now the next bit will print what is in ```$file``` but the ```${file/foo-bar/foo_bar}``` part is replacing the *foo-bar* with *foo_bar* in ```$file``` before it prints it.

```
git mv $file ${file/foo-bar/foo_bar}
```

This is the part I don't understand and can't find anything on the web yet. I am guessing that this is executing a shell command.

```
sh -c ''
```

Rename a file extension:

```
find . -name '*jpeg' -exec sh -c 'file={}; git mv $file ${file/jpeg/jpg}' \;
```

And if you want to delete a bunch of files you can use ```git rm``` to remove them from git and the project.

```
find . -name '*old-stuff-to-find*' -exec sh -c 'file={}; git rm $file' \;
```

Enjoy!
