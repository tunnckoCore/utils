# utils [![NPM version](https://badge.fury.io/js/utils.svg)](http://badge.fury.io/js/utils)  [![Build Status](https://travis-ci.org/jonschlinkert/utils.svg)](https://travis-ci.org/jonschlinkert/utils) 

> Fast, generic JavaScript/node.js utility functions.

## Install with [npm](npmjs.org)

```bash
npm i utils --save
```

## TOC

<!-- toc -->

- [Usage](#usage)
- [API](#api)
- [Code coverage](#code-coverage)
- [Running tests](#running-tests)
- [Contributing](#contributing)
  * [Adding utils](#adding-utils)
  * [Updating the docs](#updating-the-docs)
  * [Running verb](#running-verb)
- [About](#about)
- [Related projects](#related-projects)
- [Author](#author)
- [License](#license)

_(Table of contents generated by [verb])_

<!-- tocstop -->

## Usage

**Utils grouped by collection**

The top level export gives you an object with utils grouped into collections, like `array`, `object`, `math`, etc:

```js
var utils = require('utils');
//=> {array: {flatten: [function], ...}, collection: {...}}
```

See [example.md](./example.md) for an example of the `utils` object.

**Get all utils on one object**

If you want all utils on a single object (e.g. not grouped by collection):

```js
// all utils are on the `_` property
var utils = require('utils')._;
```

**Only get a specific collection**

If you just want the `string` or `object` utils:

```js
var string = require('utils').string;
var object = require('utils').object;
```

## API

### [.after](lib/array/after.js#L19)

Returns all of the items in an array after the specified index.

**Params**

* `array` **{Array}**: Collection    
* `n` **{Number}**: Starting index (number of items to exclude)    
* `returns` **{Array}**: Array exluding `n` items.  

**Example**

```js
after(['a', 'b', 'c'], 1)
//=> ['c']
```

### [.arrayify](lib/array/arrayify.js#L20)

Cast the give `value` to an array.

**Params**

* `val` **{*}**    
* `returns` **{Array}**  

**Example**

```js
arrayify('abc')
//=> ['abc']

arrayify(['abc'])
//=> ['abc']
```

### [.before](lib/array/before.js#L20)

Returns all of the items in an array up to the specified number Opposite of `<%= after() %`.

**Params**

* `array` **{Array}**    
* `n` **{Number}**    
* `returns` **{Array}**: Array excluding items after the given number.  

**Example**

```js
before(['a', 'b', 'c'], 2)
//=> ['a', 'b']
```

### [.compact](lib/array/compact.js#L17)

Remove all falsey values from an array.

**Params**

* `arr` **{Array}**    
* `returns` **{Array}**  

**Example**

```js
compact([null, a, undefined, 0, false, b, c, '']);
//=> [a, b, c]
```

### [.difference](lib/array/difference.js#L24)

Return the difference between the first array and additional arrays.

**Params**

* `a` **{Array}**    
* `b` **{Array}**    
* `returns` **{Array}**  

**Example**

```js
var a = ['a', 'b', 'c', 'd'];
var b = ['b', 'c'];

diff(a, b);
//=> ['a', 'd']
```

### [.each](lib/array/each.js#L27)

Loop over each item in an array and call the given function on every element.

**Params**

* `array` **{Array}**    
* `fn` **{Function}**    
* `thisArg` **{Object}**: Optionally pass a `thisArg` to be used as the context in which to call the function.    
* `returns` **{Array}**  

**Example**

```js
each(['a', 'b', 'c'], function (ele) {
  return ele + ele;
});
//=> ['aa', 'bb', 'cc']

each(['a', 'b', 'c'], function (ele, i) {
  return i + ele;
});
//=> ['0a', '1b', '2c']
```

### [.first](lib/array/first.js#L20)

Returns the first item, or first `n` items of an array.

**Params**

* `array` **{Array}**    
* `n` **{Number}**: Number of items to return, starting at `0`.    
* `returns` **{Array}**  

**Example**

```js
first(['a', 'b', 'c', 'd', 'e'], 2)
//=> ['a', 'b']
```

### [.flatten](lib/array/flatten.js#L18)

Recursively flatten an array or arrays. Uses the fastest implementation of array flatten for node.js

**Params**

* `array` **{Array}**    
* `returns` **{Array}**: Flattened array  

**Example**

```js
flatten(['a', ['b', ['c']], 'd', ['e']]);
//=> ['a', 'b', 'c', 'd', 'e']
```

### [.forEach](lib/array/forEach.js#L27)

Loop over each item in an array and call the given function on every element.

**Params**

* `array` **{Array}**    
* `fn` **{Function}**    
* `thisArg` **{Object}**: Optionally pass a `thisArg` to be used as the context in which to call the function.    
* `returns` **{Array}**  

**Example**

```js
forEach(['a', 'b', 'c'], function (ele) {
  return ele + ele;
});
//=> ['aa', 'bb', 'cc']

forEach(['a', 'b', 'c'], function (ele, i) {
  return i + ele;
});
//=> ['0a', '1b', '2c']
```

### [.isArray](lib/array/isArray.js#L19)

Returns true if the given `value` is an array.

**Params**

* `value` **{Array}**: Value to test.    

**Example**

```js
isArray(1);
//=> 'false'

isArray([1]);
//=> 'true'
```

### [.last](lib/array/last.js#L20)

Returns the last item, or last `n` items of an array.

**Params**

* `array` **{Array}**    
* `n` **{Number}**: Number of items to return, starting with the last item.    
* `returns` **{Array}**  

**Example**

```js
last(['a', 'b', 'c', 'd', 'e'], 2)
//=> ['d', 'e']
```

### [.map](lib/array/map.js#L27)

Returns a new array with the results of calling the given function on every element in the array. This is a faster, node.js focused alternative to JavaScript's native array map.

**Params**

* `array` **{Array}**    
* `fn` **{Function}**    
* `returns` **{Array}**  

**Example**

```js
map(['a', 'b', 'c'], function (ele) {
  return ele + ele;
});
//=> ['aa', 'bb', 'cc']

map(['a', 'b', 'c'], function (ele, i) {
  return i + ele;
});
//=> ['0a', '1b', '2c']
```

### [.slice](lib/array/slice.js#L21)

Alternative to JavaScript's native array-slice method. Slices `array` from the `start` index up to but not including the `end` index.

**Params**

* `array` **{Array}**: the array to slice.    
* `start` **{Number}**: Optionally define the starting index.    
* `end` **{Number}**: Optionally define the ending index.    

**Example**

```js
var arr = ['a', 'b', 'd', 'e', 'f', 'g', 'h', 'i', 'j'];

slice(arr, 3, 6);
//=> ['e', 'f', 'g']
```

### [.union](lib/array/union.js#L19)

Return an array free of duplicate values. Fastest ES5 implementation.

**Params**

* `array` **{Array}**: The array to uniquify    
* `returns` **{Array}**: With all union values.  

**Example**

```js
union(['a', 'b', 'c', 'c']);
//=> ['a', 'b', 'c']
```

### [.unique](lib/array/unique.js#L19)

Return an array free of duplicate values. Fastest ES5 implementation.

**Params**

* `array` **{Array}**: The array to uniquify    
* `returns` **{Array}**: With all unique values.  

**Example**

```js
unique(['a', 'b', 'c', 'c']);
//=> ['a', 'b', 'c']
```

### [.any](lib/collection/any.js#L14)

Returns `true` if `value` exists in the given string, array
or object. See [any] for documentation.

**Params**

* `value` **{*}**    
* `target` **{*}**    
* `options` **{Object}**    

### [.contains](lib/collection/contains.js#L17)

Return true if `collection` contains `value`

**Params**

* `collection` **{Array|Object}**    
* `string` **{*}**    
* `returns` **{Boolean}**  

### [.tryReaddir](lib/fs/tryReaddir.js#L16)

Try to read the given `directory`. Wraps `fs.readdirSync()` with
a try/catch, so it fails silently instead of throwing when the
directory doesn't exist.

**Params**

* `dir` **{String}**: Starting directory    
* `returns` **{Array}**: Array of files.  

### [.tryRequire](lib/fs/tryRequire.js#L15)

Try to require the given file, returning `null` if not successful
instead of throwing an error.

**Params**

* `fp` **{String}**: File path of the file to require    
* `returns` **{*}**: Returns the module function/object, or `null` if not found.  

### [.hasValues](lib/lang/hasValues.js#L34)

Returns true if any value exists, false if empty. Works for booleans, functions, numbers, strings, nulls, objects and arrays.

**Params**

* `object` **{Object}**: The object to check for `value`    
* `value` **{*}**: the value to look for    
* `returns` **{Boolean}**: True if any values exists.  

**Example**

```js
utils.lang.hasValues('a');
//=> true

utils.lang.hasValues('');
//=> false

utils.lang.hasValues(1);
//=> true

utils.lang.hasValues({a: 'a'}});
//=> true

utils.lang.hasValues({}});
//=> false

utils.lang.hasValues(['a']);
//=> true
```

### [.isEmpty](lib/lang/isEmpty.js#L37)

Returns true if the given value is empty, false if any value exists. Works for booleans, functions, numbers, strings, nulls, objects and arrays.

**Params**

* `object` **{Object}**: The object to check for `value`    
* `value` **{*}**: the value to look for    
* `returns` **{Boolean}**: False if any values exists.  

**Example**

```js
utils.lang.isEmpty('a');
//=> true

utils.lang.isEmpty('');
//=> false

utils.lang.isEmpty(1);
//=> true

utils.lang.isEmpty({a: 'a'}});
//=> true

utils.lang.isEmpty({}});
//=> false

utils.lang.isEmpty(['a']);
//=> true
```

### [.isObject](lib/lang/isObject.js#L22)

Return true if the given `value` is an object with keys.

**Params**

* `value` **{Object}**: The value to check.    
* `returns` **{Boolean}**  

**Example**

```js
isObject(['a', 'b', 'c'])
//=> 'false'

isObject({a: 'b'})
//=> 'true'
```

### [.isPlainObject](lib/lang/isPlainObject.js#L23)

Return true if the given `value` is an object with keys.

**Params**

* `value` **{Object}**: The value to check.    
* `returns` **{Boolean}**  

**Example**

```js
isPlainObject(Object.create({}));
//=> true
isPlainObject(Object.create(Object.prototype));
//=> true
isPlainObject({foo: 'bar'});
//=> true
isPlainObject({});
//=> true
```

### [.sum](lib/math/sum.js#L20)

Returns the sum of all numbers in the given array.

**Params**

* `array` **{Array}**: Array of numbers to add up.    
* `returns` **{Number}**  

**Example**

```js
sum([1, 2, 3, 4, 5])
//=> '15'
```

### [.defaults](lib/object/defaults.js#L13)

Extend `object` with properties of other `objects`

**Params**

* `object` **{Object}**: The target object. Pass an empty object to shallow clone.    
* `objects` **{Object}**    
* `returns` **{Object}**  

### [.extend](lib/object/extend.js#L16)

Extend `o` with properties of other `objects`.

**Params**

* `o` **{Object}**: The target object. Pass an empty object to shallow clone.    
* `objects` **{Object}**    
* `returns` **{Object}**  

### [.functions](lib/object/functions.js#L20)

Returns a copy of the given `obj` filtered to have only enumerable properties that have function values.

**Params**

* `obj` **{Object}**    
* `returns` **{Object}**  

**Example**

```js
functions({a: 'b', c: function() {}});
//=> {c: function() {}}
```

### [.hasOwn](lib/object/hasOwn.js#L18)

Return true if `key` is an own, enumerable property of the given `obj`.

**Params**

* `key` **{String}**    
* `obj` **{Object}**: Optionally pass an object to check.    
* `returns` **{Boolean}**  

**Example**

```js
hasOwn(obj, key);
```

### [.keys](lib/object/keys.js#L15)

Return an array of keys for the given `obj`. Uses `Object.keys`
when available, otherwise falls back on `forOwn`.

**Params**

* `obj` **{Object}**    
* `returns` **{Array}**: Array of keys.  

### [.merge](lib/object/merge.js#L23)

Recursively combine the properties of `o` with the
properties of other `objects`.

**Params**

* `o` **{Object}**: The target object. Pass an empty object to shallow clone.    
* `objects` **{Object}**    
* `returns` **{Object}**  

### [.methods](lib/object/methods.js#L15)

Returns a list of all enumerable properties of `obj` that have function
values

**Params**

* `obj` **{Object}**    
* `returns` **{Array}**  

### [.reduce](lib/object/reduce.js#L32)

Reduces an object to a value that is the accumulated result of running each property in the object through a callback.

**Params**

* `obj` **{Object}**: The object to iterate over.    
* `iterator` **{Function}**: Iterator function    
* `initial` **{Object}**: Initial value.    
* `thisArg` **{Object}**: The `this` binding of the iterator function.    
* `returns` **{Object}**  

**Example**

```js
var a = {a: 'foo', b: 'bar', c: 'baz'};

reduce(a, function (acc, value, key, obj) {
  // `acc`- the initial value (or value from the previous callback call),
  // `value`- the of the current property,
  // `key`- the of the current property, and
  // `obj` - original object

  acc[key] = value.toUpperCase();
  return acc;
}, {});

//=> {a: 'FOO', b: 'BAR', c: 'BAZ'};
```

### [.camelcase](lib/string/camelcase.js#L20)

camelCase the characters in `string`.

**Params**

* `string` **{String}**: The string to camelcase.    
* `returns` **{String}**  

**Example**

```js
camelcase("foo bar baz");
//=> 'fooBarBaz'
```

### [.centerAlign](lib/string/centerAlign.js#L21)

Center align the characters in a string using non-breaking spaces.

**Params**

* `str` **{String}**: The string to reverse.    
* `returns` **{String}**: Centered string.  

**Example**

```js
centerAlign("abc");
```

### [.chop](lib/string/chop.js#L26)

Like trim, but removes both extraneous whitespace and non-word characters from the beginning and end of a string.

**Params**

* `string` **{String}**: The string to chop.    
* `returns` **{String}**  

**Example**

```js
chop("_ABC_");
//=> 'ABC'

chop("-ABC-");
//=> 'ABC'

chop(" ABC ");
//=> 'ABC'
```

### [.count](lib/string/count.js#L21)

Count the number of occurrances of a substring within a string.

**Params**

* `string` **{String}**    
* `substring` **{String}**    
* `returns` **{Number}**: The occurances of `substring` in `string`  

**Example**

```js
count("abcabcabc", "a");
//=> '3'
```

### [.dashcase](lib/string/dashcase.js#L22)

dash-case the characters in `string`. This is similar to [slugify], but [slugify] makes the string compatible to be used as a URL slug.

**Params**

* `string` **{String}**    
* `returns` **{String}**  

**Example**

```js
dashcase("a b.c d_e");
//=> 'a-b-c-d-e'
```

### [.dotcase](lib/string/dotcase.js#L20)

dot.case the characters in `string`.

**Params**

* `string` **{String}**    
* `returns` **{String}**  

**Example**

```js
dotcase("a-b-c d_e");
//=> 'a.b.c.d.e'
```

### [.ellipsis](lib/string/ellipsis.js#L23)

Truncate a string to the specified `length`, and append it with an elipsis, `…`.

**Params**

* `str` **{String}**    
* `length` **{Number}**: The desired length of the returned string.    
* `ch` **{String}**: Optionally pass custom characters to append. Default is `…`.    
* `returns` **{String}**: The truncated string.  

**Example**

```js
ellipsis("<span>foo bar baz</span>", 7);
//=> 'foo bar…'
```

### [.hyphenate](lib/string/hyphenate.js#L20)

Replace spaces in a string with hyphens. This

**Params**

* `string` **{String}**    
* `returns` **{String}**  

**Example**

```js
hyphenate("a b c");
//=> 'a-b-c'
```

### [.isString](lib/string/isString.js#L20)

Returns true if the value is a string.

**Params**

* `val` **{String}**    
* `returns` **{Boolean}**: True if the value is a string.  

**Example**

```js
isString('abc');
//=> 'true'

isString(null);
//=> 'false'
```

### [.pascalcase](lib/string/pascalcase.js#L20)

PascalCase the characters in `string`.

**Params**

* `string` **{String}**    
* `returns` **{String}**  

**Example**

```js
pascalcase("foo bar baz");
//=> 'FooBarBaz'
```

### [.pathcase](lib/string/pathcase.js#L20)

path/case the characters in `string`.

**Params**

* `string` **{String}**    
* `returns` **{String}**  

**Example**

```js
pathcase("a-b-c d_e");
//=> 'a/b/c/d/e'
```

### [.replace](lib/string/replace.js#L21)

Replace occurrences of `a` with `b`.

**Params**

* `str` **{String}**    
* `a` **{String|RegExp}**: Can be a string or regexp.    
* `b` **{String}**    
* `returns` **{String}**  

**Example**

```js
replace("abcabc", /a/, "z");
//=> 'zbczbc'
```

### [.reverse](lib/string/reverse.js#L19)

Reverse the characters in a string.

**Params**

* `str` **{String}**: The string to reverse.    
* `returns` **{String}**  

**Example**

```js
reverse("abc");
//=> 'cba'
```

### [.rightAlign](lib/string/rightAlign.js#L21)

Right align the characters in a string using non-breaking spaces.

**Params**

* `str` **{String}**: The string to reverse.    
* `returns` **{String}**: Right-aligned string.  

**Example**

```js
rightAlign(str);
```

### [.sentencecase](lib/string/sentencecase.js#L19)

Sentence-case the characters in `string`.

**Params**

* `string` **{String}**    
* `returns` **{String}**  

**Example**

```js
sentencecase("foo bar baz.");
//=> 'Foo bar baz.'
```

### [.snakecase](lib/string/snakecase.js#L20)

snake_case the characters in `string`.

**Params**

* `string` **{String}**    
* `returns` **{String}**  

**Example**

```js
snakecase("a-b-c d_e");
//=> 'a_b_c_d_e'
```

### [.truncate](lib/string/truncate.js#L21)

Truncate a string by removing all HTML tags and limiting the result to the specified `length`.

**Params**

* `str` **{String}**    
* `length` **{Number}**: The desired length of the returned string.    
* `returns` **{String}**: The truncated string.  

**Example**

```js
truncate("<span>foo bar baz</span>", 7);
//=> 'foo bar'
```

### [.wordwrap](lib/string/wordwrap.js#L21)

Wrap words to a specified width using [word-wrap].

**Params**

* `string` **{String}**: The string with words to wrap.    
* `object` **{Options}**: Options to pass to [word-wrap]    
* `returns` **{String}**: Formatted string.  

**Example**

```js
wordwrap("a b c d e f", {width: 5, newline: '<br>  '});
//=> '  a b c <br>  d e f'
```

_(API documentation generated by [Verb])_

## Code coverage

Please help improve code coverage by [adding unit tests](#contributing).

```
-----------------------|-----------|-----------|-----------|-----------|
File                   |   % Stmts |% Branches |   % Funcs |   % Lines |
-----------------------|-----------|-----------|-----------|-----------|
   array/              |     82.29 |     71.67 |     92.31 |      82.8 |
      after.js         |       100 |        75 |       100 |       100 |
      arrayify.js      |       100 |       100 |       100 |       100 |
      before.js        |       100 |        75 |       100 |       100 |
      compact.js       |       100 |       100 |       100 |       100 |
      difference.js    |       100 |       100 |       100 |       100 |
      each.js          |       100 |       100 |       100 |       100 |
      first.js         |     88.89 |     83.33 |       100 |     88.24 |
      flatten.js       |       100 |       100 |       100 |       100 |
      forEach.js       |       100 |       100 |       100 |       100 |
      indexOf.js       |      7.69 |         0 |         0 |      8.33 |
      isArray.js       |       100 |       100 |       100 |       100 |
      last.js          |     88.89 |     83.33 |       100 |     88.24 |
      map.js           |       100 |       100 |       100 |       100 |
      slice.js         |       100 |       100 |       100 |       100 |
      sort.js          |     90.91 |      87.5 |       100 |     90.91 |
      union.js         |       100 |       100 |       100 |       100 |
      unique.js        |       100 |       100 |       100 |       100 |
   collection/         |        50 |         0 |         0 |        50 |
      any.js           |       100 |       100 |       100 |       100 |
      contains.js      |     42.86 |         0 |         0 |     42.86 |
   fs/                 |        80 |       100 |       100 |        80 |
      tryReaddir.js    |        80 |       100 |       100 |        80 |
      tryRequire.js    |        80 |       100 |       100 |        80 |
   lang/               |      87.5 |       100 |        50 |      87.5 |
      hasValues.js     |       100 |       100 |       100 |       100 |
      isEmpty.js       |     66.67 |       100 |         0 |     66.67 |
      isObject.js      |       100 |       100 |       100 |       100 |
      isPlainObject.js |       100 |       100 |       100 |       100 |
   math/               |       100 |       100 |       100 |       100 |
      sum.js           |       100 |       100 |       100 |       100 |
   object/             |        70 |     54.55 |     27.27 |     69.12 |
      defaults.js      |       100 |       100 |       100 |       100 |
      extend.js        |       100 |     83.33 |       100 |       100 |
      filter.js        |       100 |       100 |       100 |       100 |
      forIn.js         |       100 |       100 |       100 |       100 |
      forOwn.js        |       100 |       100 |       100 |       100 |
      functions.js     |     28.57 |         0 |         0 |     28.57 |
      hasOwn.js        |       100 |       100 |       100 |       100 |
      keys.js          |     33.33 |        50 |         0 |     33.33 |
      merge.js         |       100 |        75 |       100 |       100 |
      methods.js       |     28.57 |         0 |         0 |     28.57 |
      omit.js          |       100 |       100 |       100 |       100 |
      pick.js          |       100 |       100 |       100 |       100 |
      reduce.js        |       100 |       100 |       100 |       100 |
      some.js          |        30 |         0 |         0 |        30 |
   string/             |     99.27 |     96.77 |        96 |     99.09 |
      camelcase.js     |       100 |       100 |       100 |       100 |
      centerAlign.js   |       100 |       100 |       100 |       100 |
      chop.js          |       100 |       100 |       100 |       100 |
      count.js         |       100 |       100 |       100 |       100 |
      dashcase.js      |       100 |       100 |       100 |       100 |
      dotcase.js       |       100 |       100 |       100 |       100 |
      ellipsis.js      |       100 |       100 |       100 |       100 |
      hyphenate.js     |       100 |       100 |       100 |       100 |
      index.js         |       100 |       100 |       100 |       100 |
      isString.js      |       100 |       100 |       100 |       100 |
      pascalcase.js    |       100 |       100 |       100 |       100 |
      pathcase.js      |       100 |       100 |       100 |       100 |
      replace.js       |       100 |       100 |       100 |       100 |
      reverse.js       |       100 |       100 |       100 |       100 |
      rightAlign.js    |       100 |       100 |       100 |       100 |
      sentencecase.js  |       100 |       100 |       100 |       100 |
      slugify.js       |       100 |       100 |       100 |       100 |
      snakecase.js     |       100 |       100 |       100 |       100 |
      toString.js      |        50 |         0 |         0 |        50 |
      truncate.js      |       100 |       100 |       100 |       100 |
      wordwrap.js      |       100 |       100 |       100 |       100 |
-----------------------|-----------|-----------|-----------|-----------|
All files              |     86.43 |     79.05 |     76.79 |     85.34 |
-----------------------|-----------|-----------|-----------|-----------|
```

## Running tests

Install dev dependencies:

```bash
npm i -d && npm test
```

## Contributing

> Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/utils/issues)

### Adding utils

If you want to do a PR to add a util, please read the following first:
 
  - follow the same coding style as the rest of the library, same with code comments
  - add sufficient unit tests
  - Install dev dependencies and [run verb](#running-verb)
  - Look over the README to make sure that verb rendered out the docs with your method and code comments.

**Adding external modules as dependencies**

- External modules will only be considered if they meet the same quality and coding standards as the rest of the library. At minimum this includes documentation, code comments, and unit tests. Benchmarks are also strongly preferred.

### Updating the docs

Do not edit the readme manually since [verb] is used to generate documentation. 

  - API docs: If you see an error in the API documentation, just update the code comments for that method, then [run verb](#running-verb).
  - Everything else, please look over the [.verb.md](./.verb.md) template to see where the error is, then [run verb](#running-verb).

### Running verb

Run [verb] to generate documentation:

```js
npm i -d && verb
```

## About

**Why another utils lib?**

- I'm a node.js developer. I want fast, light, dependable utility functions for node.js projects. 
  - Do you really need bloated, everything-but-the-kitchen-sink functions that are guaranteed to work with IE 4, **for your Yeoman generator or gulp plugin**!? Nonsense. 
  - The benchmarks that accompany many of the functions in the library show that in some cases, the penalty for using such "kitchen-sink" code is a 2,000-5,000% reduction in speed. Sometimes greater.

**Project goals**

- Fastest implementation of each method, without too much compromise. Covering uncommon cases is fine, but don't go overboard.
  - Clean well-documented, commented code.
  - [When it makes sense](#adding-utils), external libraries are used and exposed instead of writing new code. 
  - Focus on node.js usage and projects that are likely to use a number of these utils in one project. If you only need one or two of these in a small project, don't use this. Use small modules that do only one thing.

## Related projects

> This project depends on these great libraries:

* [any](https://github.com/jonschlinkert/any): Returns `true` if a value exists in the given string,… [more](https://github.com/jonschlinkert/any)
* [arr-diff](https://github.com/jonschlinkert/arr-diff): Returns an array with only the unique values from the… [more](https://github.com/jonschlinkert/arr-diff)
* [arr-flatten](https://github.com/jonschlinkert/arr-flatten): Recursively flatten an array or arrays. This is the fastest… [more](https://github.com/jonschlinkert/arr-flatten)
* [arr-map](https://github.com/jonschlinkert/arr-map): Faster, node.js focused alternative to JavaScript's native array map.
* [arr-union](https://github.com/jonschlinkert/arr-union): Combines a list of arrays, returning a single array with… [more](https://github.com/jonschlinkert/arr-union)
* [array-each](https://github.com/jonschlinkert/array-each): Loop over each item in an array and call the… [more](https://github.com/jonschlinkert/array-each)
* [array-slice](https://github.com/jonschlinkert/array-slice): Array-slice method. Slices `array` from the `start` index up to,… [more](https://github.com/jonschlinkert/array-slice)
* [array-unique](https://github.com/jonschlinkert/array-unique): Return an array free of duplicate values. Fastest ES5 implementation.
* [center-align](https://github.com/jonschlinkert/center-align): Center-align the text in a string.
* [export-dirs](https://github.com/jonschlinkert/export-dirs): Export directories and their files as node.js modules.
* [export-files](https://github.com/jonschlinkert/export-files): node.js utility for exporting a directory of files as modules.
* [for-in](https://github.com/jonschlinkert/for-in): Iterate over the own and inherited enumerable properties of an… [more](https://github.com/jonschlinkert/for-in)
* [for-own](https://github.com/jonschlinkert/for-own): Iterate over the own enumerable properties of an object, and… [more](https://github.com/jonschlinkert/for-own)
* [has-values](https://github.com/jonschlinkert/has-values): Returns true if any values exist, false if empty. Works… [more](https://github.com/jonschlinkert/has-values)
* [is-number](https://github.com/jonschlinkert/is-number): Returns true if the value is a number. comprehensive tests.
* [is-plain-object](https://github.com/jonschlinkert/is-plain-object): Returns true if an object was created by the `Object`… [more](https://github.com/jonschlinkert/is-plain-object)
* [kind-of](https://github.com/jonschlinkert/kind-of): Get the native type of a value.
* [make-iterator](https://github.com/jonschlinkert/make-iterator): Convert an argument into a valid iterator. Based on the… [more](https://github.com/jonschlinkert/make-iterator)
* [object.defaults](https://github.com/jonschlinkert/object.defaults): Like `extend` but only copies missing properties/values to the target… [more](https://github.com/jonschlinkert/object.defaults)
* [object.filter](https://github.com/jonschlinkert/object.filter): Create a new object filtered to have only properties for… [more](https://github.com/jonschlinkert/object.filter)
* [object.omit](https://github.com/jonschlinkert/object.omit): Return a copy of an object without the given key,… [more](https://github.com/jonschlinkert/object.omit)
* [object.pick](https://github.com/jonschlinkert/object.pick): Returns a filtered copy of an object with only the… [more](https://github.com/jonschlinkert/object.pick)
* [object.reduce](https://github.com/jonschlinkert/object.reduce): Reduces an object to a value that is the accumulated… [more](https://github.com/jonschlinkert/object.reduce)
* [right-align](https://github.com/jonschlinkert/right-align): Right-align the text in a string.
* [word-wrap](https://github.com/jonschlinkert/word-wrap): Wrap words to a specified length.

## Author

**Jon Schlinkert**

+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright (c) 2015 Jon Schlinkert
Released under the MIT license.

***

_This file was generated by [verb-cli](https://github.com/assemble/verb-cli) on April 25, 2015._

<!-- reflinks generated by verb-reflinks plugin -->

[verb]: https://github.com/assemble/verb
[template]: https://github.com/jonschlinkert/template
[assemble]: http://assemble.io
