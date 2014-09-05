---
layout: post
title: "Re-Factoring in Vim without scrolling"
author: Chris Marks
category: vim
tags: refactor code vim editor
---

You open up a file from the source code in your project and scroll through 2000+
lines of code, Ouch! You read the code and start to see patterns of usage and
code that can be grouped together and an object is starting to form in your
mind. You need to start moving code around. So how do you that in an editor that
doesn't have scrollbars?

<!--more-->

I am not saying files should not be 2000+ lines. I don't have a problem with
large files. I do have a problem with a 2000+ line class with 1 method that has
1500 of the lines inside that one method. If the file is organized with objects
or classes that contain code that is focused on a single purpose then that is
good. For me I can use markers, split windows, and tabs the organize what I am
looking at because I am going to need to do that anyways.  Also there is a good
reason to contain all of those objects in one class and that is for organization
and self documentation. By placing a class inside and another class you are
saying either any object that uses this class will need that other variables,
methods, or whatever is in this class or if it is private then nobody is going
to use this but this class. Don't make a dependency if zero to one objects in
your program are using it. If 2 or more need it then yes, make it a dependency.  

>I am assuming that you are working in a language that allows objects or classes
>within objects or classes like JavaScript, ruby, etc... If not, you will want
>to modify some of what I describe by including a new object or class.

If you are luck enough to have a wide screen monitor with your command line open
full screen or a command prompt that is wide enough for 2 80 column screens
side-by-side then this is how I do it. If not you can do the same thing but with
a few extra steps. 

>Before you start turn on line numbers with ```:set number``` if it is not on
>already. You will need it for this.

![open file](/assets/images/posts/large_file_vim_code_start_2014-09-04.png)

Start by splitting the screen in half vertically with ```:vsp``` or ```<ctrl-w>
v```.

![split in half](/assets/images/posts/large_file_vim_vertical_split_2014-09-04.png) 

In one of the halves I split the window horizontally so I have the Vim edit
split up as one half and 2 quarter panels with the same file in each. If you
can't make nested objects or classes then this is the time to start that new
dependency. I may even split it into 3 or 4 panels depending on the number of
method that I am pulling code from at one time.

![](/assets/images/posts/large_file_vim_horizontal_split_2014-09-04.png)

On the 2 quarter panels you can position to code to the method that has code
that you want to pull out an add or combine into a new method. In the other
panel I position the code at the point that I want to add a new method. Now this
is where we get into the command line mode. Command line mode (if you remember
from above) is where you type ```:vsp``` the ```:``` starts command line mode in
ex, vi, and Vim. You will see it at the bottom of the screen. We are going to
use a complex formula to move and copy code from one place to another. I am
going to start with a simple example then I will explain the parts. Let say I
want to create a new method at the top of the file but inside the containing
class at line 2.

Now I want to move a few lines of code from line 12 to 17 into that method and
return a value to that method I cut code. How do you move the code without
jumping around?

![move the code](/assets/images/posts/large_file_vim_move_code_2014-09-04.png)

``` :12,17m 2 ```

or

``` :12,17move 2 ```

![code is moved](/assets/images/posts/large_file_vim_code_moved_2014-09-04.png)

Translated this is asking the editor to *move* lines 12 to 17 to line 2. You see
the code appear in the method and disappear from the where it was before. Now if
you didn't move your cursor and it is still around line 12 then you can start to
add the method call here.

![final re-factor](/assets/images/posts/large_file_vim_final_code_2014-09-04.png)

Now let's back up and say that instead of moving the code, which is deleting it
one place and pasting it in another, that we want the keep the code in place
and copy that code to the new method. A good reason for this is if you have unit
test coverage of the code but you want to pull code into a different object and
method and unit the new one first. After the test is passing then you delete the
old code and replace it with the new class and method call. Then the new test
and the old test should pass. If not the new method is not working the way it
should and you wrote the test incorrectly. The Vim command to copy lines is
```t``` or ```copy```. It's not ```c``` because that stands for *change*.

``` :12,17t 2 ```

or

``` :12,17copy 2 ```

The formula for this is ```:[range]move {address}``` or ```:[range]copy
{address}```. The [range] can be a number or a start and end number. It can be a
symbol like **.** (for current line) or **$** (for end of the file). It can also
be '<,'> for the beginning and end of the last visual selection.  The
*{address}* is where you want to move or copy the lines to in the file.

```
:30,40m . - move lines 30 to 40 to the current line
:30,40t $ - copy lines 30 to 40 to the end of the file
:'<,'>m 50 - move last visual selection of lines to line 50
```

You can also add with a + or - in the *[range]* and *{address}* so ```:12,12+5m
2``` is the same as ```:12,17m 2```.

>This seems like a lot of work at first and it is. But once you build the muscle
memory to the point that you don't think about it then it's pretty cool. The
first time I did I didn't realize it until I scrolled through my history.

Now wash, rinse, and repeat. Re-factor the code until you like it or it works at
least. This is just one the ways I use the tools together to complete a writing
or coding task.
