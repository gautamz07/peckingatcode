---
title: Babel basic usage guide plus usage with webpack
date: 2021-08-21 18:31:51
tags: [babel,javascript,ecmascript-6,compiler]
thumbnail: /images/code-2.jpg
---

Just for demostraction purpose lets play around with babel a little and over time i'll expand on this article on how to used babel alongside webpack. For starters lets create a folder structure that resembles the below :-
<!-- more -->

```javascipt
- src
  - index.js
- package.json
```

Let the contents of index.js be as follows.

``` javascript
const fruits = ['apples', 'oranges', 'mangos']
const fruitcopy = [...fruits]
const addition = (a,b) => a + b
```

You should have a package.json folder by default with no dependencies when you run `npm init` inside the folder ypu're runnint this project in. Run the below command to add a couple of dev dependencies.

```javascript
yarn add @babel/cli @babel/core --dev
```

It is recommended you add these dependencies locally to your project instead of have it globally installed as that makes your project more flexible (you can have different versions based on project) and portable(dependencies can be installed based on package.json).Now you can add the following command inside your package.json file.

```javascript
"scripts": {
  "build": "babel src -d lib"
},
```

Now when you run `yarn build` in your root folder, you will see a lib directory created but the contents are not quite compiled to ES-5 syntax, which is basically what we want to do with babel. For that to happen we will have to install a present and create a babel.config.json file.

```javascript
// Contents of .babel.config.json file in rootdirectory
yarn add @babel/preset-env --dev
```

Also install the present

```javascript
{
  "presets": ["@babel/preset-env"]
}
```

At this point if you run `yarn build` you should see a index.js file inside the lib directory with following contents :-

```javacsript
"use strict";

var fruits = ['apples', 'oranges', 'mangos'];
var fruitcopy = [].concat(fruits);

var addition = function addition(a, b) {
  return a + b;
};
```

Your final directory shoudl look something like below.

```javascipt
- src
  - index.js
- package.json
- babel.config.json
- lib
  - index.js
```

Voila ! we're done and with a no frills setup we are now able to use babel to trasform code into ES-5 compatable executable code, thanks to babel and `@babel/preset-env`.

In larger projects hoever its unlikely we would use babel as a standalone and rather use with alongside a task runner (gulp, grunt) or bundler (eg. webpack). Lets have a look into that in the next series. 

Also on a sidenote the `@babel/preset-env` has multile [options](https://babeljs.io/docs/en/babel-preset-env) of its own that you can explore and set so as to reduce your bundle size further.

Hope this helped you understand the mystery of babel partially. Cheers !

