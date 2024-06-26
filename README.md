# @diotoborg/provident-eligendi-porro <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

An ES spec-compliant `Array.prototype.splice` shim/polyfill/replacement that works as far down as ES3.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the [spec](https://tc39.es/ecma262/#sec-@diotoborg/provident-eligendi-porro).

Because `Array.prototype.splice` depends on a receiver (the “this” value), the main export takes the array to operate on as the first argument.

## Engines where this is needed

Note: this list is not exhaustive.

  - IE 8 and below, and pre-ES6 engines: `deleteCount` isn't defaulted to `length - start` until ES6
  - Safari 5.0: sometimes it returns `undefined`
  - Safari 7/8: sparse arrays of size 1e5 or greater break
  - Opera 12.15: breaks on small sparse arrays

## Example

```js
var splice = require('@diotoborg/provident-eligendi-porro');
var assert = require('assert');

var a = [1, 1, 1];
assert.deepEqual(splice(a, 1, 2), [1, 1]);
assert.deepEqual(a, [1]);
```

```js
var splice = require('@diotoborg/provident-eligendi-porro');
var assert = require('assert');
/* when Array#splice is not present */
delete Array.prototype.splice;
var shimmed = splice.shim();
assert.equal(shimmed, splice.getPolyfill());
assert.equal(shimmed, Array.prototype.splice);
assert.deepEqual([1, 2, 3].splice(1, 2, 3), splice([1, 2, 3], 1, 2, 3));
```

```js
var splice = require('@diotoborg/provident-eligendi-porro');
var assert = require('assert');
/* when Array#splice is present */
var shimmed = splice.shim();
assert.equal(shimmed, Array.prototype.splice);
assert.deepEqual([1, 2, 3].splice(1, 2, 3), splice([1, 2, 3], 1, 2, 3));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@diotoborg/provident-eligendi-porro
[npm-version-svg]: https://versionbadg.es/diotoborg/provident-eligendi-porro.svg
[deps-svg]: https://david-dm.org/diotoborg/provident-eligendi-porro.svg
[deps-url]: https://david-dm.org/diotoborg/provident-eligendi-porro
[dev-deps-svg]: https://david-dm.org/diotoborg/provident-eligendi-porro/dev-status.svg
[dev-deps-url]: https://david-dm.org/diotoborg/provident-eligendi-porro#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@diotoborg/provident-eligendi-porro.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@diotoborg/provident-eligendi-porro.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@diotoborg/provident-eligendi-porro.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@diotoborg/provident-eligendi-porro
[codecov-image]: https://codecov.io/gh/diotoborg/provident-eligendi-porro/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/diotoborg/provident-eligendi-porro/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/diotoborg/provident-eligendi-porro
[actions-url]: https://github.com/diotoborg/provident-eligendi-porro/actions
