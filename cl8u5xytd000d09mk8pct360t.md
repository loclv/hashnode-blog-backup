# TypeScript - Viết doc comments cơ bản và eslint cho doc 📖

## 💁 Giới thiệu - lý do `doc` comments hữu dụng

Với JS thì ta có [JSDoc](https://jsdoc.app/), còn với TS thì ta có [TSDoc](https://tsdoc.org/) là bộ quy chuẩn để viết doc comments rõ ràng hơn, dễ đọc, dễ hiểu hơn.

> TSDoc is a proposal to standardize the doc comments used in TypeScript code.

Đây là 1 ví dụ thông dụng:

```ts
/**
 * Returns the average of two numbers.
 *
 * @param x - The first input number
 * @param y - The second input number
 * @returns The average of `x` and `y`
 */
export const getAverage = (x: number, y: number): number => {
    return (x + y) / 2;
};

```

Từ TSDoc ta có thể tự động tạo ra các trang document dành cho các dự án lớn:

![Screenshot from 2022-09-26 19-32-56.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1664195661731/h6cuy6GI3.png align="left")

Bạn thấy đấy, nhìn vào doc thì rất dễ hiểu, đặc biệt là với các method/class phức tạp. Còn về các cú pháp và cách viết thì TSDoc rất "na ná" JSDoc.

## 🧑‍🤝‍🧑 Đối tượng sử dụng được doc

Bao gồm:

- method của 1 class
- class
- function, bao gồm cả arrow function
- ngay cả 1 biến, ví dụ:

```ts
/**
 * oneDayMilliSeconds = 1000 * 60 * 60 * 24 = 86_400_000
 */
const oneDayMilliSeconds = 86_400_000;
```

Khi hover chuột qua biến đó trên vscode, sẽ thấy được doc của variable này:

![Screenshot from 2022-10-03 19-05-26.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1664798772881/Ue-dR2hSR.png align="left")

## 📖 Cách đọc doc

Tương tự với 1 biến bên trên, các đối tượng như method, function, class đều có thể xem tương tự. Ví dụ khi hover chuột vào 1 function:

![Screenshot from 2022-10-04 08-37-26.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1664847495153/nHM3Xu65C.png align="left")

Chú ý là nếu dùng kiểu comment `// ` thay vì khối `/**` thì sẽ không đọc được như trên, vì cách comment `// ` không đúng chuẩn của doc.

## 🔑 Các từ khóa - tag cơ bản

1 tag được định nghĩa trong TSDoc hay JSDoc theo dạng: `@tagName` như `@param`, `@returns`.

- Cú pháp mô tả 1 param:

`@param` - `space` - `mô tả`. 

Ví dụ:

```md
@param x - The first input number
```

Khác với JSDoc, việc mô tả type tại param là không cần thiết. Tuy nhiên vẫn có bạn quên mất điều này và viết như dưới đây:

```md
@param {number} x - The first input number
```

Để khắc phục vấn đề có thể "quên" này thì ta có thể dùng rule [eslint-plugin-jsdoc-rules-no-types](https://github.com/gajus/eslint-plugin-jsdoc#eslint-plugin-jsdoc-rules-no-types).

- Cú pháp mô tả giá trị trả về:

`@returns` - `space` - `mô tả`.

Ví dụ:

```md
@returns The average of `x` and `y`
```

## 🚧 Cấu trúc của 1 doc

### Phần đầu tiên là nội dung mô tả method / class / function / value này

Thông thường mình nên xuống thêm 1 dòng để doc nhìn thoáng dễ đọc hơn, dễ phân biệt đâu là nội dung, đâu là các tag khác. Để mọi người trong team tuân thủ ta có thể dùng [](https://github.com/gajus/eslint-plugin-jsdoc#eslint-plugin-jsdoc-rules-newline-after-description)

### Phần thứ 2 thường là các tag khác ngoài param, returns (tag chính) nếu có như

- `@link`
- `@see`
- `@example`: cũng có thể để ở cuối sau các tag chính
- `@inheritDoc`
- ...

Xem thêm tại [tsdoc](https://tsdoc.org/).

### Phần thứ 3 là param, returns tag

Tất nhiên nếu function không có param hay return value thì không cần.
Để tránh việc không cần mà cũng thêm tag thừa vào ta có thể dùng [eslint - valid-jsdoc](https://eslint.org/docs/latest/rules/valid-jsdoc).

## 🚩 Các tag hữu ích khác

Có rất nhiều từ khóa để đặc tả doc, tuy nhiên theo kinh nghiệm của mình thì những tag sau là sử dụng nhiều nhất:

- `@link`
- `@see`
- `@example`
- `@inheritDoc`

Ở bài viết này, ta sẽ làm quen với cách sử dụng `@example` và `@link` đã.

### Sử dụng `example` tag

![example.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1664871716609/MJnzbXCLd.png align="left")

Với ví dụ trên ta có thể thấy `example` theo sau có thể là text hoặc nội dung dưới dạng `md` hay `markdown`.

Việc viết dưới dạng `markdown` giúp ta đọc example code dễ hơn.

Thực ra đoạn code sau `@example` cũng không cần phải cho vào code-block của `markdown`.
Ta chỉ cần viết code nằm giữa vùng `@example` tag và tag khác là được:

![Screenshot from 2022-10-04 19-03-42.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1664885287850/nqGzkBBrW.png align="left")

Và đây là ví dụ viết code chưa đúng vùng nằm giữa, code sẽ không được tự động highlight lên:

![Screenshot from 2022-10-04 19-02-48.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1664885372123/uCcSAtTdL.png align="left")

### Sử dụng `link` tag cơ bản

Với input là doc comment dưới đây:

```ts
/**
 * Explain URL: {@link https://levelup.gitconnected.com/cross-browser-crazy-44e90d61b204}
 */
```

Thì output khi hover chuột sẽ là:

```txt
Explain URL: https://levelup.gitconnected.com/cross-browser-crazy-44e90d61b204
```

Như vậy, phần `@link` sẽ biến mất ở output.

---

Như vậy về cơ bản TSDoc bạn có thể sử dụng và kết hợp với eslint.
Điều này rất quan trọng khi bạn viết 1 library, hay 1 package để người khác sử dụng.
