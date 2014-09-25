---
layout: post
title: "Saving your file and layout in Vim"
tag: vim, editor
---

You read the article on tabs and splits in Vim and tried it out [see post]({% post_url 2014-09-03-splits-and-tab-a-one-two-punch %}). You setup paths so you can rock the ```:find``` command. You start to get the hang of it then at the end of the day you type ```:qa``` an shut it all down. The next day you open Vim and Ouch!. I have to setup all my tabs and splits and load the files again. <!--more-->Now you just went from feeling that Vim could be great, to thinking it's most useless editor created. My {NAME OF IDE I THINK IS AWSOME HERE} just remembers all this stuff, right!

> This is not available to Vi versions only Vim

Well, Vim remembers everything you do in a buffer somewhere but it doesn't save what you do automaticlly. You have to tell it to save it and how and where. Vim has *:Ex* commands for saving this buffer. It is ```:mksession {path/to/filename}``` or ```:mkv``` Where *{path/to/filename}* is were you want to store the session. There is also ```:mkview {path/to/filename}``` for storing only the information about the current window. You don't need an extention but most use *.vim* and you can name it anything. 

##Views

Views in Vim only store information for the current window. So if you are a tab and split screen pro. then check out sessions. the options that are stored are cursor position, fold information, and window buffer. Also ```:source``` doesn't work for loading views you need to load use ```:loadview {path/to/file}``` or ```:lo``` to load the view.


#### Save a vim view

``` :mkview ~/myview.vim ```

#### Load a vim view after Vim is open

``` :loadview ~/myview.vim ```

#### Auto save a view

Add this to your *.vimrc* to auto save views

```
autocmd BufWinLeave *.* mkview!
autocmd BufWinEnter *.* silent loadview
```

##Sessions

Sessions are like views but in Vim they store more information on buffers, the current working directory, fold in your window, global variables that were set, tabs window position and size. These options are configurable in your *.vimrc*. 


#### Save a vim session

``` :mksession ~/mysession.vim
```

#### Load a vim session after Vim is open

``` :source ~/mysession.vim ```

#### Load a vim session when opening Vim

``` $ vim -S ~/mysession.vim ```

#### How do I find my session options

``` :set ssop?  ````

>By the way, if you want to find out any options in Vim type ```:set {OPTION}?```. The *?* is  

##Should I just use Sessions then?

Session management is enterly up to you. You can save the session in the project folder. You can save a copy with time stamps at different points for workflow history. You can use the same name an copy over it each time reusing the same file. Whatever makes you workflow easier. However that means you are going to have to think about what **is** easier for you. This is where IDE's do the thinking for you, but that is the tradeoff. You can never expand beyond the limitation of the predefined workflow of the IDE. Before I start using Tmux I used both view and session files. Sessions I used for large tasks like adding a feature. View I save when there is some future re-factoring or project I would like to do on a piece of code. Now I save a vim session if I have a complex setup that is relate to my mental oeganization of the task then change tasks. An example is if I an researching how to implement a feature and I get a bug fix the need to be investigated right now.
