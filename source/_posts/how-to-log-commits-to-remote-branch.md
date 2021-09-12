---
title: How to log commits to remote branch
date: 2021-03-14 20:47:06
tags: [git, productivity]
thumbnail: /images/code-git.jpg
excerpt: 'Do you have to often switch between the browser and your editor to check the latest commits to a remote branch ?'
---

Do you have to often switch between the browser and your editor to check the latest commits to a remote branch, to check if any new commits have been added by a developer ? well in that case you can use a combination of commands that would log the latest commits to your console.

```javascript
git fetch origin dev-branch
```

and then just log it like below.

```javascript
git log --pretty=oneline dev-branch
```

Note for self :- Look up how to alias current branch instead of typing it out.
