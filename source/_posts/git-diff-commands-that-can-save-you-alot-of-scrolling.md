---
title: lala
date: 2022-08-09 19:09:27
tags: [git]
thumbnail: /images/code.jpg
excerpt: 'These git diff commands can save you alot of scrolling through large PR's to find exactly the file or type of file you're looking for. Cheers and happy reading.'
---

hese git diff commands can save you alot of scrolling through large PR's to find exactly the file or type of file you're looking for. Cheers and happy reading.

Suppose you wanna check the diff between two commits but only want the file names :

```javascript
 git diff e79c9cfd5c4a6d6a05c0a6a98a2c02c8b3695c78 a48280889774f5be78cc2817c7c8d541b02a600e --name-only
```


Suppose you wanna check the diff between two commits but only want the file names, but also you wanna exclude the deleted file :

```javascript
  git diff e79c9cfd5c4a6d6a05c0a6a98a2c02c8b3695c78 a48280889774f5be78cc2817c7c8d541b02a600e --name-only --diff-filter=M
```

Suppose you wanna check the diff between two commits but only want the file names, but also you wanna exclude the deleted file and only show the logs for a specific file type :

```javascript
  git diff e79c9cfd5c4a6d6a05c0a6a98a2c02c8b3695c78 a48280889774f5be78cc2817c7c8d541b02a600e --name-only --diff-filter=M -- '*.js'
```

For a slightly more advanced use case where you wanna compare the diff between 2 commits but want to exclude all the commits in between checkout this so thread (HERE)[https://stackoverflow.com/questions/1191282/how-to-see-the-changes-between-two-commits-without-commits-in-between]

Also for checking the actualy contents of the diff i use a plugin called git lens in VS code and it has a compare commits feature which give you a more comprehensive analysis/view then a simple `git diff <COMMIT ID> <COMMIT ID>`.

Hope this article was helpful. Cheers.

