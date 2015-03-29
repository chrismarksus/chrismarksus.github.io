---
layout: post
title: Get a list of unused steps from Cucumber
date: 2015-03-20 10:17:00
tags: gherkin cucumber bash grep
---

Keeping your gherkin step definitions clean is a difficult task. But with a cucumber command and a little bash magic you can print a list of the unused steps. This will give you a starting point for your clean up.

<!--more-->

The command to run in the command line is ```cucumber --dry-run -f stepdefs```. This will a second or two and you will dashes print on the screen as it is working. I believe each dash is a file that is read.

Once it is complete you will see a list of steps. If a step is not match in the search you will see the line **'NOT MATCHED BY ANY STEPS'** below the step. This is an unused step in the step definition files. See the example below:

```
/^this step def is used in a gherkin file somewhere$/
/^this step def is not used in a gherkin file at all$/
NOT MATCHED BY ANY STEPS
/^this step def is used in a gherkin file somewhere$/
```

Now I just wanted the list of unused steps so I am going to have to get my grep on. If you pipe the results to this line ```grep -B 1 "NOT MATCHED BY ANY STEPS"```. This will match the line with the string **"NOT MATCHED BY ANY STEPS"** and the ```-A 1``` will also get the one line above the match. This is the unused step not the one below. But using the ```-A``` or ```-B``` property add a separator when it print the results that looks like this ```--```. See below:

```
/^this step def is not used in a gherkin file at all$/
NOT MATCHED BY ANY STEPS
--
```

This can be done in one step but I use two because I build up to what I want and it is easier to chop the action to do different things with the data. I use the ```-v``` to reverse match and exclude the matches I don't want.

```grep -v "NOT MATCHED BY ANY STEPS"```

Then I do the same for the ```--``` dashes in the match results.

```grep -Ev "^\-\-$"```

```
cucumber --dry-run -f stepdefs | grep -A 1 "NOT MATCHED BY ANY STEPS" | grep -v "NOT MATCHED BY ANY STEPS" | grep -Ev "^\-\-$"
```

If you add a ```wc -l``` to the end you can get a count of the steps that are not used. Or if you want to look at the list of step and it is really long add ```less``` instead.
