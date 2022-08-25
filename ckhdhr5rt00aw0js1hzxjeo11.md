## Các extension của vscode giúp dự án Angular đỡ khổ 😍

Editor ở đây chúng ta hướng tới là [vscode](https://code.visualstudio.com/) hoặc `vscode-insiders` hoặc [vscodium](https://vscodium.com/).

![Screenshot from 2022-08-25 09-13-15.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661393629780/e6dAngXZu.png align="left")

## 🤖 Code Linter - refactor - formatter

### 🌈 [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Giúp tự động sửa code bẩn (không đúng coding rules) thành đẹp.

Đỡ bực mình khi cả nghìn dòng code bẩn khó sửa chẳng hạn.

Config hữu ích tại settings (ctrl + shift + P + `Open Settings JSON`):

```json
    "[typescript]": {
        "editor.formatOnSave": true,
        "editor.tabSize": 2,
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[html]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[scss]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[yaml]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
```

### 🐭 [EditorConfig for VS Code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig) - must be installed!

Vì khi dùng `Angular CLI` để tự động tạo ra 1 base project thì đã có sẵn  `.editorconfig` rồi.

Tùy theo coding rules mà sửa `.editorconfig` thôi.

### ✅ [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Quan trọng gần nhất, check chính tả, định nghĩa thế nào là cách viết code tệ.

```json
    "eslint.packageManager": "yarn"
```

Do `TSLint` đã không còn được support (update) nữa từ năm 2019, ta nên dùng `ESLint`.

### [TSLint (deprecated)](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)

Tới `Angular 11`, Angular sẽ warning nên dùng [angular-eslint](https://github.com/angular-eslint/angular-eslint) thay thế cho `TSLint`.

### 🛡️ [Angular Language Service](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template)

Với các tính năng:

- Completions lists
- AOT Diagnostic messages: giúp xác định lỗi từ editor thay vì đợi tới lúc compile.
- Quick info
- Go to definition

Thì nó là thằng quan trọng nhất.

Config hữu ích:

```json
    "editor.showUnused": true,
```

### 🌂 [style lint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)

Check chính tả cho `CSS/SCSS/Less`, kiểu như `eslint` nhưng cho style.

Ngoài ra, mình cũng có [bài viết Must-have style-lint basic rules 🎨](https://loclv.hashnode.dev/must-have-style-lint-basic-rules)

### ✏️ [code-spell-checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)

Check chính tả tiếng Anh. Để thằng sau đọc code nó không cười vì đặt tên biến, hàm ngu.

## 🐪 Lối tắt

### [Angular 10 Snippets](https://marketplace.visualstudio.com/items?itemName=Mikael.Angular-BeastCode)

Tạo ra cả 1 component full đồ khi chỉ cần gõ `ng-component` vào file trống chẳng hạn.

### [angular-schematics](https://marketplace.visualstudio.com/items?itemName=cyrilletuzi.angular-schematics)

Extension cho những ai lười gõ command khởi tạo `component`, `service`... hoặc không nhớ command.

- Thay thế cho Angular CLI (command line) bằng UI.
- Không còn nhưng lỗi typo - gõ sai chính tả ngớ ngẩn.
- Support nhiều option cho từng loại:

![Screenshot from 2021-06-03 12-56-15.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1622699798979/arKrb9OUp.png)

### 🧘 [Angular Zen Mode](https://marketplace.visualstudio.com/items?itemName=dolliecollective.angular-zen-mode&ref=producthunt)

Tự động chia màn hình thành 3 phần của Component:

- Code (.ts) chiếm 2/4 màn hình
- Template (.html) chiếm 1/4 màn hình
- Style (.css/.scss/.sass/.less) chiếm 1/4 màn hình

### [auto-rename-tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag)

Thằng này thì cái tên đã nói lên tất cả rồi. :v

### [angular2-switcher](https://marketplace.visualstudio.com/items?itemName=infinity1207.angular2-switcher)

Khi mà bạn bị bắt không được code kiểu inline (kiểu chung `html` và `ts` 1 file) hay là bạn thích tách riêng các file ra, thì việc chuyển qua lại giữa các file của 1 component là chuyện thường xuyên.

Đã có `angular2-switcher`, switch giữa các kiểu file: typescript(.ts)|template(.html)|style(.scss/.sass/.less/.css) trong cùng 1 component với 1 loạt phím tắt nhanh và tiện.

### 📐 [arrr](https://marketplace.visualstudio.com/items?itemName=obenjiro.arrr)

- Gom HTML được bôi dên thành 1 component mới.
- Tự động nhận biết và tạo `@Input()` cho component đó.
- Generates HTML, CSS, TS và spec files.

![extract-to-dir.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1623570842659/FEpXDBsbC.gif)

### [Paste JSON as Code](https://marketplace.visualstudio.com/items?itemName=quicktype.quicktype)

Chuyển file `JSON` sang `Typescript` và các ngôn ngữ khác.

### 🚀 [turbo-console-log](https://marketplace.visualstudio.com/items?itemName=ChakrounAnas.turbo-console-log)

Tạo `console.log` siêu nhanh bằng cách bôi đen biến cần log và ấn `ctrl + alt + L`.

![insert_log_message.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1623570933189/fvN0o9qqE.gif)

## 🌅 Syntax highlighting

### [angular2-inline](https://marketplace.visualstudio.com/items?itemName=natewallace.angular2-inline)

Dành cho tín đồ thích code 1 file chung có hết typescript, style (css, scss..), html - kiểu như react-native.

Và tôi cũng thích kiểu này. 😄

### [vscode-angular-html](https://marketplace.visualstudio.com/items?itemName=ghaschel.vscode-angular-html)

>Syntax highlighting for angular HTML template files.

![angular-directives.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1622700058487/6k-Z9E3iE.gif)

### 🌄 [markdown-preview-enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)

Tăng trình viết tài liệu dự án (README.md).

Thêm cả thằng [markdown lint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) nữa cho bá.

```json
    "markdown-preview-enhanced.codeBlockTheme": "monokai.css",
    "markdown-preview-enhanced.revealjsTheme": "black.css",
    "markdown-preview-enhanced.previewTheme": "atom-dark.css",
    "markdown-preview-enhanced.mermaidTheme": "dark",
    "markdown-preview-enhanced.liveUpdate": true,
    "markdown.preview.fontSize": 11,
```

### 🌓 [swagger-viewer](https://marketplace.visualstudio.com/items?itemName=Arjun.swagger-viewer)

Rất hữu dụng khi design + test + mock API theo chuẩn `openapi` hay `swagger`.

![swagger-preview.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1623570966495/DFaMxINn1.gif)

Nếu file `yaml` quá dài ảnh hưởng tới hiệu năng đọc file thì giới hạn:

```json
    "yaml.maxItemsComputed": 512,
```

### [svg-preview](https://marketplace.visualstudio.com/items?itemName=SimonSiefke.svg-preview)

Xem ảnh SVG từ mớ bùng nhùng `svg-tag`.

### [deepdark-material theme](https://marketplace.visualstudio.com/items?itemName=Nimda.deepdark-material)


![59273175-41c9bd00-8c60-11e9-917e-15a296b7f0fa.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1623570791959/8WQyhU0Fb.png)

Cùng với settings (ctrl + shift + P + `Open Settings JSON`):

```json
{
    "editor.cursorSmoothCaretAnimation": true,
    "editor.cursorBlinking": "expand",
    "workbench.colorTheme": "Deepdark Material Theme | Full Black Version",
}
```

### [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)

Giúp bạn dễ phân biệt các loại file trong Angular như Component, Service, ...

![Screenshot from 2021-01-14 18-07-38.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610622609256/FAx5S85Dp.png)

Thì đây là theme ưu thích của mình.

## ✔️ Unit test

### [Karma Problem Matcher](https://marketplace.visualstudio.com/items?itemName=rctay.karma-problem-matcher)

Bắt lỗi ngay trên vscode thay vì trên browser.

### [SimonTest](https://marketplace.visualstudio.com/items?itemName=SimonTest.simontest)

Tự động tạo ra `mock` `service` cho `TestBed` và `never have to worry about hitting the real services`. 😃

### [angular-karma-test-explorer](https://marketplace.visualstudio.com/items?itemName=raagh.angular-karma-test-explorer)

![img-running-tests-readme.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1623570889528/9sbtl1Hm4.png)

- Run và Reload tests bằng run, reload button ngay trên UI vscode.
- Xem results ngay trên UI.
- Debug tests, shows log của test thất bại ngay trên dòng source code mà nó failed.

---

### [Angular Extension Pack](https://marketplace.visualstudio.com/items?itemName=loiane.angular-extension-pack)

Nếu các bạn lười install hay quản lý đống extentions riêng cho Angular, bạn có thể dùng cái này. Hay tìm hiểu thêm extentions khác hữu ích mà mình chưa biết.

## Other `settings.json` and extentions

### Settings

Để mở `settings.json` thì ta ấn: `Ctrl` + `Shift` + `P` -> gõ `settings` -> tìm lựa chọn `settings bằng JSON`.

Edit `settings.json` để default UI/UX xịn hơn:

```json
    "editor.cursorSmoothCaretAnimation": true,
    "editor.cursorBlinking": "expand"
```

Nếu máy bạn đang cài `Fira Code` font thì setting:

```json
    "editor.fontFamily": "'Fira Code'",
    "editor.fontLigatures": true,
    "editor.fontWeight": "300",
```

### Other extentions

- [Browserslist syntax highlight](https://marketplace.visualstudio.com/items?itemName=webben.browserslist)
- [ErrorLens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens): hiển thị ngay error và warning với highlighting không cần hover bằng chuột.
- [Mintlify Doc Writer for Python, JavaScript, TypeScript, C++, PHP, Java, C#, Ruby & more](https://marketplace.visualstudio.com/items?itemName=mintlify.document): tự gen ra jsdoc  dựa trên source-code.
- [export-typescript](https://marketplace.visualstudio.com/items?itemName=mscolnick.export-typescript)
