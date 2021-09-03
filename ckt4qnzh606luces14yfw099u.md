## ✅ Check-list và 📝 note khi tạo base source-code cho Angular - phần 1 - CLI packages và Unit Test

Những ghi chú mà có thể bạn phải rút kinh nghiệm sâu sắc, vì dự án không có thì giờ để refactor và test lại khi số lượng màn hình quá lớn.

>Sai 1 ly đi 1 dặm.

## Khi khởi tạo dự án với Angular CLI

[Angular CLI](https://angular.io/cli) kể từ Angular 12 sẽ defalt bật [strict mode](https://angular.io/guide/strict-mode) nên bạn không cần lo lắng gì với v12 trở lên. Còn nếu trong 1 số ít trường hợp, tạo version < v12 thì mới cần chú ý là phải set thêm tham số cho `strict-mode` thôi.

Do Angular thường xuyên được update nên cứ cài lại - tương đương với upgrade `CLI` cho chắc cú, mà cũng đỡ phải chạy `ng --version` để kiểm tra phiên bản mới nhất hay không:

```sh
pnpm i -g @angular/cli
# output: Progress: resolved 237, reused 237, downloaded 0, added 0, done
```

Ở đây mình dùng [pnpm](https://pnpm.io/) thay vì `npm` để tiết kiệm dung lượng ổ cứng và [cho hiệu năng tốt hơn](https://pnpm.io/benchmarks).

```sh
ng new test-pnpm --skip-install
```

Nếu không có option `--skip-install` thì tự động `ng` sẽ cài packages bằng `npm`, mà mình thì đang không muốn dùng `npm`. Do không cài packages nên khởi tạo dự án cực nhanh.

`ng` sẽ hỏi bạn muốn:

>? Would you like to add Angular routing? Yes

Tùy nhu cầu của bạn mà hầu hết dự án nào cũng cần routing thôi, nên chọn `Yes`.

>? Which stylesheet format would you like to use? [SCSS](https://sass-lang.com/documentation/syntax#scss)

Tùy sở thích của bạn tuy nhiên để hợp với cả team nhiều người thì nên chọn phổ biến nhất là [SCSS](https://sass-lang.com/documentation/syntax#scss).

### Packages manager

Khi không dùng `npm` làm packages manager thì ta phải set lại:

```sh
ng config cli.packageManager pnpm
```

Kết quả là file `angular.json` được tự động sửa lại:

```diff
+  "cli": {
+    "packageManager": "pnpm"
+  },
```

`yarn` cũng là 1 trong những `packageManager` phổ biến thay thế `npm`.
Tuy nhiên nếu ổ cứng lưu trữ của bạn bị giới hạn như trên cloud service như AWS thì nên nghĩ lại, bạn không nên dùng `yarn`.
Theo như [issue yêu cầu yarn](https://github.com/yarnpkg/yarn/issues/986) cho phép bỏ qua `global cache`, thì yarn sẽ mặc định cài packages vào thư mục `global cache` rồi mới copy sang `node_modules` của dự án.

Điều này làm tăng gấp đôi bộ nhớ cho ổ cứng khi cần thiết để cài đặt packages. Đừng nghĩ dung lượng `node_modules` là nhỏ nhé, mình đã từng có dự án 833,9 MB on disk cho 82.987 items.
Và thế là dự án phải tăng chi phí bộ nhớ cho con server dùng để test. Đúng là:

>Mọi sai lầm đều phải trả giá bằng tiền mặt - thằng bạn nói.

![node_modules-meme.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1630692609546/9dDqPhTjX.jpeg)

Nguồn ảnh tại Google với từ khóa `node_modules jokes`.

Như 1 [comment](https://github.com/yarnpkg/yarn/issues/986#issuecomment-828443754) như sau:

>I'm trying to install a package inside of AWS Lambda, which has a 512 MB disk limit and only allows me to write to /tmp. If I just install my package, I'm well under the disk limit, but the yarn cache is making me exceed the disk limit by doubling the amount of disk used. I can't just remove the cache afterwards as it causes the yarn install to fail.

### Update packages

Về chuyện update packages thì update luôn từ đầu cho đỡ mệt, sau này code nhiều lên mà update version thì phải test lại hết đấy.

Trong nhiều trường hợp `ng update` không thực sự update các dependencies. Thế nên chốt luôn là dùng command của package manager cho nhanh:

```sh
pnpm up
```

## Unit Test

Mặc định, [Karma](https://karma-runner.github.io/latest/index.html) + `jasmine` sẽ được cài đặt vào phần `devDependencies` của `package.json`.
Tuy nhiên, cái dự án dài 1 năm của mình đã chứng minh rằng với số lượng Test case cự lớn, tương ứng với số lượng màn hình khoảng 600 màn thì nó phải chạy mất 25 phút.
Thử tưởng tượng xem nếu có cái CI/CD nào chạy Unit test mỗi lần có `pull request` xem.
Phải đợi bao lâu để `pull request` được review đây?!

![cry](https://media.giphy.com/media/XoW2jShBRKkxO/giphy.gif)

Như vậy tốc độ chạy test cũng rất quan trọng.
Theo như các bài viết trên mạng như [Make your Angular tests 1000% better by switching from Karma to Jest](https://dev.to/dylanwatsonsoftware/make-your-angular-tests-1000-faster-by-switching-from-karma-to-jest-1n33) thì [Jest](https://jestjs.io/) nhanh hơn.
Nguyên nhân có thể là `Jest` dùng [jsDOM](https://github.com/jsdom/jsdom) có hiệu năng cao hơn `targeted browser`.
Tuy có rủi ro khi không dùng `targeted browser` và `jsDOM` không trực quan bằng khi debugging, nhưng đại đa số dự án có thể dùng `Jest` thay thế được.

Ngoài ra còn 1 lý do nữa nên dùng `Jest` đó là nó được cộng đồng sử dụng nhiều hơn, dùng được với React, Vue, Svelte... luôn. Ta chỉ mất công học tool cho Unit test 1 lần thôi. Hơn nữa [eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest) cũng ngon nữa. Để phần sau mình sẽ nói về `eslint` cho Angular.

Thay [Karma](https://karma-runner.github.io/latest/index.html) bằng [Jest](https://jestjs.io/) thì nên tham khảo bài [Replace Karma With Jest](https://bjanderson.github.io/replace-karma-with-jest/).
Còn nếu dự án không có kế hoạch viết Unit test thì ta nên xóa `Karma` + `jasmine` cho gọn.

---

Photo by <a href="https://unsplash.com/@dtopkin1?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Dayne Topkin</a> on <a href="https://unsplash.com/s/photos/begin?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
