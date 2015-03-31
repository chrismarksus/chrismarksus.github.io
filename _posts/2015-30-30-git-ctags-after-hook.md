---
layout: post
title: "setup ctag to to run in the git after hook"
date: 2015-30-30 10:00:00
tags: git ctags
---

Ctags make Vim rock! Remebering to index the code base is a pain. But how to do it... a cron job, No, Ahh... git hooks. Perfect!

<!--more-->

After I got ctags working and indexed the files and start jumping around my code base like a bunny on cocaine. I started to get bored with typing ```ctags -R``` in the command all the time. I thought about other ways to do this and then I remembered the git after hook. After some reading the post-commit hook was what I needed. It would run ctags after a cherry-pick or anything that looked like a commit. That way the index is always fresh.

```

#!/bin/sh
#
# Run ctags after a commit

echo ""
echo "Ctags running ==============================="
echo ""

ctags -R .

if (( $? == 0 )); then
    echo "Ctags was successful"
else
    echo "Ctags failed"
fi

echo ""
echo "Ctags complete =============================="
echo ""

```
