---
title: "JS - khi nào nên sử dụng function .toString() vs String()  - chuyên sâu 📝"
datePublished: Wed Jul 30 2025 04:03:43 GMT+0000 (Coordinated Universal Time)
cuid: cmdpfy663000d02lagqgd5o4t
slug: js-khi-nao-nen-su-dung-function-tostring-vs-string-chuyen-sau
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/whWoLKPmx10/upload/22b5fe9bf78f30766478b4a538e882c7.jpeg
tags: js, javascript, typescript

---

Trong JavaScript, cả `.toString()` và `String()` đều dùng để chuyển đổi một giá trị thành chuỗi (string), nhưng **chúng có khác biệt quan trọng về cách hoạt động, an toàn và cách dùng phù hợp tùy ngữ cảnh**.

---

## 🌿 **So sánh nhanh**

| **Đặc điểm** | .toString() | String() |
| --- | --- | --- |
| Là method của object? | ✅ Có (Object.prototype.toString) | ❌ Không |
| Gây lỗi nếu giá trị là null hoặc undefined | ❗️**Có** (TypeError) | ✅ **Không** |
| Chuyển đổi kiểu | Không ép kiểu | Ép kiểu rõ ràng |
| Có thể override | ✅ Có thể bị ghi đè 1 cách rõ ràng | Trong trường hợp sử dụng \`toString()\` thì kết quả vẫn giống như bị ghi đè (xem ví dụ dưới) |

---

## **📌 Khi nào dùng**

## **.toString()**

**Dùng khi bạn chắc chắn giá trị không phải null hoặc undefined, và muốn dùng method cụ thể của object.**

### **✅ Ví dụ phù hợp:**

```javascript
const num = 123;
num.toString(); // "123"
```

```javascript
const arr = [1, 2, 3];
arr.toString(); // "1,2,3"
```

**⛔ Đối với null hoặc undefined:**

Sẽ throw ra lỗi:

```javascript
const value = null;
value.toString(); // ❗️TypeError: Cannot read properties of null
```

Thực thế sử dụng với null or undefined:

```typescript
null?.toString();
// output: undefined
String(null)
// output: 'null' (a string not `null` value)
```

## **📌 Khi nào dùng String()**

**Dùng khi bạn không chắc giá trị có thể là gì (null, undefined, number, boolean, object…), hoặc muốn ép kiểu an toàn.**

### **✅ Ví dụ phù hợp:**

```javascript
String(123); // "123"
String(null); // "null"
String(undefined); // "undefined"
String(true); // "true"
```

**Cách này an toàn hơn trong hầu hết các tình huống không kiểm soát được giá trị.**

---

## **Đối với type/kiểu**

| **Tình huống** | **Nên dùng** |
| --- | --- |
| Muốn ép kiểu an toàn, tránh lỗi với null hoặc undefined | String() |
| Biết chắc là đối tượng hợp lệ và muốn dùng logic .toString() riêng của nó (như array hoặc class custom) | .toString() |

---

## **💡 Class override**

* Khi custom toString() trong class: **dùng .toString() hoặc String() đều sẽ** tận dụng tính năng override.
    

Ví dụ:

```typescript
class User {
  name: string

  constructor(name: string) {
    this.name = name;
  }

  toString() {
    return `User: ${this.name}`;
  }
}

const u = new User("A");

console.log(`toString: ${u.toString()}`); // "User: A"
console.log(`String: ${String(u)}`);     // "User: A"
```

Trong ví dụ TypeScript/JavaScript trên, cả u.toString() và String(u) đều trả về "User: A". Mặc dù hai cách gọi khác nhau, **chúng có liên quan chặt chẽ** thông qua cơ chế **chuyển đổi kiểu (type coercion)** trong JavaScript.

---

## **✅ Cách String(value) hoạt động nội tại**

Khi bạn gọi String(value), JavaScript sẽ **không gọi trực tiếp .toString()** mà đi qua một cơ chế cụ thể hơn:

### **🔍 Bước 1: Nếu value là**

### **null**

### **hoặc**

### **undefined**

| **value** | **Kết quả** |
| --- | --- |
| null | "null" |
| undefined | "undefined" |

### **🔍 Bước 2: Nếu là object**

JS sẽ làm theo thứ tự sau:

```typescript
1. Nếu value có method [Symbol.toPrimitive] → dùng nó
2. Nếu không có:
   - Gọi value.toString()
   - Nếu kết quả là primitive → dùng nó
   - Ngược lại → gọi value.valueOf()
