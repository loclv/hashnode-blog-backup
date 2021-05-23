## Cách nhanh nhất chạy 1 file typescript trên local 🦕

Tóm tắt: Sử dụng [deno](https://deno.land/).

## Về `deno` 🦕

Tác giả `Node.js` - [Ryan Dahl](https://en.wikipedia.org/wiki/Ryan_Dahl) từ những nhược điểm của `Node.js` đã viết lại 1 `Runtime system
` bằng [Rust](https://www.rust-lang.org/) vẫn dựa trên [V8](https://v8.dev/), đó chính là [deno](https://deno.land/).

Ưu điểm lớn nhất của `deno`, theo mình đó là chạy trực tiếp `typescript` mà không cần thông qua 1 bộ chuyển đổi từ `file.ts` sang `file.js`.

## `Chạy ngay đi`

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

## Chạy

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

![deno-run](https://cdn.hashnode.com/res/hashnode/image/upload/v1621074526975/lOHaAvhF0.png)

---

Photo by <a href="https://unsplash.com/@jon_chng?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Jonathan Chng</a> on <a href="https://unsplash.com/s/photos/run?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
