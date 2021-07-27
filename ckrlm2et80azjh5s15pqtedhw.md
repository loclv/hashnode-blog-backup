## 🧪 SonarQube - Tìm hiểu Rules cho TypeScript - về các lỗ hổng bảo mật 🔓 - phần 3

Chi tiết rule tham khảo tại [sonarsource rules for typescript - vulnerabilities](https://rules.sonarsource.com/typescript/type/Vulnerability/RSPEC-5696).

Rule này thuộc loại lỗ hổng có thể bị lợi dụng - vulnerabilities.

## 🤤 Việc updates DOM không nên để dẫn tới tấn công `cross-site scripting` (XSS)

>DOM updates should not lead to cross-site scripting (XSS) attacks

Những data mà user có thể can thiệp / controll được ví dụ như `document.location.hash` không thể tin tưởng được và nên được valid (kiểm tra) trước khi được sử dụng.

Rule cũng liên quan, cùng bản chất với [rule - Việc updates DOM không nên để việc redirect đến websites không an toàn](https://loclv.hashnode.dev/sonarqube-tim-hieu-rules-cho-typescript-ve-cac-lo-hong-bao-mat-phan-1).

Kẻ tấn công có thể lợi dụng để thực hiện các đoạn script không mong muốn.

### 🤔 Ví dụ đoạn code vi phạm

Ví dụ về URL hiện tại: `http://vulnerable/page.html#<img onerror='alert(1); src='invalid-image' />`.

Và đoạn code sau đọc phải thông tin bên trên:

```ts
const rootDiv = document.getElementById('root');
const hash = decodeURIComponent(location.hash.substr(1));

rootDiv.innerHTML = hash; // Noncompliant 😨
```

Trong thẻ:

```html
<img onerror='alert(1); src='invalid-image' />
```

Đoạn code trong thuộc tính `onerror` được kích hoạt khi load image file.

Ở đây là `alert(1);`, tuy nhiên kẻ tấn công có thể lợi dụng để thực hiện các đoạn script không mong muốn.

Trong khi đó `innerHTML` quá mạnh! nó có thể thêm sửa xóa element, DOM tree được, vì thế nên tránh sử dụng.

Đây là lỗ hổng hay bị khai thác.

### Giải pháp tuân thủ rule

Thay vì dùng `innerHTML`, ta dùng `innerText`.

```ts
const rootDiv = document.getElementById('root');
const hash = decodeURIComponent(location.hash.substr(1));

rootDiv.innerText = hash; // Compliant 😌
```

Thay vào đó ta sử dụng `innerText`, để set nội dung text của 1 node trong DOM tree.

Nó chỉ render ra text thôi, chứ không thể thay đổi cả cấu trúc DOM tree như `innerHTML`.

---

Tham khảo:

- [w3schools - innerhtml](https://www.w3schools.com/jsref/prop_html_innerhtml.asp)

Photo by <a href="https://unsplash.com/@whale?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Matthew Smith</a> on <a href="https://unsplash.com/s/photos/tree?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
