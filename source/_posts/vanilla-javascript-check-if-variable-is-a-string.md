---
title: Vanilla javascript check if variable is a string
widgets:
  - position: left
    type: recent_posts
date: 2021-07-11 00:11:27
tags: [javascript]
thumbnail: /images/code.jpg
---

you can use the typeof operator like below

```javascript
let foo = 'Hello Janco !'
console.log(typeof foo) // will log 'string' 
```

For a more bullet proof check incase your using object-wrapped strings, you can do a double check like below

```javascript
if(typeof foo === 'string' && foo instanceof String) {
  // business code goes here !
}
```

