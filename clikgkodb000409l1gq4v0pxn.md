---
title: "Qwik - Chú ý khi import image với routes"
datePublished: Tue Jun 06 2023 15:51:30 GMT+0000 (Coordinated Universal Time)
cuid: clikgkodb000409l1gq4v0pxn
slug: qwik-chu-y-khi-import-image-voi-routes
tags: qwik-image-vietnamese

---

## 🥑 Vấn đề

Thoạt đầu mọi người sẽ nghĩ routes thì liên quan tới image làm sao được? Tuy nhiên mình đã gặp 1 bug ở bản:

```json
{
    "@builder.io/qwik": "1.1.4",
    "@builder.io/qwik-city": "1.1.4"
}
```

Đó là khi import image vào `Logo` component:

```tsx
export const Logo = () => <img src="images/logo.png" width="245" height="98"></img>;
```

Relative path trong source code tới image là `public/images/logo.png`.

Ta sử dụng `Logo` component phía layout, cụ thể là trong `Header` component.

Ta vào trang chủ - không sử dụng routes, thì mọi thứ vẫn OK, cho đến khi ta sử dụng routes...

Ta sử dụng `<Link />` để redirect sang routes khác:

```html
<Link href="/about">About</Link>
```

Khi navigation tới trang `about`, URL của image lại bị hiểu thành:

> http://localhost:5173/about/images/logo.png

Trong khi URL đúng phải là:

> [http://localhost:5173/images/logo.png](http://localhost:5173/images/logo.png)

URL bị thừa \`about\` path, dẫn tới lỗi `404 Not Found`, không tải được image!

## 🥥 🍆 Giải quyết

```diff
-export const Logo = () => <img src="images/logo.png" width="245" height="98"></img>;
+export const Logo = () => <img src="/images/logo.png" width="245" height="98"></img>;
```

Ta thêm dấu `/` trước `images` là xong. Nhớ tắt `pnpm start` - dev server rồi chạy lại nhé!

Nguyên nhân có thể do `routes` đã điều hướng với cả image nếu ta định nghĩa `src` sai.