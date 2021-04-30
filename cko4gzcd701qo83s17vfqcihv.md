## Tại sao bạn nên thử thiết kế Database bằng dbdiagram.io 😎

## Giới thiệu 😎

[dbdiagram.io](https://dbdiagram.io/) là bộ công cụ thiết kế Database (design Entity-Relationship diagram, database schema) trên nền Web dựa trên nguyên tắc `text to image`.

UI bao gồm 1 bên là `text editor`, 1 bên là `dragable` `diagram`.

Công cụ này dược trang [HackerNoon](https://hackernoon.com/) và [css-tricks](https://css-tricks.com/), vậy đã đủ uy tín chưa các bạn?

## Lợi ích 😌

- focus vào typing thiết kế DB mà ít phải tạo tác động đến phần diagram như [app.diagrams.net](https://app.diagrams.net/), giúp thiết kế nhanh hơn.

- Generate SQL statements - lệnh SQL để sinh ra DB thực. Ngoài ra còn có thể `export` ra `PDF/PNG`. Từ đây bạn có thể share thiết kế với team thông qua bài thuyết trình chẳng hạn.

- Lưu lại và quản lý thay đổi ngay trên 1 file trong `source code` dựa trên `Git`, điều mà công cụ dựa trên việc kéo thả khó thể làm được.

- `editor` và `diagram` support dark-mode.

- Share thiết kế thông qua trực tiếp `dbdiagram.io` hoặc thông qua file text nằm trong `source code`.

- Cú pháp thể hiện quan hệ giữa các bảng, khóa chính, khóa phụ đơn giản. Tham khảo cú pháp tại [blog này](https://hackernoon.com/dbdiagram-io-a-database-diagram-designer-built-for-developers-and-analysts-975f310d4f13).

- Có thể `import` thẳng `PostgreSQL` hoặc `MySQL` scripts có sẵn vào để hiển thị.

- Phần editor có thể `highlight syntax` và phát hiện lỗi `syntax`.


![err-syntax](https://cdn.hashnode.com/res/hashnode/image/upload/v1619796469655/PJcERHkY9.png)

## Cú pháp 🤟

Ví dụ về khóa chính, ký hiệu `PK`:

```text
Table users {
  id int PK
  email varchar
  gender varchar
  relationship varchar
  dob datetime
  country int
}
```

Để thể hiện quan hệ, bạn cũng có thể dùng chuột kéo thả nhưng với `editor` thì:

```text
// 3 Relationship Types
//   <   one-to-many
//   >   many-to-one
//   -   one-to-one

// Short-form syntax
Ref users.country < countries.code
```

## Tips khi dùng 🤟

- Double-clicking vào table label sẽ focus con trỏ vào định nghĩa table đó bên editor.
- `Ctrl/Cmd + S` để save.
