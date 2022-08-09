---
title: Reassiging arguments does't work in es6 and here's why
tags: [javascript, nodejs]
thumbnail: /images/code.jpg
excerpt: 'Lets run though a quick counter intuitive javascript behaviour you may run into. suppose you have the following function...'
---

Lets run though a quick counter intuitive javascript behaviour you may run into. suppose you have the following function :

```javascript
function validateForm(name, phone, email) {
   arguments[0] = "vladimerz"
   console.log(`${name} ${arguments[0]}`)
}

validateForm('nanco') // output :- vladimerz vladimerz
```

But now lets add a default argument to this function like so :-

```javascript
function validateForm(name, phone = null, email) {
   arguments[0] = "vladimerz"
   console.log(`${name} ${arguments[0]}`)
}

validateForm('nanco') // output :- nanco vladimerz
```

The outcome is different , and thats because in javacsript when using ES6 syntax and also "strict mode" you don't get a mapped arguments array. The following is an excerp from the ES6 standardization doc :-

>
>A mapped argument object is only provided for non-strict functions that don't have a rest parameter, any >parameter default value initializers, or any destructured parameters.
>

Cheers.