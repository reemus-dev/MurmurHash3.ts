# MurmurHash3.ts

![NPM](https://img.shields.io/npm/l/murmurhash3.ts?style=for-the-badge)
![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/reemus-dev/MurmurHash3.ts/release.yml?style=for-the-badge)
![npm bundle size](https://img.shields.io/bundlephobia/min/murmurhash3.ts?style=for-the-badge)
![npm](https://img.shields.io/npm/v/murmurhash3.ts?style=for-the-badge)
![npm type definitions](https://img.shields.io/npm/types/murmurhash3.ts?style=for-the-badge)

[![NPM Package](https://img.shields.io/npm/v/murmurHash3.js?style=for-the-badge)](https://www.npmjs.com/package/murmurhash3.js)
[![MIT License](https://img.shields.io/github/license/karanlyons/murmurHash3.js?style=for-the-badge)](https://github.com/karanlyons/murmurHash3.js/blob/master/LICENSE)
[![Build Status](https://img.shields.io/travis/com/karanlyons/murmurHash3.js?style=for-the-badge)](https://travis-ci.com/karanlyons/murmurHash3.js)
[![Coverage Status](https://img.shields.io/coveralls/github/karanlyons/murmurHash3.js?style=for-the-badge)](https://coveralls.io/github/karanlyons/murmurHash3.js)


## Usage

```javascript
> const murmurHash3 = require('murmurhash3.js');

// Return a 32bit hash as an unsigned integer:
> murmurHash3.x86.hash32("I will not buy this record, it is scratched.");
  2832214938

// Return a 128bit hash as a hexadecimal string:
> murmurHash3.x86.hash128("I will not buy this tobacconist's, it is scratched.");
  '9b5b7ba2ef3f7866889adeaf00f3f98e'
> murmurHash3.x64.hash128("I will not buy this tobacconist's, it is scratched.");
  'd30654abbd8227e367d73523f0079673'

// Specify a starting seed (defaults to 0x0):
> murmurHash3.x86.hash32("My hovercraft is full of eels.", 25);
  2520298415

// Hash buffers:
> const buf = new Uint8Array(Array.from({ length: 256}, (_, i) => i));
> murmurHash3.x86.hash32(buf);
  3825864278
> murmurHash3.x86.hash128(buf);
  Uint8Array [44, 86, 200, 143, 219, 69, 3, 223, 211, 82, 178, 26, 73, 76, 162, 192];

// Progressively hash streams of data as either buffers or strings:
> const state32 = murmurHash3.x86.hash32(buf.slice(0, 127), 0x0, false);
> murmurHash3.x86.hash32(buf.slice(127), state32, true);
  3825864278
> const state128 = murmurHash3.x86.hash128(buf.slice(0, 127), 0x0, false);
> murmurHash3.x86.hash128(buf.slice(127), state128, true);
  Uint8Array [44, 86, 200, 143, 219, 69, 3, 223, 211, 82, 178, 26, 73, 76, 162, 192];
```


## API

```javascript
murmurHash3 = {
  strToBuf: (str: string = ""
):
Uint8Array,
  bufToHex
:
(buf: Uint8Array = new Uint8Array(0)
):
string,
  x86
:
{
  hash32: (
    buf: Uint8Array | string = new Uint8Array(0),
    state
:
  U32 | X86Hash32State = 0x0,
    finalize
:
  boolean = true,
):
  U32 | X86Hash32State,
    hash128
:
  (
    buf: Uint8Array | string = new Uint8Array(0),
    state
:
  U32 | X86Hash128State = 0x0,
    finalize
:
  boolean = true
):
  Uint8Array | string | X86Hash128State,
}
,
x64: {
  hash128: (
    buf: Uint8Array | string = new Uint8Array(0),
    state
:
  U32 | X64Hash128State = 0x0,
    finalize
:
  boolean = true
):
  Uint8Array | string | X64Hash128State,
}
,
}
```


- - -

Requires [`TextEncoder`](https://caniuse.com/#feat=textencoder),
[Typed Arrays & `DataView`](https://caniuse.com/#feat=typedarrays), and additional
[es6/es2015](https://caniuse.com/#feat=es6) features; bring your own transpiler and
polyfills to target the past.
