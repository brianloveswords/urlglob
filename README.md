# urlglob [![Build Status](https://secure.travis-ci.org/brianloveswords/urlglob.png?branch=master)](http://travis-ci.org/brianloveswords/urlglob)

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

// universal (*) matching

urlglob('*') // compiles regexp, returns `/^.*?\/?$/`
urlglob('*', '/anything/goes/here') // uses regexp from cache, performs
                                    // match and returns true. Another
                                    // test would pull result from cache

urlglob('/api', '/api/') // true, notice final slash will still match
                         // to avoid the internet version of off-by-one

urlglob('/api/*.json', '/api/x/y.json') // true

// limited (*?) matching – matches anything *except* `/`

urlglob('/api/v2/*?.json', '/api/v2/all/users.json') // false
urlglob('/api/v2/*?.json', '/api/v2/users.json') // true
```

## License

MIT

```
Copyright (c) 2013 Brian J. Brennan

Permission is hereby granted, free of charge, to any person obtaining a
copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```