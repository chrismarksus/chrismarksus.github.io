---
layout: post
title:  "Tabs and splits a one, two punch"
date:   2014-09-03 22:45:51
categories: vim 
tags: vim
---

I am analyzing my current work flow. Some co-worker of mine asked if I can show them how I use vim and tmux. I thought that this will give me a good reason the try blogging again and play with jekyll a little more.

<!--more-->

## Splitting windows in Vim

Splits in Vim are a way to divide up the window into different areas. These sub-windows and display any buffer available to Vim. 

```
:sp {filename} open a file with horizontal split
:vsp {filename} open a file with vertical split
```

If you omit the filename it will split the window with the current file.

I just use these to split windows on the fly.

```
<ctrl-w> v vertical split window
<ctrl-w> s horizontal split window
```

These are what I use to jump around in the tabbed window.

```
<ctrl-w> ww
<ctrl-w> h or arrow left
<ctrl-w> j or arrow down
<ctrl-w> k or arrow up
<ctrl-w> l or arrow right
<ctrl-w> r rotate split (this only works on verticals or horizontals not combinations)
<ctrl-w> q close a tab

```

## Tabs in Vim
Tabs in Vim are not like tabs in other programs. At least you should not think of them the same way. The reason for this is that can do a few things with Vim's tabs that most other programs don't. The tabs in Vim work more like workspaces on the OSX and linux where you can divide up work spaces. You can treat them as just tabs and you starting out doing that make getting start simpler. 

###Opening tab in Vim

```
:newtab           open a new empty tab you can save this using :w {path/to/filename.ext} execute command
:Tex              Use file explorer and open in a new tab (See file explorer)
:tabfind {file}   open a new tab with filename given, searching the 'path' to find it
```

I will use this once in a while but rarely

```
:tabclose {n}     close {n} tab position
```

I don't use these with the way I work. I don't find much use for them.

```
:tabedit {file}   edit specified file in a new tab
:tabonly          close all other tabs (show only the current tab)
```

###Navigating tabs in Vim
I use ```gt``` to cycle through the tabs 98% of the time. 

```
gt            go to next tab
```

I will use these in rare cases but not in my day to day usage. I rarely have more then 5 tabs open at any one time and using ```gT``` or ```{n}gt``` requires the mental overhead of remembering where you are in the tab order. So I trade extra keystrokes for brain power. Now I may have as many as 10 tab open with split windows because I stopped and I started completely different tasks and I plan to get back to the task later. 

```
gT            go to previous tab
{n}gt         go to tab in position {n} 
```

I never use these to move around. The normal mode motions are faster and easier to remember.

```
:tabs         list all tabs including their displayed windows
:tabm 0       move current tab to first
:tabm         move current tab to last
:tabm {n}     move current tab to position {n}

:tabn         go to next tab
:tabp         go to previous tab
:tabfirst     go to first tab
:tablast      go to last tab
```

I because I organize tab the way I group them in my head I rarely need to reorder tabs. When the tabs are not working for me usually my mental organization is messed up as well so maintaining the buffers in of little value to me. So I close and reopen vi then rebuild my contexts. I can do this in about 30 seconds or less depending on the number of files.  

> On a side note most motions in Vim have 2-3 versions, one for normal mode, execute mode, and one for insert mode. In insert mode the keyboard command is proceeded by ```<crtl-w>``` (unless you configured it differently). So ```:vsp``` in insert mode is ```<ctrl-w> v``` both of these vertical split the window.

###Other ways I add files to tabs and split windows
I use the ```:ls``` execute command to open a quick list of the buffers and jump to the buffer by using ```:b{n}``` where {n} is the number in the list.

Unimpaired.vim plugin is a plugin I use a lot, in fact, I don't even know why it's a plugin at all. Vim should work this way. It doesn't add any new functioniality it just adds motions for the navigating the buffers ```[b``` and ```]b```. I create a tab and split the and cycle through the buffers in each panel until I create the context of file I have in my head.

I also use a fuzzyfinder in Vim. A fuzzyfinder helps you find files by typing any part of the path and file name that you rememeber. So If I type 'patomyfile' it will list "path/to/myfile.js" and parent/to/my/child_file.js" Then you can select the one that you want. The plugin I use is called Ctrl-p.

