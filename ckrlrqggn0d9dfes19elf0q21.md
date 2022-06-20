## 🧪 SonarQube - Tìm hiểu Rules cho TypeScript - về bug 💩 - phần 5

Chi tiết rule tham khảo tại [sonarsource rules for TypeScript - bug](https://rules.sonarsource.com/typescript/type/Bug/RSPEC-4335).

Các rule này thuộc loại code dễ gây bug.

## 🤔 Các khái niệm dạo đầu

Để hiểu rule trong bài này, bạn cần nắm được khái niệm Data Type - `Never` trong TypeScript.

### Data Type - `Never` trong TypeScript

`never` là 1 type không tồn tại trong JavaScript.

`never` hay _kiểu không bao giờ_, được định nghĩa là kiểu trả về khi mà bạn chắc chắn là không thể trả về được 1 giá trị nào đó do vòng lặp vô hạn.

Ví dụ 1 function không thực hiện được hết, hay function đó luôn trả về 1 exception - ngoại lệ:

```ts
function throwError(errorMsg: string): never {
  throw new Error(errorMsg);
}

function keepProcessing(): never {
  while (true) {
    console.log('I always does something and never ends.')
  }
}
```

`throwError` và `while (true)` sẽ ngăn function thực hiện xong, thế nên nó tất nhiên không bao giờ có thể return void. Và kiểu function này, ta có thể đặt kiểu trả về là `never`.

Nếu bạn code nhiều TypeScript thì sẽ quen mặt thằng `never` này ở thông báo lỗi khi build project.

Dưới đây là 1 thuộc tính đặc thù của `never`:

```ts
let something: void = null;
let nothing: never = null; // Error: Type 'null' is not assignable to type 'never'
```

Kiểu `void` thì gán được nếu giá trị đó là `null`, còn `never` thì không.

### Data Type - `Any` trong TypeScript

`Any` hay kiểu gì cũng được, là 1 loại type mà biến có kiểu này có thể gán với mọi kiểu giá trị trên đời.

```ts
let something: any = 'Hello World!';
something = 23;
something = true;

let arr: any[] = ['John', 212, true];
arr.push('Smith');
console.log(arr); //Output: [ 'John', 212, true, 'Smith' ]
```

Chính vì như thế nên nó hay được dùng khi mà biến có thể thuộc 1 kiểu bất kỳ.

Tuy nhiên, nhược điểm của `any` là hủy luôn tính năng hay nhất mà TypeScript mang lại, đó type safe hay check kiểu.

Dùng `any` tương đương với việc TypeScript tự phế đi võ công của mình nên hạn chế sử dụng thôi!

## Intersection types - phép hợp giữa nhiều type

```ts
interface ErrorHandling {
  success: boolean;
  error?: { message: string };
}

interface ArtworksData {
  artworks: { title: string }[];
}

interface ArtistsData {
  artists: { name: string }[];
}

// These interfaces are composed to have
// consistent error handling, and their own data.

type ArtworksResponse = ArtworksData & ErrorHandling;
type ArtistsResponse = ArtistsData & ErrorHandling;
```

Thay vì viết lặp đi lặp lại phần `ErrorHandling` thì phần shareable sẽ được viết tách ra và sử dụng chung.

Và công cụ để hợp lại đó là `Intersection types`.

---

OK, ta đã biết được các khái niệm cần thiết, sau đây là nội dung chính của rule.

## 🤤 Type mà không có thành phần con như `any` hay `never` không nên dùng trong phép hợp của nhiều type

>Types without members, 'any' and 'never' should not be used in type intersections

### 🤔 Ví dụ đoạn code vi phạm

```ts
function foo(p: MyType & null) { // Noncompliant 😨
  // do something
}

function bar(p: MyType & any) { // Noncompliant 😨
  // do something
}
```

Ví dụ trên đang sử dụng `Intersection types` - phép hợp giữa nhiều type.

### 😨 Vấn đề

Kiểu `p: MyType & null` tương đương với `never`, chẳng khác nào việc phế đi võ công gián tiếp.

Kiểu `p: MyType & any` tương đương với `any`, cũng chẳng khác nào việc phế đi võ công gián tiếp.

Tóm lại, việc này dẫn đến phá hủy cấu trúc kiêu đang rất ngon lành.
Đối với các developer biết về điều này thì cũng có khả năng gặp phải vì lỗi đánh máy chẳng hạn.

### 😌 Giải pháp tuân thủ rule

```ts
function foo(p: MyType | null) {
  // do something
}
// or
function foo(p: MyType & AnotherType) {
  // do something
}

function bar(p: any) {
 // do something
}
```

Ta có thể sử dụng `union type` nghĩa là 1 trong những kiểu được phân cách bởi phép hoặc - `|`.

Ví dụ: `number | string | boolean`.

---

Tham khảo:

- [tutorialsteacher typescript-never](https://www.tutorialsteacher.com/typescript/typescript-never)
- [Unions and Intersection Types](https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html)

Photo by <a href="https://unsplash.com/@robert2301?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Robert Ruggiero</a> on <a href="https://unsplash.com/s/photos/wrong?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
