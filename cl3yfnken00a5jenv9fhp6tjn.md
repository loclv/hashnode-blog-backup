## Run TypeScript file globally 🌠 with ts-node

# Run TypeScript file globally with ts-node

## Globally install `ts-node`

```sh
pnpm install -g typescript ts-node tslib @types/node
```

- [tslib](https://github.com/Microsoft/tslib) is a runtime library for TypeScript that contains all of the TypeScript helper functions.
- [@types/node](https://www.npmjs.com/package/@types/node) contains type definitions for Node.js.

## Prepare a simple sample

Create a ts file:

```sh
touch test.ts
```

Write a simple sample:

```ts
const teamName: string = '🦆🦆🦆';

console.log('🌊', teamName);
```

## Run ts file everywhere

```ts
ts-node test.ts
```

Expected output is "🌊 🦆🦆🦆".
