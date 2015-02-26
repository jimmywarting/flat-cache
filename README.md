# flat-cache
> A stupidly simple key/value storage using files to persist the data

[![NPM Version](http://img.shields.io/npm/v/flat-cache.svg?style=flat)](https://npmjs.org/package/flat-cache)
[![Build Status](http://img.shields.io/travis/royriojas/flat-cache.svg?style=flat)](https://travis-ci.org/royriojas/flat-cache)

## install

```bash
npm i --save flat-cache
```

## Usage

```js
// loads the cache, if one does not exists for the given 
// Id a new one will be prepared to be created
var cache = require('flat-cache').load('cacheId');

// sets a key on the cache
cache.setKey('key', { foo: 'var' });

// get a key from the cache
cache.getKey('key') // { foo: 'var' }

// remove a key
cache.removeKey('key'); // removes a key from the cache

// save it to disk
cache.save(); // very important, if you don't save no changes will be persisted.

// loads the cache from a given directory, if one does 
// not exists for the given Id a new one will be prepared to be created
var cache = require('flat-cache').load('cacheId', path.resolve('./path/to/folder'));
```

## Motivation for this module

I needed a super simple and dumb in memory cache with optional disk persistance in order to make 
a script that formatted files with `esformatter` only execute on the files that were changed since the last run.
To make that possible we need to store the `fileSize` and `modificationTime` of the files. So a simple `key/value` 
storage was needed and Bam! this module was born.

## Important notes

- when `cache.save` is called the values are persisted to disk, if you're committing your `node_modules` to any vcs, you
  might want to ignore the default `.cache` folder, or specify a custom directory.
- The values set on the keys of the cache should be `stringify-able` ones, meaning no circular references
- All the changes to the cache state are done to memory
- I could have use a timer or `Object.observe` to deliver the changes to disk, but I wanted to keep this module
  to be intentionally dumb and simple
- If no directory

## License 

MIT


