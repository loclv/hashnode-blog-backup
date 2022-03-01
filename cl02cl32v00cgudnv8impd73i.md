## NodeJs - Hiểu rõ hơn về process.argv 🍾 và ứng dụng

# NodeJs - Hiểu rõ hơn về process.argv và ứng dụng

Để hiểu rõ về nó thì tốt nhất là ta nên *chạy ngay đi*!

## Chạy ngay đi

Tạo 1 file `process-args.js`:

```js
process.argv.forEach((val, index) => {
  console.log(`${index}: ${val}`);
});

```

Hoặc là load an ES module, set `"type": "module"` trong package.json hoặc lấy tên file là `process-args.mjs`:

```js
import { argv } from 'process';

// print process.argv
argv.forEach((val, index) => {
  console.log(`${index}: ${val}`);
});

```

Chạy:

```sh
node process-args one two=three four
```

Dưới đây là output từ local của mình:

```txt
0: /home/{user-name}/.fnm/node-versions/v16.13.0/installation/bin/node
1: /home/{user-name}/w/blogs/process-args.js
2: one
3: two=three
4: four
```

## Giải thích

`process.argv` trả về 1 mảng gồm các string chứa lần lượt:

0. PATH của NodeJs
1. PATH của file source code
2. Từ vị trí này là các argument được phân cách bằng dấu cách
3. ...

`process.argv` giúp truyền mảng giá trị từ command-line dưới dạng string.

## Cách lấy mảng các giá trị khi người dùng gõ command-line argument không theo 1 thứ tự nhất định

Để các value này đúng thứ tự ta có thể áp dụng nguyên tắc đánh dấu value của rất nhiều CLI khi sử dụng options.

Ví dụ [NextJs CLI](https://nextjs.org/docs/api-reference/cli) đánh dấu giá trị *port* bằng cách đặt trước giá trị *4000* 1 argument nữa là `-p`.

```sh
node process-args -p 4000 -H 192.168.1.2
```

Cách xử lý đầu vào như trên là lấy argument kế bên mốc được đánh dấu:

```js
const args = process.argv;
console.log('🚀 ~ args', args);

let port;
let host;

// first item is NodeJs PATH, second is src PATH
for (let i = 2; i < args.length; ++i) {
  const arg = args[i];
  const nextArg = args[i + 1];

  if (arg === '-p') {
    port = Number(nextArg);
  } else if (arg === '-H') {
    host = nextArg;
  }
}

console.log('🍾 ~ port', port);
console.log('🌎 ~ host', host);

```

Output:

```txt
🚀 ~ args [
  '/home/{user}/.fnm/node-versions/v16.13.0/installation/bin/node',
  '/home/{user}/w/blogs/process-args.js',
  '-p',
  '4000',
  '-H',
  '192.168.1.2'
]
🍾 ~ port 4000
🌎 ~ host 192.168.1.2
```

Về convention của CLI command-language syntax ta có thể tham khảo [Angular CLI command-language syntax](https://angular.io/cli#cli-command-language-syntax).
Có thể đặt tên option theo *camelCase* or *dash-case*, như --myOptionName và --my-option-name.

## Tham khảo

- [nodejs.org - parse command line arguments](https://nodejs.org/en/knowledge/command-line/how-to-parse-command-line-arguments/)
- Comment ghi trong `node_modules/@types/node/process.d.ts`, phần giải thích cho `argv: string[];`.

---

Photo by [Krzysztof Niewolny](https://unsplash.com/@epan5?utm_source=Hashnode&utm_medium=referral) on Unsplash.