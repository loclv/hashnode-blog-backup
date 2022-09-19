## TypeScript - Data Type - Never 🚫

## Data Type - `Never` trong TypeScript

### Định nghĩa

> A function returning 'never' cannot have a reachable end point.

`never` là 1 type không tồn tại trong JavaScript.

`never` hay _kiểu không bao giờ_, được định nghĩa là kiểu trả về khi mà bạn chắc chắn là không thể trả về được 1 giá trị nào đó do vòng lặp vô hạn hay chủ động dừng, không thực hiện tiếp.

### Ví dụ với function

Ví dụ, 1 function không thực thi được hết, không tới được cú pháp đóng function (`}`), hay function đó luôn bị dừng do throw 1 exception - ngoại lệ:

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

Trên là ví dụ với function, dưới đây là 1 ví dụ khác của `never` đối với 1 biến.

### Ví dụ với biến

```ts
let randomNum: null | number = null;

// 🚫 Error: Type 'null' is not assignable to type 'never'
let nothing: never = null;
```

Kiểu `null | number` thì gán được nếu giá trị đó là `null`, vì bản thân `randomNum` vẫn "trả về" `null`.
Như vậy, bản chất của biến là vẫn trả về được 1 giá trị nào đó.

Còn `never` thì "không trả về", điều này hoàn toàn trái ngược với cách hoạt đông của 1 biến đã có 1 giá trị nào đó.
Điều đó lý giải vì sao TS báo lỗi:

> 🚫 Error: Type 'null' is not assignable to type 'never'

Thế còn trường hợp 1 biến mà nó chưa có giá trị khởi tạo, chỉ được khai báo thì sao?

```ts
let nothing: never;

// 🚫 Error: Variable 'nothing' is used before being assigned.
console.log(nothing + 1);
```

Ta thấy đoạn `let nothing: never;` không báo lỗi!
Bởi vì thời điểm đó, nó chỉ được khai báo, chứ chưa có giá trị khởi tạo, nên chưa trả về giá trị nào cả.
Điều đó hoàn toàn phù hợp với logic của `never`.

Tuy nhiên, khi cố tình sử dụng mà chưa gán giá trị cho nó thì đương nhiên ta sẽ gặp lỗi:

> 🚫 Error: Variable 'nothing' is used before being assigned.

Vậy thì 1 biến liệu có thể có kiểu là `never` được không?
Ta xét ví dụ sau:

```ts
const throwError = (errorMsg: string): never => {
  throw new Error(errorMsg);
};

const testNeverValue: never = throwError('');
console.log('🤔 ~ test', testNeverValue);
```

`testNeverValue` type vẫn có thể được gán với `never`.
Tuy nhiên, khi chạy đoạn code này, ta chỉ có thể tới được đoạn `throw new Error(errorMsg);`, còn sẽ không thể log ra màn hình giá trị của `testNeverValue` được.

Như vậy việc ta gán giá trị trả về `never` với 1 biến không có ý nghĩa gì trong trường hợp này!

## Ứng dụng

### Hữu dụng khi báo lỗi

Nếu bạn code nhiều TypeScript thì sẽ quen mặt thằng `never` này ở thông báo lỗi khi build project. Bởi lẽ `never` thường đi kèm với việc có gì đó đang không thể return được.

### Sử dụng với Generic types

Khi muốn tạo ra 1 [generic types](https://www.typescriptlang.org/docs/handbook/2/generics.html#generic-types) với input type bất kỳ _ngoại trừ_ 1 số types nào đó thì ta có thể viết như sau:

```ts
type TNonNullable<T> = T extends null | undefined ? never : T;

// 🚫 Error: Type 'undefined' is not assignable to type 'never'.
const value: TNonNullable<undefined> = undefined;
console.log('🚀 ~ value', value);

// ---
// another example:
type TNotANumber<T> = T extends number ? never : T;

// 🚫 error: Type 'number' is not assignable to type 'never'.
const notANumberValue: TNotANumber<number> = 1;
console.log('🚀 ~ notANumberValue', notANumberValue);
```

- `TNonNullable` sẽ không chấp nhận `null | undefined`.
- `TNotANumber` cũng không chấp nhận 1 number type.

---

Tham khảo:

- [tutorialsteacher typescript-never](https://www.tutorialsteacher.com/typescript/typescript-never)

- [stackoverflow - understanding-the-never-type-in-typescript](https://stackoverflow.com/questions/40225384/understanding-the-never-type-in-typescript-2)
