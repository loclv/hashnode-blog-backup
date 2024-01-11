---
title: "How to force developers in a project to use Bun not pnpm npm or yarn 😹"
seoTitle: "How to force developers in a project to use Bun not pnpm npm or yarn"
seoDescription: "How to force developers in a project to use Bun not pnpm npm or yarn"
datePublished: Sat Dec 23 2023 23:02:59 GMT+0000 (Coordinated Universal Time)
cuid: clqio1y3f000009i84x4abl7m
slug: how-to-force-developers-in-a-project-to-use-bun-not-pnpm-npm-or-yarn
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/vv-oEGlN-4E/upload/1e6a3f9720a1965d551fc31ef9fd6a7b.jpeg
tags: bun

---

## How?

Create `/path/to/my/project/.npmrc`:

```bash
touch .npmrc
```

Update `.npmrc` with the configuration below:

```conf
engine-strict=true
```

Add package manager configuration to `package.json`:

```json
{
  "engines": {
   "npm": "Please use Bun",
   "yarn": "Please use Bun",
   "pnpm": "Please use Bun",
   "bun": ">=1.0.19"
  }
}
```

## Reference

- <https://docs.npmjs.com/cli/v10/configuring-npm/npmrc>
- <https://www.freecodecamp.org/news/how-to-force-use-yarn-or-npm/>
