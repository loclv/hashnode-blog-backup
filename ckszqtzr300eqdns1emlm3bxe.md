## Bạn yêu TypeScript nhưng đại ca khách hàng lại muốn bạn dùng JavaScript? 🤔 Enum in JS

## Lợi ích của `Enums`

Với những ai yêu TypeScript thì [Enums](https://www.typescriptlang.org/docs/handbook/enums.html) là một tính năng khá cơ bản.
Ví dụ:

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}
```

Ưu điểm khi dùng `Enums` đó là:

- Không phải comment các con số vô nghĩa, ví dụ như trên là `0` tương ứng với `Up`.

- Nếu dùng kiểu `string` để định nghĩa dữ liệu thì không tối ưu về performance như đối với kiểu `number`.

- Với 2 điều trên thì bạn không phải đánh đổi giữa hiệu năng và khả năng đọc hiểu của code.

- Khi gõ `Direction.` thì editor sẽ tự động suggest 4 thuộc tính bên trên,
tránh lỗi đánh máy hay chính tả như khi dùng với kiểu dữ liệu `string`.
Ví dụ khi định nghĩa bởi `string` `Up` mà gõ nhầm thành `Up-` thì chẳng editor nào cứu được cả.

- Thống nhất định nghĩa của giá trị constant - giá trị bất biến trong App, thậm chí cả backend và frontend nếu cùng dùng TypeScript.

![hair flip](https://media.giphy.com/media/8gUuSM6DgGLtYIBsOK/giphy.gif)

## Vấn đề khi tạo Enum object trong JS

Trong JS, nếu các bạn chưa biết về tham biến và tham trị, khái niệm `Immutable` và `mutation` thì có thể tham khảo bài viết [Understanding Immutability in JavaScript](https://css-tricks.com/understanding-immutability-in-javascript/).

Khi ta khai báo 1 biến là `object` dạng `const`:

```js
const Direction = {
  Up: 0,
  Down: 1
}
```

Tuy nhiên, ta vẫn thay đổi được thuộc tính của `object` trên. Vì cái `const` chỉ là cái địa chỉ tham chiếu tới `object` chứ không phải giá trị từng thuộc tính.

```js
Direction.Down = 2
console.log('Direction: ', Direction)
// output: Direction:  {Up: 0, Down: 2}
```

## Cách tạo ra `enum in javascript`

Sau khi search với từ khóa `enum in javascript` thì mình đã tìm được câu hỏi [này](https://stackoverflow.com/questions/287903/how-can-i-guarantee-that-my-enums-definition-doesnt-change-in-javascript) trên `stackoverflow`.

Giải pháp đóng băng object đó là dùng [Object.freeze](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze).

```js
const Direction = Object.freeze({Up: 0, Down: 1})
```

Khi ta thay đổi giá trị thuộc tính của object `DaysEnum`

```js
Direction.Up = 33
// Throws an error in strict mode

console.log('Direction: ', Direction)
// output: Direction:  {Up: 0, Down: 1}
```

Vậy là ta đã đạt được mục đích, `Direction` Object không bị thay đổi thuộc tính (property) trong quá trình chạy. Ngoài ra `Object.freeze` cũng dùng được với `Array`.

Tuy nhiên lưu ý quan trọng là đối với kiểu data mà object cha con:

```js
const Direction = Object.freeze({Up: 0, Down: {prop: 1}})
Direction.Down.prop = 33

console.log('Direction: ', Direction)
// output: Direction:  {Up: 0, Down: {prop: 33}}
```

Thì `Object.freeze` vẫn bó tay nhé.

![what?](https://media.giphy.com/media/toB3AnUDkqE3GENKx0/giphy.gif)

---

Photo by <a href="https://unsplash.com/@ankhesenamunnn?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Ankhesenamun</a> on <a href="https://unsplash.com/s/photos/freeze?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
