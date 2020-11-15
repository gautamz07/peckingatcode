---
title: Identify content type of API response
date: 2020-11-10 07:57:02
tags: [javascript, fetch]
thumbnail: /images/code.jpg
---

You can set 

```javascript
response.headers.get("Content-Type")
```

And then use

```javascript
.get(param)
```

Source :- [stack overflow](https://stackoverflow.com/a/64746175/4381665)