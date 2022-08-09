---
title: Does require create new instance of module
date: 2020-11-22 07:57:02
tags: [javascript, nodejs]
thumbnail: /images/code.jpg
excerpt: 'Often we are faced with the scenario when a nested value of an obeject needs to be passed into a variable or parameter to an API. something like below...'
---

Ever wondered if the require stateent in nodejs creates a new instance of a module ? or does it just cache the imported module ? Lets take a quick peek in this article.

Suppose you have the following 3 modules.

```javascript
// module-shared.js

let GLOBAL_STR = 'LOGGER :-'

const logger = (str) => {
  GLOBAL_STR += ' ' + str
  console.log(GLOBAL_STR)
}

module.exports = logger
```

```javascript
// module-1.js

const logger = require('./module-shared')

const useLogger = () => {
  logger('module 1')
}

module.exports = useLogger
```

```javascript
// module-2.js

const logger = require('./module-shared')

const useLogger = () => {
  logger('module 2')
}

module.exports = useLogger
```

And then you required() both module-1.js and module-2.js inside a index.js like so.

```javascript
const useLogger1 = require('./module-1')
const useLogger2 = require('./module-2')

useLogger1()
useLogger2()
```

What you get as the output is 

```javascript
LOGGER :- module 1
LOGGER :- module 1 module 2

// Instead of 
LOGGER :- module 1
LOGGER :- module 2
```

This is because require cache's modules. Now there is a way to get around this, but i'll explain that in a later article. The takeaway here is require does't create by itself a new instance of a module and caches a module once imported for subsequent imports of the same module.

Hope this was educational. Cheers.

***P.S. Other good articles on the subject***
- [How to create a singleton in nodejs](https://iaincollins.medium.com/how-not-to-create-a-singleton-in-node-js-bd7fde5361f5)
