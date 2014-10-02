---
layout: post
title: 'Spacing ascii tables in Vim'
category: vim
tags: vim editor selection
---

I open up a feature file that was written in gherkin and there is a number of strings that need to be tested. The formatting of the pipe character ```|``` is not consistent. This isn't a showstopper issue but it would be great if can leverage the power of Vim to format this fast.

<!--more-->

>This is going to combine a number of vim's features and commands so if your new to vim this may be confusing.

Well I was looking for a way to align the pipes on the end without a plugin. I didn't find a way. Yet! But this helped out. I wrote the test so it would *raise* and error if it did not find one of the strings in an array and print the string with the error. I was having trouble finding the message in the sea of 10 to 40 strings that needed tested. By sorting the the messages in the test I was able to find the offending message faster. 

This is not the orginal test of course it is only the an exmaple but it proves my point.

```gherkin
Given that I have a table of data
And That table is not sorted
When I use Vim to sort the table
Then I get a pretty table
  | Can you find the String |
  | Is the string in the right place |
  | By the string in the file |
  | The string to the file |
  | A string |
```
First I start with the longest line. I start macro recording by typing ```qa``` where ```a``` is the registry location where this macro will be stored. Now I set a starting point at the fist character on the line ```0```. This sent the cursor to the fornt of the line. This will be recorded even if I am here to start with. Now type ```f|;``` this will jump to the first pipe *|* anf the ```;``` will repeat the jump. So you land on the last pipe. 

```
  | Is the string in the right place | <-This is at line 32 and character 37
```

When create macros you want to think in term of reset, jump, action, and setup. This means that you want reset your starting point like the first or last character of a line or the next search target. Then you jump to where you want to edit. Last to think about setup for your next move. Some you will jump and do an action I number of times. Sometimes the reset and jump are one action. And sometime you will not need a setup. Thinking in this way has help create macro for may simple but repeatable tasks.

> You want to think in term of reset, jump, action, and setup.

Next look the Vim taskbar in the bottom right there should be 2 number and a word like ```37,93 Top``` (as I type this). If you move around the buffer (Vim speak for the file in memory) you will see this change. It is your line number and the character position of the cursor. Mine is ssaying 38 after the jump to the second pipe. If I use my brain I know that if I jump 37 characters to the right from the start of the line and type a pipe I am at character 38. so 37 is point that i will be deleting from.

> If you have taskbar plugin installed or you have customized your vim taskbar then your line and character counts my be in different locations. See the code or the plugin your documentation for more information.

Next I type ```x``` to delete the pipe followed by typing ```50A<space>```. This add 50 spaces at the end of the line. Pick a crazy number it's ok we will fix it next. Now jump back to the first character by typing ```0``` followed by ```37l``` and this will put at the point where you want to align the pipe at the end of the lines. 

Last type ```vt|x``` this will select the space up to the pipe and delete them. Wow that was a lot work for the brain but here is a payoff. go to any of the lines in file where you need to align the pipes to the longest location and type ```@a``` (again where a is the registry locations). 


```
  | Can you find the String          | 
  | Is the string in the right place | 
  | By the string in the file        | 
  | The string to the file           | 
  | A string                         | 
```

All nice and pretty, there were 50 keystrokes and 5-8 mouse movments. This is the wrist, elbow and shoulder movements in correct posture to get to the next pipe character. 76 keystrokes if you start at the first character of the first line and use only the keyboard. The Vim way is 20 for the macro and 2 to repeat for each line and you have the macro recorded. That is a 50-70% reduction in typing. It doesn't sound like much but it adds up fast. 

> [ex](http://en.wikipedia.org/wiki/Ex_(text_editor)) was the text editor before vi and Vim. It is still present in vi and Vim by typing the *:*

This is what the buffer looks like. To a Vim power user and read this stuff even if it takes some time.

```
0f|;x50A i|037lvt|x
```
But we can do better by throwing the ex mode in the mix. Go to the first line of the content with the pipe. Enter selection mode by typing ```v```. If you don't have line numbers on turn them on now ```:set number``` in the command line. Now type the last line number of the piped content. Now type ```:``` and you will see ```:'<,'>``` appears in in the command line. This is how you tell Vim to use the selected text. then type ```:'<,'>normal @a``` again where ```a``` is the registry location. Hit enter and you will see all of the selected lines with the pipe move align to the right at character 38. Now if you have other tests in the page you can type the range in and use ```normal```. Type ```:{RANGE}normal @a``` where ```{RANGE}``` in the start and the stop line numbers ```:20,30normal @a```. This will apply the macro to line 20 through line 30. 

Now that you have the macro you can large areas of text and format it all it once.
