---
title: Git stash staged files only
date: 2020-11-15 08:04:10
tags: [git, github]
thumbnail: /images/code.jpg
---

If you've been using git for a while , chances are you've come across the scenario where you need to stash not all your changes , but just the changes you've staged. In this scenario you can simply double stash in 2 simple steps.


```bash
$ git stash --keep-index
```

the above saves all your changes in a stash but keeps the staging changes in the working directory.

then you can just 

```bash
$ git stash push -m 'staging changes only'
```

Now you have your stash with staging changes only.