---
title: "Web - Use console.log and Vite Env Variables to show building time on browser console"
seoTitle: "Web - Use console.log and Vite Env Variables to show building time"
seoDescription: "Web - Use console.log and Vite Env Variables to show building time on browser console"
datePublished: Tue Nov 28 2023 16:36:00 GMT+0000 (Coordinated Universal Time)
cuid: clpik7zn6000409k399vef1kn
slug: web-use-consolelog-and-vite-env-variables-to-show-building-time-on-browser-console
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/k7rZ8wTfABA/upload/fb99fd1ea8818c005f7450d26cb67a5a.jpeg
tags: js

---

## Create `env.d.ts` file

```bash
cd src
touch env.d.ts
```

```typescript
/// <reference types="vite/client" />

interface ImportMetaEnv {
  readonly VITE_BUILD_TIME: string;
  // more env variables...
}

interface ImportMeta {
  readonly env: ImportMetaEnv;
}
```

## Logs at `main.tsx`

```typescript
// eslint-disable-next-line no-console
console.log("BUILD_TIME: ", import.meta.env.VITE_BUILD_TIME);
```

## Add environment variables to `package.json`

```diff
   "scripts": {
-    "dev": "vite",
-    "build": "vite build",
+    "dev": "VITE_BUILD_TIME=\"$(date)\" vite",
+    "build": "VITE_BUILD_TIME=\"$(date)\" vite build",
```

You can use [cross-env](https://www.npmjs.com/package/cross-env) package for Windows.

## Reference

* [https://vitejs.dev/guide/env-and-mode](https://vitejs.dev/guide/env-and-mode)
    
* [https://stackoverflow.com/questions/25112510/how-to-set-environment-variables-from-within-package-json](https://stackoverflow.com/questions/25112510/how-to-set-environment-variables-from-within-package-json)
    
* [https://www.npmjs.com/package/cross-env](https://www.npmjs.com/package/cross-env)
    
* [https://stackoverflow.com/questions/49741967/passing-date-to-package-json-script](https://stackoverflow.com/questions/49741967/passing-date-to-package-json-script)