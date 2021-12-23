---
title: A better pattern then ad-hoc try catch
widgets:
  - position: left
    type: recent_posts
date: 2021-12-23 12:11:05
thumbnail: /images/code.jpg
tags: [nodejs, javascript, error-handling, sequilizejs]
---

I was recently working on some controller code in nodejs which has `try...catch` as the catch all mechanism for errors. something like the below :

<!-- more -->

```javascript
const isUserLoggedIn = async (req, res, next) => {
  const { email, password } = req.body;

  if (!email || !password) {
    // 400 - missing data
    return res.status(400).json({ error: true });
  }

  try {
    
    /*
      - Typical code for comparing password hash.
      - Check if user exists.
    */

    await access_tokens.update_user(req.token, USER_DATA);
    await clearRedis(cannonicalName, req.token);

    await sendPromotionalEmailer();

    return res.status(200).json({ success: true });
  } catch (error) {
    logger.log({ message: error.message, level: 'error' });
    return res.status(500).send(error.message);
  }
};
```

As you can see there are multiple places where there can be a failure case.

`update_user`, `clearRedis` or `sendPromotionalEmailer` any of these function calls can throw an error and the control moves on to catch block. I want to do a few of things here :

1. Have a global handler handle `500` error. 
2. Have custom error incase of each function call failure. I.E. propogate errors to the top.

With the above in mind we can make the following changes.

For the global handler we add the following :

```javascript
app.use(function(error, req, res, next){
  if(!error) {
    next()
  }
  logger.log({ message: error.message, level: 'error' });
  res.status(500).send('Internal server Error !')
})
```

For the secound point I.E. indivisual error handing for each type of failure, for more granuler control.

```javascript
const isUserLoggedIn = async (req, res, next) => {
  const { email, password } = req.body;

  if (!email || !password) {
    return res.status(400).json({ error: true });
  }

  try {
    /*
      - Typical code for comparing password hash.
      - Check if user exists.
    */
    await access_tokens.update_user(req.token, USER_DATA).catch((error) => {
            throw new Error(error);
          });
    await clearRedis(cannonicalName, req.token).catch((error) => {
            throw new Error(error);
          });

    await sendPromotionalEmailer().catch((error) => {
            throw new Error(error);
          });
    
    return res.status(200).json({ success: true });
  } catch (error) {
    return next(error);
  }
};
```

As you can see in the catch block we don't handler the error anymore, we just propogate it to the top. Lastly, we add `catch()` blocks to all the calls, though we have't pushed any custom messages, now we can.

To write a more robust error handling function please reference the boilerplate code from [express rest boilerplate](https://github.com/danielfsousa/express-rest-boilerplate/blob/main/src/api/middlewares/error.js).

