## TypeScript - Data Type - Never

## Data Type - `Never` trong TypeScript

> A function returning 'never' cannot have a reachable end point.

`never` là 1 type không tồn tại trong JavaScript.

`never` hay _kiểu không bao giờ_, được định nghĩa là kiểu trả về khi mà bạn chắc chắn là không thể trả về được 1 giá trị nào đó do vòng lặp vô hạn hay chủ động dừng, không thực hiện tiếp.

Ví dụ 1 function không thực hiện được hết, hay function đó luôn bị dừng do throw 1 exception - ngoại lệ:

```ts
const throwError = (errorMsg: string): never => {
  throw new Error(errorMsg);
};

const keepProcessing = (): never => {
  while (true) {
    console.log('I always does something and never ends.');
  }
};
```

`throwError` và `while (true)` sẽ ngăn function thực hiện xong, thế nên nó tất nhiên không bao giờ có thể return void. Và kiểu function này, ta có thể đặt kiểu trả về là `never`.

Dưới đây là 1 ví dụ khác của `never`:

```ts
let something: void = null;
let nothing: never = null; // Error: Type 'null' is not assignable to type 'never'
```

Kiểu `void` thì gán được nếu giá trị đó là `null`, còn `never` thì không. Bởi vì trả về `null` thì bản chất là vẫn trả về được 1 giá trị đó là `null`.

## Ứng dụng

### Hữu dụng khi báo lỗi

Nếu bạn code nhiều TypeScript thì sẽ quen mặt thằng `never` này ở thông báo lỗi khi build project. Bởi lẽ `never` thường đi kèm với việc có gì đó đang không thể return được.

### Sử dụng với Generic types

Khi muốn tạo ra 1 [generic types](https://www.typescriptlang.org/docs/handbook/2/generics.html#generic-types) với input type bất kỳ _ngoại trừ_ 1 số types nào đó thì ta có thể viết như sau:

```ts
type TNonNullable<T> = T extends null | undefined ? never : T;

// 🚫 error: Type 'undefined' is not assignable to type 'never'.
const value: TNonNullable<undefined> = undefined;
console.log('🚀 ~ value', value);

// ---
// another example:
type TNotANumber<T> = T extends number ? never : T;

// 🚫 error: Type 'number' is not assignable to type 'never'.
const notANumberValue: TNotANumber<number> = 1;
console.log('🚀 ~ notANumberValue', notANumberValue);
```

`TNonNullable` sẽ không chấp nhận `null | undefined` và `TNotANumber` cũng không chấp nhận 1 number type.

---

Tham khảo:

- [tutorialsteacher typescript-never](https://www.tutorialsteacher.com/typescript/typescript-never)

- [stackoverflow - understanding-the-never-type-in-typescript](https://stackoverflow.com/questions/40225384/understanding-the-never-type-in-typescript-2)
