## Lên đời con hàng Angular 11 🚀

Bài viết tham khảo tại trang chủ của `Angular`: <https://angular.io/guide/updating-to-version-11>.

Như thông tin từ `Angular` 🚀 thì phiên bản 11.0.0 đã được vào ngày Big Sale vừa rồi - 11/11. 😄

Version ^10.0.0 sẽ không còn được update các tính năng mới kể từ Giáng sinh năm nay 24/12/2020.

Vậy nên đây là thời gian tốt để tìm hiểu những thay đổi lớn khi `lên đời` con hàng `Angular ^11.0.0` từ phiên bản `^10.0.0`.

## Những API sẽ bị loại bỏ

Xem thêm tại [đây](https://angular.io/api?status=deprecated) hoặc cụ thể hơn tại [đây](https://angular.io/guide/deprecations) danh sách API sẽ bị loại bỏ.

Về chính sách loại bỏ thì:

- Khi 1 API hay 1 tính năng bị thông báo loại bỏ ở 1 version bất kỳ thì nó vẫn sẽ được giữ lại cho tới 2 bản release lớn sau này. Ví dụ như API bị thông báo loại bỏ ở `Angular 7.xx` thì vẫn được giữ lại ở `Angular 8.xx` và `Angular 9.xx`, thực sự không thể dùng ở `Angular 10.0`.

- Cho tới khi nó bị loại bỏ thực sự thì nó chỉ được sửa các lỗi về bảo mật thôi.

- `npm dependencies` chỉ phải update nếu `Angular` được update lên đời - `major version` (ví dụ từ 10.xx lên 11.xx).

## Những thay đổi lớn

- IE 9, 10 và IE mobile sẽ không còn được support. Tuy nhiên các bạn đừng lo, vẫn còn IE 11 cơ mà 😄.

- Phải update lên ít nhất là `TypeScript 4.0`.

- `@angular/router` loại bỏ `preserveQueryParams`, thay vào đó sử dụng `queryParamsHandling = "preserve"`. Những thay đổi tương tự như thế này rất nhiều nên mình xin phép không liệt kê ở đây nữa.

-  Config cho `router module`, trong `forRoot()` thì thuộc tính `relativeLinkResolution` sẽ được chuyển default là `corrected` thay vì `legacy`.

```ts
RouterModule.forRoot(routes, { relativeLinkResolution: 'corrected' })
```

Nó enable `a bug fix` (bug cụ thể tại [đây](https://stackoverflow.com/questions/50503577/how-to-navigate-to-sibling-in-angular-4-using-relative-navigation)).

Nó làm cho 1 components với 1 path là rỗng:

```ts
const routes = [
  {
    path: '',
    component: ContainerComponent,
    children: [
      { path: 'a', component: AComponent },
      { path: 'b', component: BComponent },
    ]
  }
];
```

Trong `ContainerComponent` thì đoạn sau sẽ không hoạt động:

```ts
<a [routerLink]="['./a']">Link to A</a>
```

Thay vào đó là:

```ts
<a [routerLink]="['../a']">Link to A</a>
```

Tóm lại là dùng `../` thay vì `./`.

- Xóa bỏ `@angular/platform-webworker`.

- Một số type được sửa trong API.

- [InitialNavigation](https://angular.io/api/router/InitialNavigation) bỏ option `enable`, thay vào đó thì dùng `'disabled' | 'enabledBlocking' | 'enabledNonBlocking'`.

- `DatePipe` không làm tròn phần chữ số thập phân thứ 3 (milliseconds) nữa.

- Mảng dữ liệu ngôn ngữ chuyển sang chế độ `read-only`.

- Gọi `overrideProvider` trước khởi tạo `TestBed` sẽ có lỗi.

- `async function` trong `@angular/core/testing` được đổi tên thành `waitForAsync` để tránh nhầm lẫn với cú pháp `JavaScript` `async`.

Ngoài ra còn những `bug fix` và việc cảu thiện hiệu năng khác.

- Từ giờ có thể sử dụng `webpack 5` bằng việc sử dụng `yarn` và thêm `"resolutions": {"webpack": "^5.0.0"}` vào `package.json`. Việc này hứa hẹn bundle size sẽ giảm xuống chăng?

- `Angular Forms` với `async validators` được định nghĩa tại thời điểm khởi tạo trong `class instances` của `FormControl`, `FormGroup` hoặc `FormArray`, khi async validator completed thì event mà `status change` không được gửi đi (emitted). Giờ thì `status event` gửi tới `statusChanges` `observable` (`formControlInstance.statusChanges.subscribe()`).

---

## Sau khi upgrade thành công

Gõ `ng lint` thì ra dòng cảnh báo:

```text
TSLint's support is discontinued and we're deprecating its support in Angular CLI.
To opt-in using the community driven ESLint builder, see: https://github.com/angular-eslint/angular-eslint#migrating-from-codelyzer-and-tslint.
```

Tới tận phiên bản 11, Angular mới có hướng dẫn 1 cách chính thống về việc chuyển `tslint` sang `@typescript-eslint`.

Sau khi xem qua các thay đổi chính thì tôi có thể yên tâm upgrade to `Angular 11` rồi. Ngoài ra bạn có thể xem chi tiết hơn nữa qua `CHANGELOG` ở github tại [đây](https://github.com/angular/angular/blob/master/CHANGELOG.md) nhé.

Icon source lấy ở [đây](https://www.iconfinder.com/icons/308433/angular_front-end_javascript_long_shadow_technologies_web_web_technology_icon).
