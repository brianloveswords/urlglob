# urlglob

Convert glob-like urls to regexps and match on them.

For efficiency `urlglob` stores both compiled regexps and matches in a LRU cache that can hold up to 500 items.

## Install

```bash
$ npm install urlglob
$ npm test urlglob
```

## Usage

```js
const urlglob = require('urlglob')

urlglob('*') // compiles regexp, returns `/^.*?\/?$/`
urlglob('*', '/anything/goes/here') // uses regexp from cache, performs
                                    // match and returns true. Another
                                    // test would pull result from cache

urlglob('/api/*.json', '/api/x/y.json') // true
urlglob('/api/v2/*?.json', '/api/v2/all/users.json') // false
urlglob('/api/v2/*?.json', '/api/v2/users.json') // true
```