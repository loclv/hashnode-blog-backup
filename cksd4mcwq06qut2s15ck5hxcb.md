## Trong Micro Frontends, thực thi Custom Elements + Server Side Includes = ❤️ - phần 2

## SSI giải cứu `Custom Elements` trong môi trường SSR

Trong [phần 1](https://loclv.hashnode.dev/trong-micro-frontends-tai-sao-custom-elements-server-side-includes-phan-1) mình có nhắc tới dùng `Custom Elements` trong `Micro Frontends`.
Trong thời điểm load SSR web, JS không tồn tại, chỉ có HTML,
thay vì dùng JS để tạo ra `Custom Elements`, ta sẽ dùng SSI:

```html
<blue-buy sku="t_porsche">
  <!--#include virtual="/blue-buy?sku=t_porsche" -->
</blue-buy>
```

`#include` comment sẽ được thay thế bằng response từ endpoint:  `/blue-buy?sku=t_porsche`.

### Ngoài SSI ra thì ta cũng có các giải pháp thay thế

- [Edge_Side_Includes](https://en.wikipedia.org/wiki/Edge_Side_Includes) (ESI) có cú pháp:

```html
<esi:include src="http://example.com/1.html" alt="http://bak.example.com/2.html" onerror="continue"/>
```

ESI kết hợp với [nodesi](https://github.com/Schibsted-Tech-Polska/nodesi), biến phần dynamic của web hoạt động dựa trên cơ chế `Promise`.

- [Compoxure](https://github.com/tes/compoxure) - Proxy middleware dựa trên công nghệ [htmlparser2](https://github.com/fb55/htmlparser2/) dành cho phần viết bằng ESI hoặc SSI.

- [tailor](https://github.com/zalando/tailor) - `pre-rendered markup on the backend` có số star là 1.6k nhiều nhất trong số các tools ở trên.  `tailor` lấy các phần động đồng thời song song với nhau.

Kiến trúc trong `tailor` tổng quan:

Ảnh lấy từ [mosaic9.org](https://www.mosaic9.org/):

![tailor-achi.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629026796524/lzC6ZtP2Q.png)

`Tailor` sử dụng [parse5](https://github.com/inikulin/parse5/) để dịch `template`, thay thế `fragmentTag` thành các luồng bất đồng bộ:

```html
<html>
<head>
    <script type="fragment" src="http://assets.domain.com"></script>
</head>
<body>
    <fragment src="http://header.domain.com"></fragment>
    <fragment src="http://content.domain.com" primary></fragment>
    <fragment src="http://footer.domain.com" async></fragment>
</body>
</html>
```

TechLead nên cân nhắc thật kỹ các giải pháp thay thế được SSI, để phù hợp nhất với dự án của mình.

### Cụ thể thực hiện SSI bằng nginx

```conf
upstream team_blue {
  server team_blue:3001;
}

upstream team_green {
  server team_green:3002;
}

upstream team_red {
  server team_red:3003;
}

server {
  listen 3000;
  ssi on;

  location /blue {
    proxy_pass  http://team_blue;
  }

  location /green {
    proxy_pass  http://team_green;
  }

  location /red {
    proxy_pass  http://team_red;
  }

  location / {
    proxy_pass  http://team_red;
  }

}
```

Ta để ý khi `ssi: on;`, các team c, mỗi ông sẽ code dự án của riêng mình tại 3 cổng khác nhau chạy trên con web server này lần lượt là: `3001`, `3002`, `3003`.

[Đây](https://github.com/neuland/micro-frontends/tree/master/2-composition-universal) là source-code đầy đủ về cách kết hợp giữa `nginx` + `docker-compose` + 3 project tách biệt nhau hoàn toàn của team Red, Green, Blue.

Ảnh chụp web khi thay đổi thành phần dựa trên params: ``t_fend` hoặc `t_eicher`:

![web server console example.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629026862434/M7yOHUkGJ.png)

3 nút tương ứng với 3 cái xe Red, Green, Blue mỗi lần bị click sẽ reload lại cả page!
Đây không còn là SPA - Single Page Application thân thương nữa rồi!

![cry](https://media.giphy.com/media/3oz8xUK8V7suY7W9SE/giphy.gif)

3 nút đó sẽ route cả page tới từng phần của 1 trong 3 team đã làm.

1 khi JavaScript khả dụng là sau khi SSR web đã load xong phần JS thì phần việc route page tới đâu sẽ là việc của client-side (phần việc của JS). Từ đây, khi bấm vào 1 trong 3 nút trên sẽ không còn reload lại cả trang nữa mà thay vào đó sẽ hoạt động dựa trên `Custom Elements` + `JS`. Lý thuyết là vậy, nhưng thực thi như thế nào thì để bài viết khác nhé.

![thinking](https://media.giphy.com/media/3oz8xZvvOZRmKay4xy/giphy.gif)

Phần tiếp theo là `Data Fetching & Loading States` dành cho `Custom Elements` + `SSI/ESI`.

## Tham khảo

- [Apache - How to SSI](https://httpd.apache.org/docs/2.4/howto/ssi.html)
- [Server Side Includes, the hottest of the web in 1995](https://dev.to/merri/server-side-includes-the-hottest-of-the-web-in-1995-1pn1)
- [Micro Frontends](https://micro-frontends.org/)
- Bonus: [cách thực hiện Micro Frontends với Angular - 100 days of Angular](https://github.com/angular-vietnam/100-days-of-angular/blob/master/Day039-micro-frontends.md)

---

Photo by <a href="https://unsplash.com/@micheile?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Visual Stories || Micheile</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>

 [giphy.gif](https://media.giphy.com)
