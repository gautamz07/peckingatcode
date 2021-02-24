---
title: How to get a nested object value using lodash.
date: 2020-11-22 07:57:02
tags: [javascript, lodash]
thumbnail: /images/code.jpg
excerpt: 'Often we are faced with the scenario when a nested value of an obeject needs to be passed into a variable or parameter to an API. something like below...'
widgets:
  -
    position: right
    type: recent_posts
---

Often we are faced with the scenario when a nested value of an obeject needs to be passed into a variable or parameter to an API. something like below:

```javascript
MyObject = {
  a: [ '1' , { a : 'i am inner a' } ]
}
```


and the value can be extracted fairly easily using the dot ot arrow notation like so:

```javascript
const value = MyObject.a[1].a
```

we may also want to check if the index 1 actually exist so added a check would be advisable or your app, webpage could break, so we could simple add a trivial check like below:

```javascript
// A better alternative to the above piece of code 
const value = MyObject.a.length > 0 && MyObject.a[1].a
```

Now a game changer would be if we are using a library like lodash, which extacts the nested value, irrespective of how deeply nested it is and spits out undefined if at any level the value if not to be found. so the code can be condensed to a single like like below:

```javascript
const myObj = {
  a: [ '1' , { a : 'i am inner a' } ]
}

const value = _.get(myObj, 'a[1].a.d')
```

Now instead of undefined, if you'd like a default value, you can set it like so

```
const value = _.get(myObj, 'a[1].a.d')
```

Thats all there is to it !