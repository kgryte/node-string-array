String Array
===
[![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Coverage Status][coveralls-image]][coveralls-url] [![Dependencies][dependencies-image]][dependencies-url]

> String array class.

Why not just use native `Arrays`? A `StringArray`

*	prevents non-string primitives from being added to the `array`
*	provides options to constrain `string` length
*	allows __fancy indexing__

===
1. [Install](#installation)
1. [Usage](#usage)
	-	[StringArray()](#string-array)
	-	[Properties](#properties)
		*	[length](#length)
		*	[minLength](#minlength)
		*	[maxLength](#maxlength)
	-	[Mutator Methods](#mutator-methods)
		*	[push()](#push)
		*	[pop()](#pop)
		*	[unshift()](#unshift)
		*	[shift()](#shift)
		*	[reverse()](#reverse)
		*	[sort()](#sort)
		*	[splice()](#splice)
	-	[Accessor Methods](#accessor-methods)
		*	[indexOf()](#indexof)
		*	[lastIndexOf()](#lastindexof)
		*	[slice()](#slice)
		*	[concat()](#concat)
		*	[join()](#join)
		*	[toString()](#tostring)
		*	[toLocaleString()](#tolocalestring)
		*	[toArray()](#toarray)
	-	[Iteration Methods](#iteration-methods)
1. [Examples](#examples)
1. [Notes](#notes)
1. [Tests](#tests)
	-	[Unit](#unit)
	-	[Coverage](#test-coverage)
1. [License](#license)


===
## Installation

``` bash
$ npm install string-array
```

For use in the browser, use [browserify](https://github.com/substack/node-browserify).


## Usage

``` javascript
var StringArray = require( 'string-array' );
```


<a name="string-array"></a>
#### StringArray( [len, opts] )

String array constructor. If provided a length `len`, initializes an empty `StringArray` of length `len`.

``` javascript
var arr = new StringArray();

arr.length;
// returns 0

arr = new StringArray( 20 );

arr.length;
//returns 20
```

The constructor accepts an options `object` with the following options:
*	__min__: minimum length of a `string` added to the `array`. Default: `0`.
*	__max__: maximum length of a `string` added to the `array`. Default: `2^32-1`.

``` javascript
var opts = {
	'min': 5,
	'max': 10
};

var arr = new StringArray( opts );

// Valid string...
arr.push( 'Hello' );

// Invalid string...
arr.push( 'a' );
// throws RangeError

// Invalid string...
arr.push( 'How are you doing today?' );
// throw RangeError
```


===
#### Properties


<a name="length"></a>
##### [length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/length)

Returns the number of `array` elements.

``` javascript
var arr = new StringArray();

arr.length;
// returns 0

arr.push( 'beep' );
arr.length;
// returns 1

arr.length = 0;
arr.length;
// returns 0
```


<a name="minlength"></a>
##### minLength

Specifies the minimum allowed length of `strings` added to the `array`. Default length is `0`.

``` javascript
var arr = new StringArray();

arr.minLength;
// returns 0

// Valid string...
arr.push( 'beep' );

arr.minLength = 5;

// Invalid string...
arr.push( 'beep' );
// throws RangeError
```

__Note__: setting the `minLength` after elements have been added to the `array` does __not__ affect the existing elements; the setting only applies to future `strings` added to the `array`.


<a name="maxlength"></a>
##### maxLength

Specifies the maximum allowed length of `strings` added to the `array`. Default length is `2^32-1`.

``` javascript
var arr = new StringArray();

arr.maxLength;
// returns 2^31-1

// Valid string...
arr.push( 'beep' );

arr.maxLength = 3;

// Invalid string...
arr.push( 'beep' );
// throws RangeError
```

__Note__: setting the `maxLength` after elements have been added to the `array` does __not__ affect the existing elements; the setting only applies to future `strings` added to the `array`.


===
#### Mutator Methods


<a name="push"></a>
##### [StringArray.prototype.push( string0[, string1[,...]] )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)

Adds one or more elements to the end of an `array` and returns the new `array` length.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
// returns 3

arr.toString();
// returns 'a,b,c'

arr.push( 'd' );
// returns 4

arr.toString();
// returns 'a,b,c,d'
```


<a name="pop"></a>
##### [StringArray.prototype.pop()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)

Removes the last `array` element and returns that element.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
arr.toString();
// returns 'a,b,c'

arr.pop();
// returns 'c'

arr.toString();
// returns 'a,b'
```



<a name="unshift"></a>
##### [StringArray.prototype.unshift( string0[, string1[,...]] )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)

Adds one or more elements to the front of an `array` and returns the new `array` length.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
// returns 3

arr.toString();
// returns 'a,b,c'

arr.unshift( 'd' );
// returns 4

arr.toString();
// returns 'd,a,b,c'
```


<a name="shift"></a>
##### [StringArray.prototype.shift()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)

Removes the first `array` element and returns that element.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
arr.toString();
// returns 'a,b,c'

arr.shift();
// returns 'a'

arr.toString();
// returns 'b,c'
```


<a name="reverse"></a>
##### [StringArray.prototype.reverse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)

Reverses the `array` order.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
arr.toString();
// returns 'a,b,c'

arr.reverse();
arr.toString();
// returns 'c,b,a'
```


<a name="sort"></a>
##### [StringArray.prototype.sort( [comparator] )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

Sorts the `array` elements __in place__.

``` javascript
var arr = new StringArray();

function descending( a, b ) {
	if ( a < b ) {
		return 1;
	}
	if ( a > b ) {
		return -1;
	}
	return 0;
}

arr.push( 'a', 'b', 'c' );
arr.toString();
// returns 'a,b,c'

arr.sort( descending );
arr.toString();
// returns 'c,b,a'
```


<a name="splice"></a>
##### [StringArray.prototype.splice( start, deleteCount[, string0[, string1[,...]]] )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

Adds and/or removes `array` elements and returns any removed elements,

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
arr.toString();
// returns 'a,b,c'

arr.splice( 1, 1 );
// returns ['b']

arr.toString();
// returns 'a,c'

arr.splice( 1, 0, 'b' );
// returns []

arr.toString();
// returns 'a,b,c'
```


===
#### Accessor Methods



<a name="indexof"></a>
##### [StringArray.prototype.indexOf( [str] )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)

Returns the first index of a `StringArray` value equal to a specified value. Returns `-1` if not found.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
arr.indexOf( 'b' );
// returns 1

arr.indexOf( 'd' );
// returns -1
```




<a name="lastindexof"></a>
##### [StringArray.prototype.lastIndexOf( [str] )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf)

Returns the last index of a `StringArray` value equal to a specified value. Returns `-1` if not found.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'b', 'c' );
arr.lastIndexOf( 'b' );
// returns 2

arr.lastIndexOf( 'd' );
// returns -1
```


<a name="slice"></a>
##### [StringArray.prototype.slice( [start[, end]] )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

Extracts a section of a `StringArray` into a new `StringArray`. If not provided, `start` defaults to `0` and `end` defaults to the array length.

``` javascript
var arr = new StringArray(),
	slice;

arr.push( 'a', 'b', 'c', 'd', 'e' );

slice = arr.slice();
slice.toString();
// returns 'a,b,c,d,e'

slice = arr.slice( 2 );
slice.toString();
// returns 'c,d,e'

slice = arr.slice( -3 );
slice.toString();
// returns 'b,c,d,e'

slice = arr.slice( 1, 3 );
slice.toString();
// returns 'b,c'

slice = arr.slice( 1, -1 );
slice.toString();
// returns 'b,c,d'
```

__Note__: returns a new `StringArray` with the same `string` length constraints.






<a name="concat"></a>
##### [StringArray.prototype.concat( value0[, value1[,...]] )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)

Concatenates this `StringArray` with other StringArray(s), array(s) of strings, and/or string(s).

``` javascript
var arr1 = new StringArray(),
	arr2 = new StringArray();

arr1.push( 'a', 'b', 'c' );
arr2.push( 'd', 'e', 'f' );

var arr3 = arr1.concat( arr2 );

arr3 instanceof StringArray;
// returns true

arr3.toString();
// returns 'a,b,c,d,e,f'

var arr4 = arr3.concat( 'beep' );
arr4.toString();
// returns 'a,b,c,d,e,f,beep'

var arr5 = arr1.concat( 'd', ['e','f'] );
arr5.toString();
// returns 'a,b,c,d,e,f'
```

__Note__: returns a new `StringArray` with the same `string` length constraints.





<a name="join"></a>
##### [StringArray.prototype.join( [sep] )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

Joins all `StringArray` values into a single `string`. The default value separator is `','`.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
arr.join();
// returns 'a,b,c'
```

To specify a different separator,

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
arr.join( ' - ' );
// returns 'a - b - c'
```




<a name="tostring"></a>
##### [StringArray.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toString)

Returns a `string` representation of a `StringArray`.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
arr.toString();
// returns 'a,b,c'
```



<a name="tolocalestring"></a>
##### [StringArray.prototype.toLocaleString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toLocaleString)

Returns a locale specific `string` representation of a `StringArray`.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
arr.toLocaleString();
// returns 'a,b,c'
```


<a name="toarray"></a>
##### StringArray.prototype.toArray()

Returns a native `array` representation of a `StringArray`.

``` javascript
var arr = new StringArray();

arr.push( 'a', 'b', 'c' );
arr.toArray();
// returns ['a','b','c']
```

__Note__: changes to the returned `array` will __not__ affect the `StringArray`.




===
#### Iteration Methods




===
## Examples

``` javascript
var StringArray = require( 'string-array' );
```

To run the example code from the top-level application directory,

``` bash
$ node ./examples/index.js
```


===
## Notes

* 	A `StringArray` is __not__ an `Array` instance.
* 	`Object.keys()` will __not__ work as expected. A `StringArray` instance is an `object` which manages an internal `array`.
* 	When applied to a `StringArray`, [`Array.isArray()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)  will return `false`.
* 	While an effort has been made to retain fidelity to the ECMAScript standard for `Arrays`, no guarantee is made that method implementations are spec compliant. This is particularly the case where the spec stipulates additional checks, etc; e.g., `Array#reverse`.
*	`[]` notation does __not__ work as expected. A `StringArray` is an `object`. Using bracket notation will set and return values on the `StringArray` itself, __not__ on the internally managed `array` instance. You can set properties directly on the `StringArray` as you can with any `object`; just ensure that this is treated as distinct from the `StringArray` array data.
*	Working with external methods expecting native `arrays` will require marshalling and unmarshalling of `StringArray` data to and from `arrays`.

	``` javascript 
	var arr = new StringArray();

	arr.push( 'a', 'b', 'c' );

	// Some method expecting native arrays...
	var nativeArray = foo( arr.toArray() );

	// Assuming the native array elements are all strings, marshal the data back into a string array...
	arr = new StringArray();
	arr.push.apply( arr, nativeArray );
	```

===
## Tests

### Unit

Unit tests use the [Mocha](http://mochajs.org/) test framework with [Chai](http://chaijs.com) assertions. To run the tests, execute the following command in the top-level application directory:

``` bash
$ make test
```

All new feature development should have corresponding unit tests to validate correct functionality.


### Test Coverage

This repository uses [Istanbul](https://github.com/gotwarlost/istanbul) as its code coverage tool. To generate a test coverage report, execute the following command in the top-level application directory:

``` bash
$ make test-cov
```

Istanbul creates a `./reports/coverage` directory. To access an HTML version of the report,

``` bash
$ make view-cov
```


---
## License

[MIT license](http://opensource.org/licenses/MIT). 


## Copyright

Copyright &copy; 2015. Athan Reines.


[npm-image]: http://img.shields.io/npm/v/string-array.svg
[npm-url]: https://npmjs.org/package/string-array

[travis-image]: http://img.shields.io/travis/kgryte/string-array/master.svg
[travis-url]: https://travis-ci.org/kgryte/string-array

[coveralls-image]: https://img.shields.io/coveralls/kgryte/string-array/master.svg
[coveralls-url]: https://coveralls.io/r/kgryte/string-array?branch=master

[dependencies-image]: http://img.shields.io/david/kgryte/string-array.svg
[dependencies-url]: https://david-dm.org/kgryte/string-array

[dev-dependencies-image]: http://img.shields.io/david/dev/kgryte/string-array.svg
[dev-dependencies-url]: https://david-dm.org/dev/kgryte/string-array

[github-issues-image]: http://img.shields.io/github/issues/kgryte/string-array.svg
[github-issues-url]: https://github.com/kgryte/string-array/issues
