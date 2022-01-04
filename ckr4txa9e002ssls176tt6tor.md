## JavaScript - hiệu năng giữa 🔍 indexOf và 🔎 includes

[Array.prototype.includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes) là được giới thiệu từ `ECMAScript 7`, được support bởi tất cả các browser hiện đại.

## Performance testing source code

```js
let allElements = [...document.getElementsByTagName('*')];
console.log('allElements.length: ', allElements.length);

/**
 * get a random member of `allElements`
 */
const getRandomMember = () => {
  allElements[Math.floor(Math.random() * allElements.length)];
}
const checkingTimes = 1e7;

const t1 = performance.now();
console.log('🍀 Start includes');

for (let i = 0; i < checkingTimes; i++) {
  randEl = getRandomMember();

  // searching for that member, result should be `true`
  const isIn = allElements.includes(randEl);
}

const t2 = performance.now();
console.log('🍒 Start indexOf');

for (let i = 0; i < checkingTimes; i++) {
  randEl = getRandomMember();

  // searching for that member, result should be `true`
  const isIn = (allElements.indexOf(randEl) > -1);
}

const t3 = performance.now();
console.log('End');

const includesTime = t2 - t1;
const indexOfTime = t3 - t2;

console.log('🍀 includes time:', t2 - t1);
console.log('🍒 indexOf time:', t3 - t2);

console.log('🍒 indexOf / 🍀 includes time:', indexOfTime / includesTime);
```

## Các bước thực hiện

1. Truy cập [google.com](https://www.google.com/)
2. `ctrl` + `shift` + `i` để mở `console`
3. Copy source code trên và paste vào `console` và gõ `enter`

## Kết quả

```txt
allElements.length:  307
🍀 Start includes
🍒 Start indexOf
End
🍀 includes time: 167.10000000149012
🍒 indexOf time: 2972.7999999970198
VM1313:41 🍒 indexOf / 🍀 includes time: 17.790544583904907
```

## Kết luận

Với case là số lượng thực hiện lớn (`1e7`) và array là các elements thực sự và có length tầm `> 300` thì thời gian thực thi của `includes` gấp khoảng 17 lần so với indexOf.

## Tham khảo

- Source code cơ bản lấy từ: [Stackoverflow - Array.prototype.includes vs. Array.prototype.indexOf
](https://stackoverflow.com/questions/35370222/array-prototype-includes-vs-array-prototype-indexof)
- [w3schools includes](https://www.w3schools.com/jsref/jsref_includes_array.asp)

---

Photo by <a href="https://unsplash.com/@reskp?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Jametlene Reskp</a> on <a href="https://unsplash.com/s/photos/search?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>