---
title: Using transactions in sequlize-js
widgets:
  - position: left
    type: recent_posts
date: 2021-12-26 21:47:45
thumbnail: /images/code.jpg
tags: [nodejs, javascript, error-handling, sequilizejs]
---

Lets have a quick look at using transactions in sequilizejs, basically this is useful for rolling back queries incase a query fails.

<!-- more -->


Below is a very basic example :

```javascript
try {
  const users_data = await users.create({
    email,
    hashpwd,
  });

  const customer_data = await customers.create({
    first_name,
    last_name,
    email,
  });

  await clearRedis(cannonicalName, req.token);
  await sendPromotionalEmailer();

  return res.status(200).json({ success: true });
} catch (error) {
  console.log(error)
}
```
We can improve the above code by adding transactions like below:

```javascript
const t = await sequelize.transaction();

try {
  const users_data = await users.create({
    email,
    hashpwd,
  }, { transaction: t });

  const customer_data = await customers.create({
    first_name,
    last_name,
    email,
  }, { transaction: t });

  await clearRedis(cannonicalName, req.token);
  await sendPromotionalEmailer();

  // If the execution reaches this line, no errors were thrown.
  // We commit the transaction.
  await t.commit();

  return res.status(200).json({ success: true });
} catch (error) {
  await t.rollback();
  console.log(error)
}
```

That's it for this tutorial. Hope you learned something.
