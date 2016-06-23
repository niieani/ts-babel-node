# TypeScript-Babel Node

This package enables Babel compilation of TypeScript compilation output through a registration function and a Node binary proxy.

### Why do I want this?

Because you want `ts-node` to run `async`/`await` code, but TypeScript will only compile `async`/`await` to ES6 and Node 5.x doesn't support all of ES6 yet. So you need Babel to bridge that gap.

`ts-babel-node` wraps `ts-node` so you can do just that. Run the `ts-babel-node` executable exactly the same way you'd run `ts-node` and require `ts-babel-node/register` instead of `ts-node/register`.

## Installation

### Command Line

To use `ts-babel-node` on the command line, install this package globally. Be sure to include whichever version of TypeScript you want to compile against.

```
$ npm install --global ts-babel-node typescript babel-core babel-polyfill babel-preset-es2015 ts-node

$ ts-babel-node my-file.ts
```

### Library

To include `ts-babel-node` as a register function, install this package as a development dependency. Be sure to include whichever version of TypeScript you want to compile against.

```
$ npm install --save-dev ts-babel-node typescript babel-core babel-polyfill babel-preset-es2015 ts-node
```

## Usage

### Command Line

Since `ts-babel-node-extendable` is a wrapper around `ts-node`, anything you can do with `ts-node` works with `ts-babel-node-extendable`. See [`ts-node`'s docs](https://github.com/TypeStrong/ts-node/#usage) for more details.

### Library

`ts-babel-node-extendable` exposes two APIs. The first is a wrapper around the `ts-node` API.

```js
// $ node this-file.js

require('ts-babel-node-extendable').register(/* ts-node options, extra babel property for babel options */);
// Or
require('ts-babel-node-extendable/register');
```

You can also use this with the `--require ` option on `node`.

```
$ node --require ts-babel-node/register my-file.ts
```

The second API only adds the babel-compilation step. This is useful if your code is run from `ts-node`, as is the case in the [gulp](#gulp) scenario.

```js
// $ ts-node this-file.js

require('ts-babel-node-extendable').registerBabel();
// Or
require('ts-babel-node-extendable/register-babel');
```

### Mocha

```
$ mocha --require ts-babel-node-extendable/register [...args]
```

### Tape

```
$ ts-babel-node-extendable node_modules/.bin/tape [...args]
```

### Gulp

In your `gulpfile.ts` (note, `.ts`, not `.js`):

```
import 'ts-babel-node-extendable/register-babel';
// ...
```

Then use `gulp` normally. Keep in mind that the babel traspiler won't be active in your `gulpfile.ts`, but will be running in all your imports. 
