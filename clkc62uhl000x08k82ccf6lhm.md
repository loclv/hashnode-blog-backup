---
title: "JavaScript - Chuyện gì xảy ra khi 1 Promise không bao giờ được resolve"
datePublished: Fri Jul 21 2023 05:54:57 GMT+0000 (Coordinated Universal Time)
cuid: clkc62uhl000x08k82ccf6lhm
slug: javascript-chuyen-gi-xay-ra-khi-1-promise-khong-bao-gio-duoc-resolve
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/R3ofE-8DyLk/upload/e8aed3e631f9c16e5eba68406afc2e01.jpeg
tags: js-vietnamese

---

## Đi từ Event loop

Từ định nghĩa của resolve method - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Promise/resolve](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve), ta hiểu đơn giản là việc call resolve() sẽ call xử lý nằm trong method `then()` hoặc sau `await`.

Ví dụ với đoạn code sau sẽ minh họa điều đó:

```javascript
const promise = new Promise((resolve) => {
  console.log("start");
  if (true) resolve();
});

promise.then(() => console.log("done."));
```

Để hiểu rõ thì ta dùng [https://www.jsv9000.app/](https://www.jsv9000.app/) để xem Event Loop trong JS hoạt động thế nào.

Bước đầu tiên là "**Evaluate Script**" - chạy code theo cách đồng bộ - Synchronously.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689917839669/6dc04710-fa7a-41a8-bf61-f57c1732edd2.png align="center")

Bấm next sẽ tới bước tiếp theo. Trong Call Stack đã có 1 **anonymous function đó là:** `(resolve) => { console.log("start"); if (true) resolve(); }`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689917963123/c6ae59cd-cd9f-4cb8-baaa-795806eac7c0.png align="center")

Tiếp theo message "start" được hiển thị.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689918120374/b17e897f-cae5-4c98-8d9e-4c27812487bf.png align="center")

Tiếp theo, Microtask Queue có thêm 1 anonymous function, đó chính là `() => console.log("done.")`.

Tiếp thep, do `resolve();` được call nên Microtasks tương ứng được thực hiện nên được đưa vào Call Stack.

Và function trong Call Stack được thực thi và kết quả là "done." message được hiển thị.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689918376871/c535b50f-c8ef-480e-aeb8-cb37693aac01.png align="center")

Cuối cùng Call Stack trống và kết thúc.

## Vậy thì chuyện gì xảy ra khi 1 Promise không bao giờ được resolve?

Ta chạy thử với đoạn code sau:

```javascript
const promise = new Promise((resolve) => {
  console.log("start");
  if (false) resolve();
});

promise.then(() => console.log("done."));
```

Trong đó `resolve();` sẽ không bao giờ được thực thi.

Tương tự bên trên, chỉ khác là `resolve();` không được thực thi nên callback nằm trong `then();` không được đưa vào Microtask Queue. Điều đó dẫn đến chương trình thoát sau khi chỉ thực hiện `console.log("start");` .

Tương tự với async và await:

```javascript
const simple = async () => {
  console.log("start");
  // resolve(); không bao giờ được call
  await new Promise((resolve) => {});
  console.log("done.");
};
simple();
```

Tóm lại, callback dành cho promise đó không được thực thi và thoát luôn.

## Reference

* [https://www.jsv9000.app/](https://www.jsv9000.app/)
    
* [https://stackoverflow.com/questions/46914025/node-exits-without-error-and-doesnt-await-promise-event-callback](https://stackoverflow.com/questions/46914025/node-exits-without-error-and-doesnt-await-promise-event-callback)