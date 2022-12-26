# About ES Modules in Node.js

### What are ES Modules in Node.js?

In Node.js, the term "ES Modules" refers to a standardized way of organizing and managing JavaScript code using the import and export statements introduced in ECMAScript 2015 (also known as ES6).

ES Modules allow developers to split their code into smaller, more reusable pieces, and then import and use those pieces in other parts of their application. They can be used to import functions, objects, and other values from external modules, as well as to export values from the current module to be used by other modules.

From the official Node.js documentation, ES Modules are:

> ECMAScript modules are [the official standard format](https://tc39.github.io/ecma262/#sec-modules) to package JavaScript code for reuse. Modules are defined using a variety of [`import`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) and [`export`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) statements.

Node.js has two module systems:

* *CommonJS* modules - CJS
    
* *ECMAScript* modules - ESM
    

CommonJS modules are simply not ES Modules! It imports and exports JavaScript code using the `require()` and `module.exports` statements.

From [Node.js V14.0.0](https://github.com/nodejs/node/blob/main/doc/changelogs/CHANGELOG_V14.md#14.0.0), ES Modules are stable. However, they do not default modules in Node.js. The default modules are still CommonJS modules. So, How can we use ES Modules in Node.js?

### `How` can we use ES Modules in Node.js?

We can tell Node.js to use the ECMAScript modules loader via:

* Rename `.js` file extension to `.mjs` file extension.
    
* Set the `package.json` [`"type"`](https://nodejs.org/api/packages.html#type) field to `"module"` - `"type": "module"`
    
* Set the `--input-type=module` flag when running Node CLI
    

### Basic example

ES module exports a function:

```javascript
// addTwo.mjs
const addTwo = (num) => {
  return num + 2;
}

export { addTwo };
```

```js
// app.mjs
import { addTwo } from './addTwo.mjs';

// Prints: 6
console.log(addTwo(4));
```

`'./addTwo.mjs'` is actually exporting an object that contains a property named `addTwo`. When importing this module, we are using [destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) feture to access the `addTwo` property.

### Why we are moving to ES Modules?

[This blog post](https://dev.to/gaosun/migrate-a-60k-loc-typescript-nodejs-repo-to-esm-and-testing-become-4x-faster-12-5f82) explains the benefits of ES Modules clearly!

* Compatibility with new packages
    
* More readable code and better performance
    

If you are using an older version of Node.js or a runtime that does not support ESM, you may not be able to use ESM packages directly. However, many ESM packages provide a CommonJS version of their package that can be used with the `require()` function and the `module.exports` object, which is supported by most JavaScript runtimes.

### References

* [https://dev.to/gaosun/migrate-a-60k-loc-typescript-nodejs-repo-to-esm-and-testing-become-4x-faster-12-5f82](https://dev.to/gaosun/migrate-a-60k-loc-typescript-nodejs-repo-to-esm-and-testing-become-4x-faster-12-5f82)
    
* [https://nodejs.org/api/esm.html#differences-between-es-modules-and-commonjs](https://nodejs.org/api/esm.html#differences-between-es-modules-and-commonjs)
    
* [https://nodejs.org/api/esm.html#modules-ecmascript-modules](https://nodejs.org/api/esm.html#modules-ecmascript-modules)
    
* [https://chat.openai.com/](https://chat.openai.com/)