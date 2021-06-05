## Resource khi bắt đầu project với Angular 🛡️

## 🌈 UI Library

Chọn theo hệ thống design gần nhất với design của designer, ví dụ [10 Best Design Systems and How to Learn (and Steal) From Them](https://designerup.co/blog/10-best-design-systems-and-how-to-learn-and-steal-from-them/). Khi đó designer phải tuân thủ các luật của UI lib đó.

Nếu designer không quyết thì mặc định mình chọn [taiga-ui](https://taiga-ui.dev/) hoặc [Angular Material](https://material.angular.io/).


Chọn `Material` vì:

- Lib này có những người đóng góp là từ `Angular team` - những người hiểu rõ nhất về triết lý Angular.
- Chỉ thông qua duy nhất Angular chứ không pha tạp hỗ trợ cả React, Vue như 1 số Lib.
- component điểm mạnh là [list drag/drop](https://material.angular.io/cdk/drag-drop/overview) - trong 1 số trường hợp thì đây là điều kiện tiên quyết có chọn Material hay không.

Chọn `taiga-ui` vì:

- Hiệu ứng animation được chăm chút từng component nhỏ.
- Import cái mình cần mà không gây dư thừa code trong bundle. giảm bundle-size.
- Điểm mạnh:
  - Có các service cơ bản dùng nhiều như [notifications-service](https://taiga-ui.dev/services/notifications-service), dialog service, scroll service... Nếu không thì rất có thể bạn sẽ phải tự tạo service như thế này.
  - [Component loader](https://taiga-ui.dev/components/loader) focus vào chỗ nào đang loading data thay vì toàn bộ màn hình như nhiều lib.

- [Custom style](https://taiga-ui.dev/variables) dễ dàng để phù hợp với ngôn ngữ designer, điều mà 1 số lib ít chú trọng.
- components đều sử dụng `OnPush`, cả dự án được quảng cáo là đung với `strict` TypeScript mode, tuy nhiên [tsconfig](https://github.com/TinkoffCreditSystems/taiga-ui/blob/main/tsconfig.json) chưa dùng [Angular strict mode](https://angular.io/guide/strict-mode), `eslint`.
- Điểm cộng trên quna điểm cá nhân: Web docs thiết kế tối giản, có tên miền yêu thích của developer là `.dev`, số lượng Contributor trên github nhiều.

Trong trường hợp design không khớp với các UI lib có sẵn thì có thể tạo ra bộ style riêng thay vì đi custom lại. Tuy nhiên, nếu dùng những component phức tạp như date-picker chẳng hạn, bạn thà dùng date-picker của `Material` với custom style thay vì đi viết lại cả cái date-picker đúng không!

## 🌗 State management

Hiện tại thì mình chưa gặp bài toán nào cần thiết phải dùng lib về `state management`.

Một số cách thông thường là dùng 1 [singleton service](https://angular.io/guide/singleton-services) để link giữa các component với nhau, state thì lưu tại bản thân component, 1 biến đẩy ra ngoài template để emit event. Hoặc lưu state đó ở chính `singleton service` nếu dùng ở nhiều component. Service đó được inject vào chỗ nào cần lấy state.

Ngoài ra, [bài viết này](https://dev.to/angular/simple-yet-powerful-state-management-in-angular-with-rxjs-4f8g) có hướng dẫn làm thế nào dùng RxJS để tự tạo ra 1 `state management`. Cách này thì mình cũng chưa thử dùng thực tế.

## Typed Forms

[@ngneat/reactive-forms](https://github.com/ngneat/reactive-forms)

## Charts

Nếu dùng charts: [ngx-charts](https://github.com/swimlane/ngx-charts) tương tự công năng [d3](https://d3js.org/) nhưng viết bằng `Angular`, output trên `DOM` là thẻ `svg`.

## Tính năng đa ngôn ngữ

Nếu dùng đa ngôn ngữ: [transloco](https://ngneat.github.io/transloco/)

## Làm việc với bảng biểu (Grid) tựa Excel

[ignite-ui-angular](https://www.infragistics.com/products/ignite-ui-angular) mất phí, tuy nhiên lại opensource tại [đây](https://github.com/IgniteUI/igniteui-angular). [ignite-ui-angular's grid](https://www.infragistics.com/products/ignite-ui-angular/angular/components/grid/grid) cung cấp data grid, tree grid, hierarchical (cấp bậc) grid với excel-style filtering, live-data, sorting, draggable row và các toolbar khác.

## Bảng biểu với dữ liệu lớn

[ngx-datatable](https://github.com/swimlane/ngx-datatable)

## 🧪 Unit Test

Test dùng thêm package:

- [ng-mocks](https://github.com/ike18t/ng-mocks#readme): mock Components, Directives, Pipes, Modules, Services and Tokens, bỏ đi lượng code dư thừa khi tạo mock, tăng tốc chạy test.
- [observer-spy](https://github.com/hirezio/observer-spy): giúp test RxJS observables dễ dàng hơn.
- [@ngneat/spectator](https://github.com/ngneat/spectator): tool khủng để tương tác với UI - component là chính.

## input-mask

[@ngneat/input-mask](https://github.com/ngneat/input-mask) 's type:

- IP Address
- Currency
- Date
- License Plate
- Email

## Notifications UI

[@ngneat/hot-toast](https://github.com/ngneat/hot-toast): popup nhỏ với hiệu ứng chạy ra màn hình.

## Loading UI

[@ngneat/content-loader](https://github.com/ngneat/content-loader): Giống hiệu ứng loading các bài post (Newsfeeds) của Facebook - các bài post rỗng và kèm theo animation.

## Unsubscribe from `observables` khi component destroyed

[@ngneat/until-destroy](https://github.com/ngneat/until-destroy)

## Copy to clipboard

[@ngneat/copy-to-clipboard](https://github.com/ngneat/copy-to-clipboard)

## Hotkeys

[@ngneat/hotkeys](https://github.com/ngneat/hotkeys)

## 🪟 Dialog

[@ngneat/dialog](https://github.com/ngneat/dialog)

## Caches HTTP requests

[@ngneat/cashew](https://github.com/ngneat/cashew)

## Tránh lặp đi lặp lại các mẫu hiển thị error trên form

[@ngneat/error-tailor](https://github.com/ngneat/error-tailor)

## Dirty Check Forms

[@ngneat/dirty-check-forms](https://github.com/ngneat/dirty-check-forms): có tính năng rất hay là khi bạn muốn navigate tới đâu đó trong App thì vẫn check được forms đã dirty - có data chưa được lưu hay chưa.

[@ngneat/forms-manager](https://github.com/ngneat/forms-manager)

## Convert JS to CSS variables

[variabless](https://github.com/ngneat/variabless): Ngoài Angular ra vẫn dùng được.

## Dynamic View

[@ngneat/overview](https://github.com/ngneat/overview): Tránh lặp đi lặp lại phần template, giúp dêx bảo trì, được module hóa.

## Đồng bộ URL params với form realtime

[@ngneat/bind-query-params](https://github.com/ngneat/bind-query-params)

## Icon

[angular-fontawesome](https://github.com/FortAwesome/angular-fontawesome)

## Animation  🪃

[ng-animate](https://github.com/jiayihu/ng-animate): không phải là 1 wrapper của 1 js lib thuần nào đó hay cốt lõi được viết bằng [Angular Animations](https://angular.io/guide/animations).

[ngx-interactive-paycard](https://github.com/milantenk/ngx-interactive-paycard): Mô hình hóa credit card hay paycard như thật với animation.

## Docs

[compodoc](https://github.com/compodoc/compodoc): Dễ dàng nhìn thấy quan hệ giữa các thành phần trong App.

## OpenAPI

- [ng-openapi-gen](https://github.com/cyclosproject/ng-openapi-gen): chuyển từ thiết kế API được viết dưới dạng OpenAPI 3.0 sang source-code bao gồm model interfaces và web service.

## linter

[Angular eslint](https://github.com/angular-eslint/angular-eslint)

## Cách viết CSS-in-JS

Tham khảo bài viết [này](https://dev.to/aziziyazit/css-in-js-for-angular-1no4).

## Cách viết source template và styles cùng file với source component không?

Cá nhân mình thì thích viết source template và styles cùng file với source component, điều này giúp không phải chuyển file quá nhiều. Còn việc highlight template, styles đã có editor extention lo.

## Tham khảo

- Team [@ngneat](https://github.com/ngneat)
- [Angular resources](https://angular.io/resources?category=development)
- Tổng hợp mọi thứ (seed repos, starters, boilerplates, examples, tutorials, components, modules, videos...) hữu ích trong Angular ecosystem: [Awesome Angular](https://github.com/PatrickJS/awesome-angular)

---

Photo by <a href="https://unsplash.com/@bradencollum?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Braden Collum</a> on <a href="https://unsplash.com/s/photos/start?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
