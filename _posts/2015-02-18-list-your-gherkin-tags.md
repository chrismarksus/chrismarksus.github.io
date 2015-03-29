---
layout: post
title: "List your gherkin tags"
date: 2015-02-18 10:17:00
tags: gherkin bash grep
---

Get me a list of all the tags we have in our feature files! he said. So off I go to figure this out and this is what I can up with.

<!--more-->

```
grep -Eroh --exclude-dir=step_definitions --exclude-dir=support "\@[a-Z0-9\._-]*" features/| sort | uniq
```

I use grep to find the tags by RegEx. I use the *r* property to recursively search the folders. The *o* to show only the part of a matching line that matches. Also the *h* to Suppress	the prefixing of file names on output when multiple files are searched. If you don't use the *h* only the file names will be output. And not using the *o* will print out all match on the line and you could miss a tag.

Next I exclude the folders I know I don't need to search like the *step_definitions* and *support*. You may have other folders for test data that you may want to exclude. Then the RegEx to search for the tags. I added the dash and period to find any tag the should be used. Last I targeted the feature folder since I was in my test folder.

Pipe that to a sort and add the unique command and you have a list of tags used in your gherkin features files.

Good Luck!
