---
layout: post
title: 'Sorting text in Vim'
category: editor
tags: vim 
---

It's that gherkin feature file again. After running the test a number of times an tring to read the string that failed you realize that it would make it easier if the strings where sorted. But you need a fast way to do it. Manually sorting text is painful and not the good kind that teaches you not to touch hot stoves. It's the "Why do i keep hitting myself in the head with a hammer?" kind of pain, and that's stupid and painful.

<!--more-->

I discovered this while looking for a for a way to clean up a table of strings in a gherkin feature file. It's not what I was looking for but it did help with another issue. When I read what sort did in the documentation I realized I needed to know this and started playing.

>If you don't have line numbers turned on do that now with ```:set number```.

Let imagine that the strings with the pipes are on lines 17-21.

```gherkin
Given that I have a table of data
And That table is not sorted
When I use Vim to sort the table
Then I get a pretty table   
  | Can you find the String          |
  | The string to the file           |
  | By the string in the file        |
  | A string                         |
  | Is the string in the right place |
```

Type in a range ```:{range}sort``` for example ```:17,21sort``` or use the visual line selection tool by using ```V``` then type ```:``` and the selection markers will appear in the command line ```:'<,'>``` then type sort ```:'<,'>sort``` followed by enter.

Now you should all of the lines sort like the examples below,

```gherkin
Given that I have a table of data
And That table is not sorted
When I use Vim to sort the table
Then I get a pretty table
  | A string                         |
  | By the string in the file        |
  | Can you find the String          |
  | Is the string in the right place |
  | The string to the file           |
```

Add a *!* to the end of the ```sort``` to reverse the order ```:{range}sort!```

```gherkin
Given that I have a table of data
And That table is not sorted
When I use Vim to sort the table
Then I get a pretty table
  | The string to the file           |
  | Is the string in the right place |
  | Can you find the String          |
  | By the string in the file        |
  | A string                         |
```

The *u* property sorts and it removes duplicate lines of data. This helped fix a test that was failing because I noticed that there a was and extra repeating string. This sorted the table and removed the line that was failing the test.

You are also able to sort by numbers(n) and months(-M).

Good luck!
