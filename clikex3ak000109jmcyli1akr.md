---
title: "Qwik - Sử dụng kết hợp styles CSS modules và global CSS"
datePublished: Tue Jun 06 2023 15:05:10 GMT+0000 (Coordinated Universal Time)
cuid: clikex3ak000109jmcyli1akr
slug: qwik-su-dung-ket-hop-styles-css-modules-va-global-css
tags: qwik-vietnamese, css-modules-vietnames

---

Trước hết ta hãy đọc qua về [CSS modules với Qwik](https://qwik.builder.io/docs/components/styles/#css-modules).

## 👀 Ví dụ

Giả sử ta có `footer.tsx`:

```tsx
import { component$ } from '@builder.io/qwik';
import styles from './footer.module.css';

export default component$(() => {
  return (
    <footer>
      <div class={'container ' + styles.anchor}>
        <span>Abc</span>
      </div>
    </footer>
  );
});
```

Với styles CSS modules - `footer.module.css`:

```css
.anchor {
  display: flex;
  justify-content: center;
}
```

Còn đây là global CSS - `styles.css`:

```css
.container {
  margin: 0 auto;
  padding: 30px 40px;
}
```

## 😌 🦊 Công thức

Với ví dụ trên, ta viết `class={'container ' + styles.anchor}`, tức là

> global CSS name + space (để tách biệt 2 class name) + CSS modules name

Kết quả là rendered element:

```html
<div class="container _anchor_1r1eh_1"</div>
```

Với `_anchor_1r1eh_1` là CSS modules name.