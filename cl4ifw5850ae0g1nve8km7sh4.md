## Tại sao người ta lại yêu thích 💙 TypeScript

Theo khảo sát của [stack-overflow năm 2021](https://insights.stackoverflow.com/survey/2021#overview) và [năm 2020](https://insights.stackoverflow.com/survey/2020#technology-most-loved-dreaded-and-wanted-languages) thì TypeScript đều nằm trong top 3 ngôn ngữ được các developer yêu thích nhất.
Vì sao lại vậy?

Đơn giản là ngôn ngữ nào giúp đỡ nhiều cho developer thì sẽ được ưa thích thôi! Giúp đỡ ở đây có thể hiểu là trên các phương diện _code ít bug_.
Vậy chiến thuật _code ít bug_ của TypeScript ở đây là gì?

## TypeScript

> TypeScript is JavaScript with syntax for types.
> TypeScript is a strongly typed programming language

Đây là 2 điều viết ngắn gọn ở  [trang chủ  TypeScript](https://www.typescriptlang.org/).

TypeScript giúp ta kiểm tra lại types trong các khả năng có thể xảy ra, nhắc nhở chúng ta khi nào thì dùng được biến, hàm, property... ở chỗ này, chỗ khác thì không được phép dùng.

Ta nhắc lại nhược điểm cũng là ưu điểm của JavaScript, rằng JavaScript là 1 trong số những ngôn ngữ [dynamically typed language](https://stackoverflow.com/questions/1517582/what-is-the-difference-between-statically-typed-and-dynamically-typed-languages).

Tức là ví dụ khi định nghĩa 1 biến, ta không cần thiết định nghĩa biến đó thuộc kiểu gì, nó có thể là number, string hay bất cứ cái gì có thể gán được. Sự tiện lợi đó lại khiến ta không biết được nó có thể null, undefined, hay có thể sử dụng property đặc thù được hay không?

Ví dụ sau đây lấy từ [typescriptlang.org](https://www.typescriptlang.org/). Đoạn code JavaScript sau sẽ không có lỗi gì, nhưng sẽ _toang_ khi chạy:

```js
const compact = (arr) => {
  // error: `orr` (not `arr`)
  if (orr.length > 10) {
    // error: `arr` can be anything,
    // so maybe property 'trim' does not exist on it!
    return arr.trim(0, 10)
  }

  return arr
}
```

Đặc thù của con người - developer là xác suất gây ra sai lầm luôn luôn > 0, hay đã là con người thì lúc nào cũng có thể _nhầm nhỡ_. Thế nên cứ dynamically typed, tiện nhưng khó kiểm soát.

Viết lại đoạn code trên với TypeScript, ta sẽ thấy editor báo lỗi từng dòng luôn. Như vậy, lỗi sẽ được giảm tải từ ngay quá trình coding rồi, trước cả khi chạy thử. Điều đó giúp hạn chế bug rất nhiều cho developer!

```ts
const compact = (arr: string[]) => {
  if (arr.length > 10)
    return arr.slice(0, 10)
  return arr
}
```

`arr` được định nghĩa rõ ràng là phải là 1 `Array` mà mỗi phần tử có kiểu là `string`, thế nên nó có thể sử dung method `slice`.  Với TypeScript, mọi thứ đều có type, và type đó là bất biến, hay _tĩnh_, thế nên TypeScript là 1 _statically typed language_.

## JavaScript vs TypeScript

Do JavaScript rât phổ biến, nên TypeScript cũng được thơm lây. Cách phổ biến nhất để code frontend mà sử dụng _statically typed language_, đó là dùng TypeScript. Đối với backend thì ta có bộ đôi Node.js + TypeScript.

| JavaScript | TypeScript |
|------------|------------|
| **code nhanh hơn 🐇**, vì code không cần quan tâm tới type | **code chậm hơn 🐢**, cần quan tâm tới type khi code |
| **dễ học 🐇**, code không cần quan tâm tới type | **học khó hơn 🐢**, cần học cách sử dụng type |
| **khó bảo trì 🤕**, khi hệ thống phức tạp, nhiều thứ không được định nghĩa type | **bảo trì dễ hơn 😎**, mọi thứ được định nghĩa type, dễ hiểu hơn, đặc biệt là định nghĩa params, response API, function... |

Tham khảo thêm từ [JS interview in 2 minutes / Static vs Dynamic typing](https://dev.to/kozlovzxc/js-interview-in-2-minutes-static-vs-dynamic-typing-2d5k).

Điều duy nhất ngăn cả bạn đến với TypeScript là phải bỏ thời gian ra học nó!
