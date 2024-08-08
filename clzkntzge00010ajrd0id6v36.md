---
title: "Typescript - get Type from object with `as cons` syntax and use it like an enum type"
seoTitle: "Typescript get Type from object with as cons syntax and like enum"
seoDescription: "Typescript - get Type from object with `as cons` syntax and use it like an enum type"
datePublished: Thu Aug 08 2024 02:29:41 GMT+0000 (Coordinated Universal Time)
cuid: clzkntzge00010ajrd0id6v36
slug: typescript-get-type-from-object-with-as-cons-syntax-and-use-it-like-an-enum-type
tags: typescript

---

## Typescript - get Type from object with `as cons` syntax and use it like an enum type

You can read more about Objects vs Enums at TypeScript's document: <https://www.typescriptlang.org/docs/handbook/enums.html#objects-vs-enums>.

Document's example:

```ts
const enum EDirection {
  Up,
  Down,
  Left,
  Right,
}

const ODirection = {
  Up: 0,
  Down: 1,
  Left: 2,
  Right: 3,
} as const;

EDirection.Up;
// EDirection.Up = 0

ODirection.Up;
// ODirection.Up = 0

// Using the enum as a parameter
function walk(dir: EDirection) {}
```

To get Type from object with `as cons` syntax and use it like an enum type, just do like document's example:

```ts
type Direction = (typeof ODirection)[keyof typeof ODirection];

function run(dir: Direction) {}
```
