---
title: A Quick dive into git stash
date: 2020-04-04 21:30:17
tags: [git]
thumbnail: /images/code.jpg
---

To list out all the stashs

```bash
$ git stash list
```

To list out contents of a specific stash

```bash
$ git stash show stash@{0} -p
```

To list out just the name of the files (not the contents)

```bash
$ git stash show stash@{0} --name-only
```


