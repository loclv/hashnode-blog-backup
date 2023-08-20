---
title: "TypeScript - Prisma - prisma-error-enum - An efficient and strict way of using Prisma's error code"
datePublished: Sun Aug 20 2023 16:34:35 GMT+0000 (Coordinated Universal Time)
cuid: clljo4z48000j09micvvd60pq
slug: typescript-prisma-prisma-error-enum-an-efficient-and-strict-way-of-using-prismas-error-code
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/dXYE1d08BiY/upload/ada73796ae69d1225aefc222c91a4e2b.jpeg
tags: typescript, prisma, prisma-error-enum, prisma-error

---

## Problem

In the official document of Prisma - [https://www.prisma.io/docs/reference/api-reference/error-reference#error-codes](https://www.prisma.io/docs/reference/api-reference/error-reference#error-codes), all error codes had been described. But when I want to use it in my project, I must create many constant values. For example:

```typescript
export const UNIQUE_CONSTRAINT_VIOLATION_CODE = 'P2002';
```

When doing this, I must write all the constant values by myself and this can cause some bugs like wrong code. For example, `P2002` can become `P202`. Because we are human, being human can cause bugs!

## Solution

You can use [https://github.com/vinpac/prisma-error-enum](https://github.com/vinpac/prisma-error-enum).

From its document:

* Installation:
    

```bash
pnpm add prisma-error-enum
```

* Usage:
    

```typescript
import { PrismaError } from 'prisma-error-enum'

const createUser = () => {
  try {
    return await prisma.user.create({
      data: {
        email,
      },
    })
  } catch (error) {
    if (
      error.code === PrismaError.UniqueConstraintViolation &&
      error.meta.target[0] === 'email'
    ) {
      throw new BetterError(
        'unique_email',
        'This email is already registered by another user',
        'email',
      )
    }

    throw error
  }
}
```

You can see `PrismaError` is actually a enum of Prisma errors. So we can easily use it by typing "." - the dot symbol after that enum. We can also see all the error codes that exist in Prisma.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692548306897/6c2da493-183b-42c7-bbb7-0f6866e326ee.png align="center")

You also can hover over that enum value to read error code:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692548421810/280f1e59-78f1-41d2-af2e-fec5e2301437.png align="center")

## Risk of `prisma-error-enum` solution

This solution has risks. Just because `prisma-error-enum` is not an official package, so when the official package's error codes are changed, this package becomes outdated. But I think the error code's value is never changed for Prisma versions compatible!

In the future, there is only the possibility that Prisma will add a new error code.