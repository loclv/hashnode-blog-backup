## NodeJs - Hỏi nhanh - Nếu có process.exit trong khối try finally thì finally còn được thực thi hay không?

## Câu hỏi và trả lời

Trong khối [try - catch - finally](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch#syntax) của NodeJs thì khối *finally* đóng vai trò như 1 phần code chung dành cho cả khối *try* và khối *catch*. Với ý nghĩa kiểu như:

> Dù chuyện gì xảy ra đi nữa thì cuối cùng (finally) cũng phải làm gì đó!

Dù xảy ra lỗi chẳng hạn. Tuy nhiên, nếu trong khối *try* có `process.exit(1);` chẳng hạn thì theo bạn, khối *finally* có được thực thi không?

Ví dụ đoạn code sau đây thì *finally, cleanup* có được log ra không?

```js
try {
  console.log('START');
  process.exit(1);
  console.log('END');
} finally {
  console.log('finally, cleanup');
}
```

Chúng ta cùng chạy thử xem:

```sh
node finally.js
```

Kết quả là *finally, cleanup* không được log ra, chỉ có *START* là output.

Như vậy nếu trong khối *try* có `process.exit(1);` chẳng hạn thì khối *finally* không được thực thi.

## Giải thích

Theo như [nodejs.dev - how-to-exit-from-a-nodejs-program](https://nodejs.dev/learn/how-to-exit-from-a-nodejs-program), thì:

> When Node.js runs this line, the process is immediately forced to terminate.

> This means that any callback that's pending, any network request still being sent, any filesystem access, or processes writing to  `stdout`  or  `stderr`  - all is going to be ungracefully terminated right away.

Tức là tất cả các promise hay event (những thứ còn dang dở) chưa được thực hiện hoặc nằm trong [event-loop](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/#event-loop-explained) không được thực thi. Ngay cả nó nằm bên trong 1 khối try - catch - finally.
