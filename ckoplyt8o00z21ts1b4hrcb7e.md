---
title: "NodeJS - Cách nhanh nhất chạy 1 file typescript trên local 🦕"
seoTitle: "Cách nhanh nhất chạy 1 file typescript trên local: deno"
seoDescription: "Cách nhanh nhất chạy 1 file typescript trên local: deno
deno.land"
datePublished: Sat May 15 2021 10:30:08 GMT+0000 (Coordinated Universal Time)
cuid: ckoplyt8o00z21ts1b4hrcb7e
slug: nodejs-cach-nhanh-nhat-chay-1-file-typescript-tren-local
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1621778209788/TTMncY_FI.jpeg
tags: typescript, tsx

---

Tóm tắt: Sử dụng [tsx](https://github.com/esbuild-kit/tsx) - ⚡ TypeScript Execute.

Cách khác là sử dụng [deno](https://deno.land/).

## Sử dụng [tsx](https://github.com/esbuild-kit/tsx) - ⚡

`tsx` là 1 CLI command, chạy TypeScript và ESM. Nó sẽ compile ra `commonjs` hoặc `module` package types và chạy luôn code JS đã compiled đó 1 cách liền mạch. Không output JS source-code như [tsc - TS Compiler](https://www.typescriptlang.org/docs/handbook/compiler-options.html).

`tsx` sử dụng [esbuild](https://esbuild.github.io/) và quan trọng là `esbuild` không có type-checking nên tất nhiên là nhanh hơn các compiler truyền thống khác. Chính vì thế ta sẽ phải type-checking riêng biệt bằng IDE (như VSCode), hay `tsc --noEmit` command.

Vì thế nên sử dụng `tsx` khi:

* Chắc chắn rằng đã type-checking trước khi chạy `tsx`.
    

## Sử dụng [deno](https://deno.land/) 🦕

### Về `deno` 🦕

Tác giả `Node.js` - [Ryan Dahl](https://en.wikipedia.org/wiki/Ryan_Dahl) từ những nhược điểm của `Node.js` đã viết lại 1 `Runtime system` bằng [Rust](https://www.rust-lang.org/) vẫn dựa trên [V8](https://v8.dev/), đó chính là [deno](https://deno.land/).

Ưu điểm lớn nhất của `deno`, theo mình đó là chạy trực tiếp `typescript` mà không cần thông qua 1 bộ chuyển đổi từ `file.ts` sang `file.js`.

Chạy ngay đi!

### Cài đặt `deno`

Cách cài đặt `deno` cụ thể có tại [đây](https://deno.land/).

MacOS:

```sh
brew install deno
```

Linux (ví dụ như Ubuntu):

```sh
sudo snap install deno
```

### Chạy

Tạo 1 file `typescript` mà bạn muốn chạy, ví dụ `add.ts` với nội dung dưới đây.

```typescript
const add = (num1: number, num2: number): number => {
  return num1 + num2;
};

console.log("🚀 ~ file: add.ts ~ line 5 ~ add(2, 3)", add(2, 3));
```

Chạy command:

```sh
deno run ./add.ts
```

Kết quả:

![deno-run](https://cdn.hashnode.com/res/hashnode/image/upload/v1621074526975/lOHaAvhF0.png align="left")

---

Photo by [Jonathan Chng](https://unsplash.com/@jon_chng?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/run?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)