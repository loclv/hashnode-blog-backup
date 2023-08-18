---
title: "Typescript - Khi viết Unit Test và muốn mock 1 property thì Object.defineProperty và phép gán thông thường khác nhau như thế nào?"
datePublished: Fri Aug 18 2023 18:44:57 GMT+0000 (Coordinated Universal Time)
cuid: cllgxwx5y000109mhb8zlbu7m
slug: typescript-khi-viet-unit-test-va-muon-mock-1-property-thi-objectdefineproperty-va-phep-gan-thong-thuong-khac-nhau-nhu-the-nao
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/ojEoSvAq2ik/upload/0eb9928fd84299f59ef9a64bb4632e24.jpeg
tags: typescript-vietnamese

---

## Phân biệt `Object.defineProperty` và phép gán 1 property thông thường

Câu hỏi này cũng đã được hỏi tại [stackoverflow - object-defineproperty-vs-object-prototype-property-vs-object-property-when-to](https://stackoverflow.com/questions/31816983/object-defineproperty-vs-object-prototype-property-vs-object-property-when-to).

### Phép gán thông thường - **direct assignment**

Giải thích lại phép gán thông thường thông qua ví dụ ta muốn mô tả 1 object `person` có property là `age`, trong đó value của `age` là 25. Thì ta sẽ làm:

```typescript
interface Person {
  age?: number;
};

const person: Person = {};

// phép gán thông thường
person.age = 25;

console.log("age: ", person.age);
// Expected output: age: 25
```

### Gán bằng `Object.defineProperty`

Còn đây là cách còn lại:

```typescript
interface IPerson {
  age?: number;
}

const definedPerson: IPerson = {};

Object.defineProperty(definedPerson, "age", {
  value: 25,
  configurable: true,
  writable: true,
});

console.log("age: ", definedPerson.age);
// Expected output: age: 25
```

Ta thấy là cách viết này khá dài dòng và khó hiểu!

`age` có giá trị tương ứng với giá trị của `value` property. Còn `configurable` và `writable` thì có ý nghĩa gì?

Ta lấy lại ví dụ ở [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Object/defineProperty](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty):

```typescript
const object1: { property1?: number } = {};

Object.defineProperty(object1, "property1", {
  value: 42,
  writable: false,
});

object1.property1 = 77;
// Throws an error in strict mode and when run with `ts-node`
// TypeError: Cannot assign to read only property 'property1' of object

console.log(object1.property1);
```

Định nghĩa về `writable`:

> `true` if the value associated with the property may be changed with an [assignment operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators#assignment_operators). **Defaults to** `false`.

Đại ý là property này sẽ không thể bị thay đổi sau khi được định nghĩa - defined.

Còn đối với `configurable`, tóm tắt ý nghĩa là không thể dùng `defineProperty` để tái định nghĩa - redefined nữa. Hay khi `configurable: false` - default value thì chỉ dùng `defineProperty` được 1 lần duy nhất.

Ví dụ sau lấy từ [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Object/defineProperty](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty):

```javascript
const o = {};

Object.defineProperty(o, "a", {
  get() {
    return 1;
  },
  configurable: false,
});

Object.defineProperty(o, "a", {
  configurable: true,
});
// throws a TypeError

Object.defineProperty(o, "a", {
  enumerable: true,
});
// throws a TypeError

Object.defineProperty(o, "a", {
  set() {},
});
// throws a TypeError (set was undefined previously)

Object.defineProperty(o, "a", {
  get() {
    return 1;
  },
});
// throws a TypeError
// (even though the new get does exactly the same thing)

Object.defineProperty(o, "a", {
  value: 12,
});
// throws a TypeError
// ('value' can be changed when 'configurable' is false,
// but only when the property is a writable data property)

console.log(o.a);
// 1
delete o.a;
// Nothing happens; throws an error in strict mode
console.log(o.a);
// 1
```

## So sánh 2 cách trên

Khi sử dụng 2 cách trên với 1 property được định nghĩa trước với TypeScript thì không có gì đặc biệt. Tuy nhiên 1 số trường hợp phải mock data thêm 1 property từ object có sẵn.

Ở vú dụ dưới đây, `name` property chưa được định nghĩa type trước:

```typescript
Object.defineProperty(person, "name", {
  value: "abc-name",
  configurable: true,
  writable: true,
});

// vs

(person as IPerson & { name: string }).name = "abc-name";
```

Như vậy thì các ưu nhược điểm của 2 cách là:

| Tiêu chí | Phép gán thông thường | `Object.defineProperty` |
| --- | --- | --- |
| Ngắn gọn, dễ hiểu | OK | NG |
| Tính chặt chẽ | đạt yêu cầu với cách dùng thông thường, TypeScript `readonly`, `enum` có thể thay thế 1 phần. | Rất chặt chẽ đối với JS thuần. |
| performance | Tốt hơn nhiều lần `Object.defineProperty` | Kém hơn |

Ghi chú: kết quả đo performance có ở [https://measurethat.net/Benchmarks/Show/1046/0/defineproperty-vs-direct-assignment](https://measurethat.net/Benchmarks/Show/1046/0/defineproperty-vs-direct-assignment).

Tóm lại, quyết định dùng phương pháp nào tùy vào yêu cầu từng dự án.

## Tham khảo

* [https://stackoverflow.com/questions/31816983/object-defineproperty-vs-object-prototype-property-vs-object-property-when-to](https://stackoverflow.com/questions/31816983/object-defineproperty-vs-object-prototype-property-vs-object-property-when-to)