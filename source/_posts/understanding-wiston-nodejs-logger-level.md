---
title: Understanding level in winston nodejs logger.
date: 2022-10-21 22:54:49
tags: [node, express, javascript, morgan, winston]
thumbnail: /images/code.jpg
excerpt: 'Understanding how level works in winston logger, with a code example.'
---

So suppose you have a logger in winston like so :-

```javascript
// logger.js - main application file
const winston = require('winston');

const logger = winston.createLogger({
  level: 'info',
  levels: winston.config.npm.levels,
  format: winston.format.json(),
  transports: [
    //
    // - Write to all logs with level `info` and below to `combined.log`
    // - Write all logs error (and below) to `error.log`.
    //
    new winston.transports.File({ filename: 'error.log', level: 'error' }),
    new winston.transports.File({ filename: 'combined.log' }),
  ],
});

module.exports = logger;
```

You can define levels at the top level as well as at the level of each transport, so basically in the above example if you defined any transport eg.  

```
new winston.transports.File({ filename: 'combined.log' }),
```

The above defined transport would only log *error*, *warn* and *info* and the levels that would't be logged would be *http*, *verbose*, *debug* and *silly*. Keep in mind the default logging levels is `npm logging levels`. Just for reference the npm logging levels are listed below. More can be learnt about logging levels in the winston [HERE](https://github.com/winstonjs/winston#logging-levels) and the spec can be found [HERE](https://www.rfc-editor.org/rfc/rfc5424).

```json
{
  error: 0,
  warn: 1,
  info: 2,
  http: 3,
  verbose: 4,
  debug: 5,
  silly: 6
}
```

Also keep in mind you can override the level at the transport level like below, now the below will log for all levels, except silly i.e. debug and below. 

```javascript
new winston.transports.File({ filename: 'combined.log', level: 'debug' })
```

Hope this was insightful to you. cheers.

