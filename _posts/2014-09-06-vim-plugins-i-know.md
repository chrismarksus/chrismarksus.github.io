---
layout: post
title: "Vim Plugins I know or use"
tag: vim editor plugins
---

I am not quick to add plugins to Vim. I am talking about a my personal vim setup not something like januas. Plugins should add to my workflow and not burden me in any way. In reading and working with people I find some unhealthy views about Vim plugins. Here are some viewpoints:

<!--more-->

>You just need Vim and bash. If you can't do it with that your a bad programmer, and that includes those IDE people, gosh darnit! Even emacs uses I can respect but those IDE people.

I completely agree that learning the bash/Vim way is a better way in the long run. You learn more about the technologies that all the other ones are built on. That will always payback the time effort that you spent. But that is not always the case. There are plugins the re-arrange key commands or motions, add motions to existing functionality, or re-arranges Vim into a more productive workflow for and individual. But in-order to make the most of those plugin and know what to install you need to study how you write code. One of the thing that surprised me when I start to use Vim was how little I type and how dependent on the mouse I was. IDEs remove the need to learn how you write code by providing a pre-packaged workflow to learn. People that create Vim setups like janus are doing the same thing. There packaging what they learned about how they write code and how they improved it by customizing the .vimrc, making shortcuts, make scripts that automate repetitive action they do when writing code.

>The problem with Vim is that have about know about and know how to configure all of the plugins to make it useful.

Vim has everything you will ever need to editor code and can do it just as well as any other IDE or text editor. Yes you have to learn and know more about how your tools work. That in turn will motivate you to learn how tool configure your tools. That will lead to improved workflow and encourage you to learn more. If you augment Vim with bash commands like grep then you will in time become a Unix power house able to be deployed in any environment that has a *nix terminal. 

>Vim is not a good editor because you need a whole bunch of plugins to make it work.

What most people don't understand about vim plugins is that most of the plugins are just one persons repetitive actions and/or configurations. Some of these are .vimrc configurations. Most are combinations of key commands that someone is using over and over again an they takes the time wrap it up as a plugin to share with others that do the same tasks or have the same problems. So Vim already does what these plugins do in the first place.

>Wow, you sound like you really hate plugins

No I don't I just see them for what there are and use that to my advantage.

##How I pick a plugin for Vim

First there is really only one motivation that drives people to look at a plugin. Not just in Vim but any editor really.

>It would be great if *MY EDITOR* did *THIS* and/or *THAT*.

At this point people start searching the web for a plugin, but this reaction is
based in one fatal assumption. That is that your editor doesn't *do* what it is
you want it to *do* already. Expert Vim users are like chefs that don't need
recipes anymore. They so much about the kitchen tool and ingredients that they
can make up recipe on the fly. But to do that you need knowledge. We don't like
to mental say things to ourselves like "I am ignorant of this in my editor". Or
we get complacent with what little we know about our editor and just try to get by with just that.

What I do is ask myself how might I do it with what I know then I will look to fill in the gaps that I need to fill to make it work. This forces me to learn and grow. This is how I learn to pipe output in bash to other command. This was and *AH-HA* moment for me. Bash seemed kind of point until I learn how to combine commands. This added a new dimension to the knowledge I already had in my head about bash commands.

##Why it maybe time to stop using a plugin

I started with the Janus plugin arrange when I started to get the hang of Vim after the seventh time of tring. It has a lot of great plugins that made learning Vim less taxing. But over time I started to notice that as I learn more about how to do things in Vim that I start to rely more on building actions with Vim commands and I start to forget about the plugin commands. Over time I stopped use the plugins because I got tried of looking up the commands. Noticing this change my view of plugins. 

##Plugins I know

###Use a good packet manager

Packet managers make Vim plugins much easier to handle. All of these are pretty good. I use Pathogen. There are differeces between them but I find that I just don't care about what each one does better. I just want to download and manage my plugins. I don't want a feature rich manager. I don't even want to know it's there. To me that is the sign of great plugin/packet manager.

[Neobundle](https://github.com/Shougo/neobundle.vim)
[Vundle](https://github.com/gmarik/vundle)
[Pathogen](https://github.com/tpope/vim-pathogen)

###vim-trailing-whitespace

Highlights white-space like tabs and spaces at the end of lines. It's a little thing but it makes a big difference.

###vim-multiple-cursors

This is a neat little plugin. It doesn't do much but what it does is really cool. It allow you to pick instances of the same word like a varaible and change all of them at the same time. But I usually ```<shift> * cw {NEWWORD}``` then ```n``` to the next and use ```.``` or ```n```. 

###Syntastic

Syntax hightlight and that's all. It does a get job and if it can even clue you into error that occur that may not be syntax related. like a comment that will cause a parser to throw an error.

###Unimpaired

Make navigating the buffer lists easy ```[b``` and ```]b``` to move back and forth through the buffer list. It does more but that is all I care about and use.
This is a great example of a plugin that improves Vim. I know how to do this without the plugin but this plugin re-organizes the keyboard commands and reduces the key strokes.

###Ctrl-P

A fuzzyfinder like (Command-T) lets you type what you remember about a file name and directory structure and shows you matches.

###Fugitive

It is worth downloading this for the ```:Gblame``` alone. The rest it I can do without. I don't like having the remember multiple version of the same command. ```:Gstatus``` and ```$git status```. The benifit of not having to leave Vim verses the ease of switching windows in a Tmux session and using real git command is in the negatives.  

###Sparkup

This plugin lets you use a css selector like query and expands it into html. I found this helpful when I wrote a lot html templates but now that I javascript and other non-html templating I doesn't need it.

###Surround

Auto-complete for closures of any kind ,```(```, ```[```, ```{```, and ```<html>```. *I don't use it*.

###SnipMate

This is like micro templates for code you type def in a ruby file. Hit ```tab``` and ```def function_name(arguments){ // code here }``` appears nicely formatted and the function_name is selected you start type and place the name then tab start typeing and replace the arguments. 

###tCommenter or NERDCommenter

These are plugins that help comment out code. These are great examples of why
you should do some research to find out if Vim can already do something first. I
always had trouble configure these to work with other plugins. Then I
discoveried the beneifits of visual block selections in Vim and started using
that to comment out code. Yes, does do the automatic commenting better but I
find the versitility of know how the visual block selection work. Hey! That
sound like good [post]({% post_url 2014-09-12-commenting-out-code-with-visual-block-in-vim %}).   
