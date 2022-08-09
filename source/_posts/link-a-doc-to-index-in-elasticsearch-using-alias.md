---
title: Link a doc to index in elasticsearch using alias
date: 2022-07-08 21:49:31
tags: [elasticsearch]
thumbnail: /images/code.jpg
excerpt: 'Sometimes you may have the need to link a doc to an index, cause deleteing the doc associated with a certain unique id becomes so much easier.'
---

Sometimes you may have the need to link a doc to an index, cause deleteing the doc associated with a certain unique id becomes so much easier.

Example time , first lets create our index.

```javascript
PUT alias_test_index
{
  "settings": {},
  "mappings": {
    "properties": {
      "name": {
        "type": "text"
      }
    }
  }
}
```

Now lets add a few _docs to our index

```javascript
POST alias_test_index/_doc/1
{
  "name": "anzo"
}

POST alias_test_index/_doc/2
{
  "name": "malko"
}
```

Lets create an alias that links our _doc to the top level index

```javascript
PUT alias_test_index/_aliases
{
  "actions": [
    {
      "add": {
        "index": "alias_test_index",
        "alias": "anzo",
        "filter": {
          "term": {
            "name": "anzo"
          }
        }
      }
    }
  ]
}
```

And now BOOM just like that we can delete a _doc by doing something like 

```javascript
POST anzo/_delete_by_query?q=*

// _doc/1 is gone viola magic!!
```

Learnt this trick from this SO article [HERE](https://stackoverflow.com/questions/53975779/elasticsearch-6-0-removal-of-mapping-types-alternatives). 

Cheers and hope you learnt something.



