## Trong Micro Frontends, tại sao Custom Elements + Server Side Includes = 💚 ? - phần 1

Chẳng là gần đây dự án rảnh, free task nên mọi người trong team có thời gian tìm hiểu công nghệ.

Có 1 chủ đề mình cùng tìm hiểu với team đó là `Micro Frontends`, thì tình cờ mình thấy có đoạn, `Custom Elements + Server Side Includes = ❤️`.

Mà ở 1 dự án khác đang gặp vấn đề làm sao kết hợp [Nuxt.js](https://nuxtjs.org/) - 1 framework chuyên dùng SSR mode với Server Side Includes (SSI) như thế nào?

![thinking](https://media.giphy.com/media/3oz8xZvvOZRmKay4xy/giphy.gif)

## Các khái niệm

Trước hết ta cùng làm rõ qua các khái niệm sẽ nhắc tới trong bài.

### [Micro Frontends](https://micro-frontends.org/)

Để dễ hiểu, ta tìm hiểu trước về `Monolithic Frontends` - mô hình ra đời trước.

Trong mô hình `Monolithic Frontends`, Monolithic có thể dịch là `nguyên khối`. `Monolithic Frontends` thì trái ngược với `Micro Frontends`.

Ảnh lấy tại [micro-frontends.org](https://micro-frontends.org/).

![monolith-frontback-microservices.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629023557185/dSlSGbFpH.png)

Ở hình trên, lần lượt là:

- `The monolith`: Backend, DB và  Frontend chung 1 source-code, tuy bên trong có thể tách biệt các module, nhưng những App ngoài không thể sử dụng chung thành phần nào cả.
Mô hình này khá là phổ biến ở các dự án những năm trước khi điện thoại thông minh - iPhone ra đời.

- `Front & Back`: Backend, DB và  Frontend tách ra thành 2 phần. Do nhu cầu request Data bây giờ có thêm App trên Mobile nữa chẳng hạn, nên giờ người ta tách Backend ra để có thể dùng chung 1 API hay DB.
Ngoài ra, 1 Backend có thể dùng ở nhiều website, như kiểu 1 bên thứ 3 chuyên cung cấp API như 1 dịch vụ độc lập chẳng hạn. Ví dụ `Google Map API` chẳng hạn.

-`Micro-services`: 1 Frontend có thể dùng nhiều Backend, DB. Mô hình cũng được nhiều công ty sử dụng, do 1 App/Web có thể dùng nhiều API khác nhau kết hợp.

Mục đích những mô hình trên đều là phục vụ `kinh tế chia sẻ`, tiết kiệm công sức khi develop.
Giống như không ai bỏ công sức ra để tự làm cái gì đó (đồ dùng gia dụng chẳng hạn) quá mất thời gian, chẳng thà ra chợ mua luôn cho nhanh.

Mô hình `Micro Frontends`  cũng có mục đích như vậy.

Ảnh lấy tại [micro-frontends.org](https://micro-frontends.org/).

![verticals-headline.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629025330505/bxVNthaeQ.png)

`End-to-End Teams`: Mô hình `Micro Frontends` - 1  website hay web app được chia theo chiều dọc theo cụm chức năng.
Từng chức năng này có thể được viết bởi 1 framework riêng, tách biệt hoàn toàn so với chức năng khác.

Mục đích:

- Chia sẻ 1 phần frontend giữa nhiều Web hoặc App: Ví dụ phần biểu đồ tài sản, giá cổ phiếu trong App chứng khoán thì dùng trên App và trên Web bản desktop.
Lúc này thì ta có thể viết phần chung này ra riêng 1 project.

- Dự án chạy song song nhiều team Frontend: Ví dụ có team chỉ biết React, có team chỉ biết Angular thì phần frontend của team React có thể dùng chung với team Angular.

- Vấn đề version: Ví dụ 1 phần viết bằng `React` đã cũ, vì không có công số upgrade lên phiên bản mới nên ta có thể viết sang 1  project mới hoàn toàn sử dụng version mới.

Bất kể mô hình nào cũng có nhược điểm, thì nhược điểm ở đây là khi các project Frontend có phần chung - phần common hay phần shareable thì cách chia sẻ khá loằng ngoằng.
Vấn đề này thì xin để ở 1 bài viết khác. Và tất nhiên là ở các dự án nhỏ, không có tính chia sẻ thì đừng dại mà dùng cái này cho tốn thời gian!

Mô hình này cũng có thể kết hợp với `Micro-services` giống như trò chơi xếp hình lego, mọi phần có của Web có thể tái sử dụng hoặc shareable.

Để thực hiện mô hình `Micro Frontends`, có nhiều cách, cụ thể từng framework sẽ có cách thực hiện khác nhau. Trong đó có 1 cách là [The DOM is the API](https://micro-frontends.org/#the-dom-is-the-api).

### [The DOM is the API](https://micro-frontends.org/#the-dom-is-the-api)

Đầu tiên, ta phải hiểu tính năng [Custom Elements](https://developers.google.com/web/fundamentals/web-components/customelements) là 1 phần cốt lõi của hệ thống `web component` - 1 tính năng của trình duyệt.
`Custom Elements` cho phép định nghĩa 1 HTML tags mới, thay vì các thẻ truyền thống như `<div>`, `input`.
Danh sách cụ thể các trình duyệt hỗ trợ tại [can i use?](https://caniuse.com/?search=Custom%20Elements). Hiện tại tất cả các trình duyệt hiện đại đã hỗ trợ tính năng này.

Là 1 khái niệm coi mỗi [Custom Elements](https://developers.google.com/web/fundamentals/web-components/customelements) giống như 1 API dành cho Frontend.
Mỗi khi chèn thêm 1 `custom element` ví dụ `blue-buy` tag chẳng hạn, browser sẽ get toàn bộ phần Frontend đã được gán với `blue-buy` về.

![custom-element.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629025769097/XZibjZz7_.gif)

Ta sẽ không đi sâu vào cách này.

Tuy cách này hoạt động tốt trong môi trường `SPA` - `Single Page Application`, nhưng trong môi trường `Server-side Rendering / Universal Rendering` hay còn gọi là `SSR` thì sao?

Ảnh lấy tại [Client-Side v/s Server-Side Rendering: What to Choose When?](https://dzone.com/articles/client-side-vs-server-side-rendering-what-to-choos):

![ssr.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629025725825/lxlyZObLy.png)

Ta thấy, thời điểm tại bước số 3, browser đã render ra HTML rồi nhưng chưa thể tương tác do nó chưa downloads `JS`.
Việc ưu tiên HTML được render ra là nhằm mục đích
[SEO - Search Engine Optimization](https://vi.wikipedia.org/wiki/T%E1%BB%91i_%C6%B0u_h%C3%B3a_c%C3%B4ng_c%E1%BB%A5_t%C3%ACm_ki%E1%BA%BFm)
tốt hơn.

Tuy nhiên đối với cách dùng `Custom Elements` thì nếu chưa có `JS` thì `tag` trên `DOM` không được định nghĩa.
Browser cứ thể hiển thị và nó sẽ không biết get phần Frontend nào ra cả.

Buồn hơn là [developers.google - nguyên tắc cơ bản dành cho web  - Custom Elements](https://developers.google.com/web/fundamentals/web-components/customelements) cũng không nhắc đến `SSR`.

>No JavaScript, no Custom Elements :(

## Giải pháp cho SSR: Custom Elements + Server Side Includes = ❤️

### Server Side Includes (SSI)

`Server Side Includes` là cách viết thẻ HTML động, thay đổi cấu trúc DOM nếu thỏa mãn điều kiện nào đó.
Thẻ tag HTML được thêm vào bởi server-side - HTTP service hay web server - tools phụ trách việc trả về web resource cho browser.
Ngày xưa thì hay dùng HTTP service như [Apache](https://httpd.apache.org/), giờ thì có [NGINX](https://www.nginx.com/), `Node.js`, [caddy-server](https://caddyserver.com/) viết bằng Go.

Ví dụ `index.html` có:

```html
<!--#include virtual="/head.html"-->
```

`head.html` file được thêm vào từ đoạn này.

Ví dụ khác:

```html
<!--#echo var="DATE_LOCAL" -->
```

Khi page được render ra thì nội dung sau sẽ được thay thế vào:

```text
Tuesday, 15-Jan-2013 19:28:54 EST
```

Cách set giá trị cho 1 biến:

```html
<!--#set var="name" value="Rich" -->
```

Set biến tên là `name` có giá trị `Rich`.

Cấu trúc điều kiện:

```html
Good <!--#if expr="%{TIME_HOUR} <12" -->
morning!
<!--#else -->
afternoon!
<!--#endif -->
````

>This lets SSI be a tiny programming language of sorts

Vâng, đọc đến đây thì ... what the hell!

![cry](https://media.giphy.com/media/3oz8xUK8V7suY7W9SE/giphy.gif)

Ta có thể thấy để tạo nội dung động cho web thì có rất nhiều cách dùng JS thuần hoặc Frontend Framework hiện này làm được. Chính vì vậy mà hiện nay ta thấy SSI hiếm khi được sử dụng.

[Server Side Includes, the hottest of the web in 1995](https://dev.to/merri/server-side-includes-the-hottest-of-the-web-in-1995-1pn1), vâng, đã 25 năm kể từ ngày công nghệ này khá là hot. 😅

Điểm mạnh của các công nghệ pre-rendered ở backend này đó là tốt cho SEO và load web nhanh hơn ở thời điểm ban đầu mới load web về. Tuy nhiên tùy trường hợp tăng performance không đáng kể vì từ resource, browser render ra nhanh, với cả nếu dùng SPA thì browser đã cache lại resource, không phải load lại rồi.

Điểm yếu của SSI đó là mỗi lần trả về website cho mỗi browser thì `index.html` buộc phải được web server xử lý (update nội dung động). Điều này làm tốn tài nguyên dành cho server. Còn đối với SPA chẳng hạn, nội dung động (dynamic) sẽ do browser xử lý dựa trên JS.

Vì SSI có là công nghệ có từ lâu và dựa trên HTML nên có lỗ hổng bảo mật [owasp.org - attacks/SSI](https://owasp.org/www-community/attacks/Server-Side_Includes_(SSI)_Injection). Mình sẽ nói về lỗ hổng này ở bài viết khác. Từ khóa để tìm hiểu lỗ hổng này là `server side includes injection`.

Vậy thì ứng dụng của công nghệ này ở đâu? Câu trả lời chính là thời điểm JS chưa load được trong quá trình loading SSR web.
Cũng vì vậy, hướng tìm cách làm `Micro Frontends` cho 1 SSR web bằng 1 SSR JS Framework (như Nuxt.js chẳng hạn) là không khả thi.
Ta phải dựa vào web server, middleware. Trong đó mình khá là thích các web server, middleware đến từ Node.js, Go.

Ở [phần 2](https://loclv.hashnode.dev/trong-micro-frontends-thuc-thi-custom-elements-server-side-includes-phan-2) của bài viết ta sẽ tìm hiểu về cách thức thực hiện cụ thể hơn.

## Tham khảo

- [Apache - How to SSI](https://httpd.apache.org/docs/2.4/howto/ssi.html)
- [Server Side Includes, the hottest of the web in 1995](https://dev.to/merri/server-side-includes-the-hottest-of-the-web-in-1995-1pn1)
- [Micro Frontends](https://micro-frontends.org/)
- Bonus: [cách thực hiện Micro Frontends với Angular - 100 days of Angular](https://github.com/angular-vietnam/100-days-of-angular/blob/master/Day039-micro-frontends.md)

---

Photo by <a href="https://unsplash.com/@micheile?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Visual Stories || Micheile</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
