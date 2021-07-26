## 🧪 SonarQube - Tìm hiểu Rules cho TypeScript - về các lỗ hổng bảo mật 🔓 - phần 1

Chi tiết rule tham khảo tại [sonarsource rules for typescript - vulnerabilities](https://rules.sonarsource.com/typescript/type/Vulnerability/RSPEC-6105).

Các rule dành cho TypeScript chia thành các loại:

- 🤤 Vulnerabilities - lỗ hổng có thể bị lợi dụng
- 😨 Bug
- 🤢 Security Hotspot - điểm nóng bảo mật
- 🤭 Code smell - Code thối hay code tệ

## Việc updates DOM không nên để việc redirect đến websites không an toàn

>DOM updates should not lead to open redirect vulnerabilities

Những data mà user có thể can thiệp / controll được ví dụ như `document.location.hash` không nên được dùng để chuyển tới 1 trang web khác.

## Giải thích về `location.hash`

`document.location.hash` trả về phần trang web được đánh dấu bởi ký hiệu `#`, thường là phần đề mục - Headings.

### Ví dụ về `location.hash` - Trường hợp `location.hash` thực sự tồn tại

https://www.markdownguide.org/basic-syntax/#headings

Khi vào URL trên, trang web sẽ không hiển thị từ đầu trang mà chuyển tới phần đề mục có tên là `headings`.

![location-hash-headings.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627281521240/j1lmeugyc.png)

`location.hash` được định nghĩa trong thuộc tính `href` trong HTML.

![location-hash-html.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627281553256/kiGxoLZxg.png)

Theo như [html.spec.whatwg.org](https://html.spec.whatwg.org/multipage/history.html#dom-location-hash-dev) - spec của HTML thì:

>The `href` attribute setter intentionally has no security check.

Sẽ không có phần kiểm tra security cho thuộc tính `href`, nên luật này check xem đã có phần code kiểm tra security hay chưa.

Để lấy thử giá trị này, mở `ctrl` + `shift` + `I`, tới `console` tab và gõ:

```js
location.hash
```

Output:

![console-location-hash.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627281594705/dZ9v497hI.png)

### 😂 Trường hợp `location.hash` không hề tồn tại

https://www.google.com.vn/#test

Vào `google.com.vn` tất nhiên là không có `location.hash` nào tên là `#test` cả. Đây là 1 lỗ hổng về bảo mật.

Khi `location.hash` không hề tồn tại, tuy nhiên `location.hash` đó vẫn được redirect tới. Ví dụ:

`http://vulnerable/page.html#https://www.attacker.com/`

Thử test https://www.google.com.vn/#http://example.com/ với Chrome thì không bị redirect sang `http://example.com/`.
Tuy nhiên ta không thể khẳng định điều này ở các browser khác.

### Ví dụ đoạn code vi phạm

```ts
document.location = document.location.hash.slice(1);
```

Khi set `document.location`, trang web bị redirect sang `${currUrl}${document.location.hash.slice(1)}`.

### Giải pháp tuân thủ rule

Valid URL trước khi redirect.


```ts
function isValidUrl(url) {
  if(url.startsWith("https://www.example.com/")) {
    return true;
  }

  return false;
}

if(isValidUrl(document.location.hash.slice(1))) {
   document.location = document.location.hash.slice(1);
}
```

---

Photo by <a href="https://unsplash.com/@kfc0105?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Kenta Miyahara</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
