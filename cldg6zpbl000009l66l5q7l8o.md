# Typescript - ReactJS - Property 'directory' does not exist on type definition

## 🍇 Problem

When I try to upload a directory by using the `input` element with *NextJS*, *ReactJS* and TypeScript. A TypeScript error occurs:

> Type '{ type: "file"; directory: string; multiple: true; webkitdirectory: string; }' is not assignable to type 'DetailedHTMLProps&lt;InputHTMLAttributes&lt;HTMLInputElement&gt;, HTMLInputElement&gt;'.  
> Property 'directory' does not exist on type 'DetailedHTMLProps&lt;InputHTMLAttributes&lt;HTMLInputElement&gt;, HTMLInputElement&gt;'.ts(2322)

I think this is a weird error because the `directory` is a normal property in the HTML input element. 🥲

I checked out the ReactJS type definition by using `ctrl + click` on the input element attribute name and found out that the directory property is not defined. 🥲

## 🌾 The Solution

After some research, I found out that the directory property must be defined by using the following code. `src/types/input-html.d.ts` :

```typescript
/* eslint-disable @typescript-eslint/naming-convention */
export {};

declare module 'react' {
  interface InputHTMLAttributes<T> extends HTMLAttributes<T> {
    // extends React's HTMLAttributes
    directory?: string;
    webkitdirectory?: string;
  }
}
```

Now, the error is gone. ✨

We used the `export {}` line in our `.d.ts` file to mark it as an external module. `directory` and `webkitdirectory` are should be string type and optional properties.

## 🌱 Reference

* [https://stackoverflow.com/questions/72787050/typescript-upload-directory-property-directory-does-not-exist-on-type](https://stackoverflow.com/questions/72787050/typescript-upload-directory-property-directory-does-not-exist-on-type)
    
* [github.com/facebook/react/issues - webkitdirectory and directory with TypeScript](https://github.com/facebook/react/issues/3468#issuecomment-1031366038)
    
* [https://bobbyhadz.com/blog/typescript-process-env-type](https://bobbyhadz.com/blog/typescript-process-env-type)