## Các extension của vscode giúp dự án Angular đỡ khổ

Editor ở đây chúng ta hướng tới là [vscode](https://code.visualstudio.com/) hoặc `vscode-insiders`.

## Editor Extensions

### [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Giúp tự động sửa code bẩn (không đúng coding rules) thành đẹp.

Đỡ bực mình khi cả 1000 dòng code bẩn khó sửa chẳng hạn.

### [EditorConfig for VS Code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig) - must be installed!

Vì khi dùng `Angular CLI` để tự động tạo ra 1 base project thì đã có sẵn  `.editorconfig` rồi.

Tùy theo coding rules mà sửa `.editorconfig` thôi.

### [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Quan trọng gần nhất, check chính tả, định nghĩa thế nào là cách viết code tệ.

Do TSLint đã không còn được support (update) nữa từ năm 2019 nên phải dùng thêm `ESLint`.

### [TSLint (deprecated)](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)

Quan trọng gần nhất tại thời điểm hiện tại, do tới `Angular 10` mà `ESLint` vẫn chưa được hỗ trợ sau bao lần lỡ hẹn với cộng đồng (xem thêm tại [đây](https://github.com/angular/angular-cli/issues/13732)).

### [Angular Language Service](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template)

Với các tính năng:

- Completions lists
- AOT Diagnostic messages
- Quick info
- Go to definition

Thì nó là thằng quan trọng thứ 3.

### [Angular 10 Snippets](https://marketplace.visualstudio.com/items?itemName=Mikael.Angular-BeastCode)

Tạo ra cả 1 component full đồ khi chỉ cần gõ `ng-component` vào file trống chẳng hạn.

### [angular-schematics](https://marketplace.visualstudio.com/items?itemName=cyrilletuzi.angular-schematics)

1 extension cho những ai lười gõ command khởi tạo `component`, `service`... hoặc không nhớ command.

- Thay thế cho Angular CLI (command line) bằng UI.
- Không còn nhưng lỗi typo - gõ sai chính tả ngớ ngẩn.
- Support nhiều option cho từng loại:

![Screenshot from 2021-06-03 12-56-15.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1622699798979/arKrb9OUp.png)

### [angular2-inline](https://marketplace.visualstudio.com/items?itemName=natewallace.angular2-inline)

Dành cho tín đồ thích code 1 file chung có hết typescript, style (css, scss..), html - kiểu như react-native.

Và tôi cũng thích kiểu này. :v

### [vscode-angular-html](https://marketplace.visualstudio.com/items?itemName=ghaschel.vscode-angular-html)

>Syntax highlighting for angular HTML template files.


![angular-directives.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1622700058487/6k-Z9E3iE.gif)

### [code-spell-checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)

Check chính tả tiếng Anh. Để thằng sau đọc code nó không cười vì đặt tên biến, hàm ngu.

### [markdown-preview-enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)

Tăng trình viết tài liệu dự án (README.md).

Thêm cả thằng [markdown lint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) nữa cho bá.

### [auto-rename-tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag)

Thằng này thì cái tên đã nói lên tất cả rồi. :v

### [angular2-switcher](https://marketplace.visualstudio.com/items?itemName=infinity1207.angular2-switcher)

Khi mà bạn bị bắt không được code kiểu inline (kiểu chung `html` và `ts` 1 file) hay là bạn thích tách riêng các file ra, thì việc chuyển qua lại giữa các file của 1 component là chuyện thường xuyên.

Đã có `angular2-switcher`, switch giữa các kiểu file: typescript(.ts)|template(.html)|style(.scss/.sass/.less/.css) trong cùng 1 component với 1 loạt phím tắt nhanh và tiện.

### [style lint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)

Check chính tả cho `CSS/SCSS/Less`, kiểu như `eslint` nhưng cho style.

### [Paste JSON as Code](https://marketplace.visualstudio.com/items?itemName=quicktype.quicktype)

Chuyển file `JSON` sang `Typescript` và các ngôn ngữ khác.

### [Angular Extension Pack](https://marketplace.visualstudio.com/items?itemName=loiane.angular-extension-pack)

Nếu các bạn lười install hay quản lý đống extentions riêng cho Angular, bạn có thể dùng cái này. Hay tìm hiểu thêm extentions khác hữu ích mà mình chưa biết.

### [Karma Problem Matcher](https://marketplace.visualstudio.com/items?itemName=rctay.karma-problem-matcher)

Bắt lỗi ngay trên vscode thay vì trên browser.

### [SimonTest](https://marketplace.visualstudio.com/items?itemName=SimonTest.simontest)

Tự động tạo ra `mock` `service` cho `TestBed` và `never have to worry about hitting the real services`. 😃

### [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)

Giúp bạn dễ phân biệt các loại file trong Angular như Component, Service, ...

![Screenshot from 2021-01-14 18-07-38.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610622609256/FAx5S85Dp.png)