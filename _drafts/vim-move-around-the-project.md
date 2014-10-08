---
layout: post
title: "Setting up VIM to find your files by name"
tags: vim
---

<!--more-->

## Modify your .vimrc
You will need to add the file extensions, locations, and things to ignore to your *.vimrc* file.

Add the file extension that you work with

```shell
set suffixesadd+='.xml'
set suffixesadd+='.js'
set suffixesadd+='.jsf'
set suffixesadd+='.jsp'
set suffixesadd+='.html'
set suffixesadd+='.soy'
set suffixesadd+='.rb'
set suffixesadd+='.feature'
set suffixesadd+='.java'
set suffixesadd+='.class'
set suffixesadd+='.properties'
```

Add path to places I want to look for code

```shell
set path+='/path/to/your/project/javascript/**'
set path+='/path/to/your/project/custom/code/**'
set path+='/path/to/custom/library/code/**'
set path+='/path/to/your/project/\.lib/dojo-release-1\.7\.3-src/**'
set path+='/path/to/your/project/tests/**'
```

Add files and folder in those location I want to ignore

```shell
set wildignore+='*/test_assest/*'
set wildignore+='*/target/*'
set wildignore+='*/\.tmp/*'
```

##Open Vim and get started
If Vim is already open you will need to source the .vimrc or close and reopen Vim. to source the *.vimrc* use the :Ex command ```:source path/to/.vimrc``` or ```:so path/to/.vimrc```

###Using the :find command
To find a file that you know the name of just use the ```:find``` command. Type ```:``` then ```find```. Then type the *file name*. Then press the enter key.

![open find file](open_find_file.png)

If you spelled it right (with capitals) then you should see a file with the same name. But this may not be the file I want. there may be files with the same name that are in a directory structure that places it ahead of the one I am looking for. Well ```:find``` returns an array of all the files it finds if there is more than one file with the same name. You can add a number in front of ```:2find``` to get the next file. 

![find file with same name](find_file_with_same_name.png)

This is the file I am looking for, unfortunately there is no quick list for ```:find``` results. If a result is not successful I type ```:``` then hit the up arrow then add a number before the *find* command. 

![correct file found](correct_file_found.png)

###Opening in a new tab
To open a file in a new tab use ```:tabfind``` or ```:tabf```. The same rules about the return array still apply so you can use ```:3tabfind```. 

###Jump to a dependancy
In Vim anything that looks like a folder structure for example *js/amd/file* or *org.my.java.classes*. Vim will look at the ```path``` property in the *.vimrc* or if you adding it to the path from the command line.

To jump to a file in Vim place the cursor over the object in the path that you want to jump too. In this case the name of the JavaScript object then use the motion ```gf``` in normal mode or ```<Ctrl-w>f``` in insert mode.

![open jump to file](open_jump_to_file.png)

If all is setup correctly then you see the file. Now just like the ```:find``` command an array is returned so if there is more than one file name that matches an array will be returned. So you can add a number before the motion ```2gf``` to jump to the next one.

![jump to js dependancy](jump_to_js_dependancy.png)

In Vim there is what is referred to as a jump list I will go into there here in detail but there are 2 useful motions to remember ```<ctrl> o``` and ```<ctrl> i``` With these you can move back and forth through the files that you open with ```:find``` and ```gf```.

>You may have started to notice a repetitive pattern to these commands ```2gf``` and ```:2find``` and ```:2tabf'''. Anything in Vim that returns a list you can add a number to the front to jump to a different point in the list {number}motion.

##Discoveries

###Set path escaping
- When adding paths with characters like periods ```path/version_1.3.5``` in the name add backslashes ```\``` to escape the character ```path/version_1\.3\.5```.

###Project structure and vim
Jumping to dojo source code can be a problem in some cases. Jumping to the dom.js file will not work because there is a empty dom/ folder and a dom.js file. What Vim does is open the file explorer in that dom/ folder. But since it changed form a file jump to the explorer you do not get an array. I have not found a way to deal with this issue yet but I have found a workaround.

![jump to dojo dom](jump_to_dojo_dom.png)

And now you are in Netrw. 

![explorer](explorer.png)

Also trying to jump to a dojo dependency with a ```dojo/require!``` will not work either because require! is not a folder. Example ```dojo/require!project/template/Filename```.

####How I work around the issue
In the case of the dependencies. You know the name of the file so you can easily use ```:find```.