```

Dưới đây là nguồn gốc chính xác và đáng tin cậy cho quy trình ép kiểu về string trong JavaScript:

### [**ECMAScript Language Specification – §7.1.1 ToPrimitive**](https://tc39.es/ecma262/#sec-toprimitive)

## **🔹 Tài liệu bổ trợ dễ hiểu**

1. MDN Web Docs:
    
    * [Symbol.toPrimitive](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toPrimitive)
        
    * [Object.prototype.valueOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)
        
    * [Object.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)
        
    * [Type Conversion](https://developer.mozilla.org/en-US/docs/Glossary/Type_conversion)
        

### **🧠 Cụ thể trong ví dụ của bạn:**

1. `u` là object
    
2. Không có Symbol.toPrimitive, không có valueOf() trả về primitive
    
3. Có .toString() → được gọi và trả về "User: A" → hợp lệ → dùng
    

## **🧪 Nếu bạn muốn kiểm chứng:**

### **✅ Override valueOf**

```typescript
u.valueOf = () => ({});
console.log(String(u)); // vẫn dùng toString vì valueOf không trả về primitive
```

### **✅ Override Symbol.toPrimitive**

```typescript
u[Symbol.toPrimitive] = (hint) => {
  if (hint === "string") return "Primitive from Symbol";
};
console.log(String(u)); // "Primitive from Symbol"
```

## **🧠 Tóm tắt**

| **Gọi** | **Gọi trực tiếp?** | **Kết quả** |
| --- | --- | --- |
| u.toString() | ✅ Trực tiếp | "User: A" |
| String(u) | ❌ Gián tiếp: Symbol.toPrimitive → toString → valueOf | "User: A" |

**→ Vì bạn đã override toString() trả về primitive, nên String(u) sẽ dùng đúng method này.**

---

## **🧪 So sánh hiệu năng**

Việc so sánh hiệu năng giữa .toString() và String() trong JavaScript có thể mang lại kết quả hơi khác nhau tùy vào trình thông dịch (V8, SpiderMonkey, JavaScriptCore…), nhưng có một số nguyên tắc chung:

### **✅ 1.** `.toString()`

* Là method của Object.prototype hoặc các prototype khác (Number, Boolean, Array…).
    
* Với **primitive**, JS sẽ thực hiện **autoboxing** (tạo object tạm thời):
    

```typescript
const n = 123;
n.toString(); // JS tạo new Number(n), rồi gọi method
```

⏱️ Autoboxing → **tốn thêm một bước tạo object tạm** → hiệu năng **chậm hơn một chút** so với String().

### **✅ 2.** `String(value)`

* Gọi hàm ép kiểu toàn cục, có logic nội tại hiệu quả trong trình thông dịch.
    
* Tránh được bước autoboxing (đặc biệt với primitive như number, boolean, null, undefined).
    
* Thường tối ưu hơn trong JavaScript engine (V8, Chakra, etc.).
    

⏱️ Với primitive → thường **nhanh hơn** .toString() một chút.

### **📊 Benchmark thực tế dành cho** primitive

Bạn có thể chạy benchmark này trong trình duyệt hoặc Node.js:

```typescript
const iterations = 1e7;
const num = 123;

console.time("toString");
for (let i = 0; i < iterations; i++) {
  num.toString();
}
console.timeEnd("toString");

console.time("String()");
for (let i = 0; i < iterations; i++) {
  String(num);
}
console.timeEnd("String()");
```

## **🎯 Kết luận**

* **Khác biệt hiệu năng là có nhưng nhỏ**, chỉ đáng quan tâm trong **vòng lặp lớn hoặc code cực tối ưu hóa**.
    
* Muốn an toàn type → **ưu tiên dùng String()**.