More about installing plugins and fuzzyfinders.

## Combining splits and tabs to organize mental contexts
I use Vim's tabs to organize or group modes of thought or mental contexts. I separate tasks according to the files I need to work on by starting a tab then splitting the window and adding more files. An example of this would be if I am working on a JavaScript task and I the open the source code and then split the tab in half horizontally and open the unit test in the other. As I work on the test and code I may temporarily split one or both windows again. I do this so I can look at 2 places in the code at once instead of using markers to jump around the page. I use markers for a different purpose but that is a later post. 

> If you are using gui a version of Vim (like gVim) these are not the tab at the top of the program. Most of those open an instance of vim in a tab and you can use Vim tabs with in them. Then they remap the keyboard commands so the looks like there the same thing. Some you can create tabs within tabs. You can do the same thing with a terminal multi-plexer like TMUX or Screens. This can be confusing and it is why some hard core Vim uses tell people to use command line Vim first.

Right now I have only worked on the default window/tab. Now that I have edited the code and I need to work on the gherkin tests. Instead of closing the buffer or replacing them I will use ```:tabfind``` or ```:Tex``` or ```:newtab``` then ```:Ex``` to open a file in a new tab then I split the window and jump to the step definition in one the steps by using ```<ctrl-]>``` See vim_move_around_files.md. Now I can see and edit the step and the step definition in one view. Now if I have to edit a step I may need to the edit it in a number of files. At that point I can could open more split windows and open the files that I need to edit in each split or I could add the files to the args list and do an ```:argdo``` command on all the files. 

Mentally I may organize these into 2 tabs. One tab edits/re-factor the step and one feature file that uses the step. And another tab containing all the other files that use the step. Once I have the step written and working the way I like I switch context just by typing ```gt```.

Now lets say I need to reconcile a class selector path in the step definition. Again instead destroying this thought process I can open a new tab and split it and open have the JavaScript and the gherkin step definition open side by side. Now if you make a change that requires you to edit the gherkin or unit test. You already have those tabs grouped and ready to go. You don't need to phyically change contexts nor do you have to mentally change contexts. It's right there in a tab you ```gt``` or ```gT``` to it and start working.

In the middle of this is were a co-worker or boss appears and starts asking you questions. Instead completely breaking your context you open a tab with ```:Tex``` get the file that you need to start looking at to answer the question and start splitting the window from there. When you are done you can return to your previous tab and pick your context quicker because the arrangement of the tab and split windows is how you left it.

>In most cases this is where I get 10+ tabs in vim I have a task that needs 3 to 5 tab and I have questions form other workers that use 5-8 tabs. I don't destroy them because they will come back and ask more questions. If this goes on for more then a day I will use ```mksession {filename}``` to save all of it so I can return later.

Now let's say you open a huge file 2000+ lines of code and see this needs re factored into smaller objects before you start your task. You leave the file in your current tab of split window context then open a new tab with the file and split the window with the same file in all of the windows. You use one large split to look for code to cut and paste and then position the other window where you want to start the new object. This becomes a re-factoring context and when this work is done you jump back to the tab that you left and start implementation of the task. 

>An interesting side effect of this is that the work that is done in the tabs can make great commits in git, Well organized and focused and easier to review.

## The real difference with Vim
This were Vim starts to shine over IDEs. Vim can be made to do anything an IDE can do (that is, if you know enough about Vim). IDEs Improve your work flow by restricting your choices not adding choices or functionality. Arguments about this IDE vs that IDE are really about preferences in the freedom and restrictions an IDE has verses the what the user knows or wants to know and doesn't know. Or put another way. I know how to do this (or want to know) so get me freedom here verse I don't know this or like this so restrict it into a nice little feature or abstraction. Comparing Vim to any IDE though is like like comparing the toolbox of a furniture maker to the toolbox of someone that assembles pre made furniture. Both have quality tools and may have the same tools but the furniture maker has to know more about his tools and that give him the freedom to do more with those tools. Include making new tools to make new furniture. 
