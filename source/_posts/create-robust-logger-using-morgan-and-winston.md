---
title: Create robust logger using morgan and winston in your express app
date: 2022-09-19 17:32:25
tags: [node, express, javascript, morgan, winston]
thumbnail: /images/code-2.jpg
excerpt: 'Ever wanted to create a robust logger when for each log type(error, info, warn) and have granular control ?'
---

Ever wanted to create a robust logger when for each type log (error, info, warn) you have granular control ? A combination of [winston](https://www.npmjs.com/package/winston) and [morgan](https://www.npmjs.com/package/morgan) can help you acheive the same. Here's a simple demo to setup both these packages in you're existing or new express project


```javascript
// index.js - main application file

const morgan = require('morgan');
const envLogType = process.env.NODE_ENV === 'production' ? 'combined' : 'dev',

app.use(morgan(envLogType, { stream: { write: (message) => logger.log('info', message) } }));
```


```javascript
// logger.js - main application file
const winston = require('winston');

const logger = winston.createLogger({
  level: 'info',
  format: winston.format.simple(),
  transports: [
    //
    // - Write to all logs with level `info` and below to `combined.log`
    // - Write all logs error (and below) to `error.log`.
    //
    new winston.transports.File({ filename: 'error.log', level: 'error' }),
    new winston.transports.File({ filename: 'combined.log', level: 'info' }),
  ],
});

if (process.env.NODE_ENV !== 'production') {
  logger.add(new winston.transports.Console({
    format: winston.format.simple(),
  }));
}

module.exports = logger;
```

And voila ! thats it.

Do checkout the [**docs**](https://github.com/winstonjs/winston#usage) for winston as it is a package that does have a slight learn curve as it has multiple options I.E. log levels (error|info|warn|silly...) , Transport options(File,Console...) , also format I.E. what format would you like the logs to appear in. 

Cheers and hope this article was insightful.