## Angular - Lazy loading modules 😴 - lợi và hại

## 😴 Lazy loading modules là gì?

Giới thiệu về `Lazy loading modules` của trang chủ Angular tại [đây](https://angular.io/guide/lazy-loading-ngmodules).

Cũng có thể gọi nó là `Lazy-loaded modules`.

Đúng với cái tên của nó, load các modules 1 cách `lười biếng nhất`.

### 😆 `lười nhiều` để làm gì?

`Lười biếng` thì bạn sẽ cần làm ít hơn, đồng nghĩa với load ít modules hơn và loading mà không cần tải lại trang.

Có 2 mục đích:

- Load ít modules hơn thì trang web sẽ nhanh hơn.
- Load nội dung mới mà không phải reload lại cả trang web giúp trải nghiệm người dùng tốt hơn, không có cảm giác phải chờ cho loading xong.

### 🤔 Thế làm thế nào để có thể `lười biếng`?

Muốn load ít modules hơn thì ta phải chia để trị.

Chiến lược chia của `lazy loading modules` là chia theo routes.

Muốn chia theo routes thì phải phân biệt được các module chung cho cả app và các module con - modules được load riêng rẽ.

Dấu hiệu để biết các module chung là được dùng với method `forRoot()`, còn ngược lại sẽ là `forChild()`.

Chính vì `forRoot()` thiết kế để gọi cho tất cả nên nó chỉ cần gọi 1 lần. Nếu được gọi lần 2 thì tất nhiên là có khả năng `module` được nạp vào 2 lần. Còn ngược lại `forChild()` cho phần con nên nếu muốn dùng `modules con` 2 lần ở 2 route thì phải gọi nó 2 lần.

Như trong ví dụ của trang chủ Angular dưới đây:

```ts
{
    path: 'customers',
    loadChildren:
        () => import('./customers/customers.module').then(m => m.CustomersModule)
}
```

Thì với thuộc tính `path`, ta định nghĩa `url path` là `customers` - tên gọi của các module con dành riêng cho `customers`.

Với thuộc tính `loadChildren`, ta định nghĩa tập hợp các module đó cụ thể là gì.

Từ đó, chỉ những module mà `customers` dùng mới được load. Nói ngắn gọn là `cần thì mới chi` nên rất tiết kiệm băng thông.

Ngoài ra còn `Preloading`, là âm thầm load trước khi người dùng thực sự gọi tới nó.

Vấn đề là nó có ưu điểm như vậy thì lúc nào cũng nên dùng nó không?

## Khi nào nên dùng?

Khi mà mỗi tính năng có thể chia theo routes và có modules khác biệt sâu rộng.

Ví dụ như `customers` dùng thư viện về bảng biểu có tính năng như `Excel`, trong khi `login` thì không cần. Chỉ cần login mà load cả cái thư viện có `bundle size` lên tới 1 hoặc 2MB thì không hợp lý đúng không.

## 🙄 Khi nào không nên dùng?

- Dự án có các tính năng không quá khác biệt và khác biệt không quá lớn, hầu hết các module là dùng chung, dùng thêm chỉ tội mất time đúng không. :v

### Những vấn đề tiềm ẩn

#### Một số lib không hỗ trợ `lazy-loaded module` tốt

Ví dụ với [ngx-translate](https://github.com/ngx-translate/core), khi search các `issues` trên `github` với từ khóa `is:issue is:open lazy` tại [đây](https://github.com/ngx-translate/core/issues?q=is%3Aissue+is%3Aopen+lazy), chúng ta có thể thấy rất nhiều vấn đề nếu như lib không hỗ trợ `lazy-loaded module` tốt.

Điển hình như `issue` dưới đây.

<https://github.com/ngx-translate/core/issues/1193>

Ngay bản thân tôi khi làm dự án cũng gặp phải vấn đề có chỗ lib `ngx-translate` không hoạt động đúng khi sử dụng `Lazy loading modules`.

Cũng có lib không gặp vấn đề nào ví dụ như [transloco](https://ngneat.github.io/transloco/), xem thêm tại [đây](https://github.com/ngneat/transloco/issues?q=is%3Aissue+is%3Aopen+lazy). Lib này cũng hỗ trợ tốt với tính năng load file theo từng module tách biệt và cũng chỉ được gọi khi người dùng gọi đến nó, cụ thể tại [đây](https://ngneat.github.io/transloco/docs/scope-configuration).

#### 🌲 `lazy-loaded module` lồng nhau phức tạp

`Lazy loading modules` lồng nhau là kiểu `app module` lazy-load `content module`, rồi `content module` lại lazy-load thằng khác. Trong khi đó bản thân trong thằng `app module` cũng có nhiều nội dung liên quan tới `content module`.

Ví dụ như ảnh dưới đây từ vấn đề trên `stackoverflow` tại [đây](https://stackoverflow.com/questions/53413612/ngx-translate-with-shared-lazy-loading-modules/53483123).


![lazy-loaded-module-structor.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606305086507/TWfZ0MsmP.png)

Không hiểu tại sao nhưng tôi đã phải import service `ngx-translate` cho từng module riêng lẻ được lazy-load để cho nó chạy được. :v

Khi mà phần `content module` có text gì đó cần translate ra mà phần module con của `content module` cũng dùng chung 1 file json translation, để không bị load lại 2 lần file translation tôi phải sử dụng giải pháp từ `stackoverflow` bên trên. :(

Có nhiều cái để nói với các lib không hỗ trợ `lazy-loaded module` tốt, nên tôi update thêm sau phần này.

---

Nguồn ảnh tại [đây](https://pixabay.com/photos/sloth-sleeping-animal-rest-sleep-5043324/).