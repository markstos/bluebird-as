bluebird-as
===========

A tiny number of helper functions to use with bluebird (other promise libraries not tested) for higher level functions such as sequence etc

Usage
-----

var Promise = require('bluebird');

var as = require('bluebird-as');
as.use(Promise);


### sequenceOf
Run Promises in strict sequence (without passing the result).

javascript:

```javascript
  var urls = ['http://www.google.de'];

  Promise.cast(urls)
    .then( as.sequenceOf(function(url){
      return scrapeUrlIntoDatabaseOrSo(url);
    }))
    .then(function(){
      doSomethingWithAllResultsCollectedInDatabase();
    });
```

coffeescript:

```coffeescript
  urls = ['http://www.google.de']

  Promise.cast(urls)
    .then as.sequenceOf (url)->
      scrapeUrlIntoDatabaseOrSo(url)
    .then ()->
      doSomethingWithAllResultsCollectedInDatabase()
```

This is like [async.eachSeries](https://github.com/caolan/async#eachSeries)


### sequenceWithParallelism
Run promises in sequence but with a degree of parallelism.

javascript:

```javascript
  var urls = ['http://www.google.de'];

  Promise.cast(urls)
    .then( as.sequenceWithParallelism(10,function(url){
      return scrapeUrlIntoDatabaseOrSo(url);
    }))
    .then(function(){
      doSomethingWithAllResultsCollectedInDatabase();
    });
```

coffeescript:

```coffeescriptThis is like [async.eachSeries](https://github.com/caolan/async#eachSeries)
  urls = ['http://www.google.de']

  Promise.cast(urls)
    .then as.sequenceWithParallelism 10, (url)->
      scrapeUrlIntoDatabaseOrSo(url)
    .then ()->
      doSomethingWithAllResultsCollectedInDatabase()
```

This is like [async.eachLimit](https://github.com/caolan/async#eachLimit)
