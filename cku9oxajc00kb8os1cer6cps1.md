## ✅ Check-list và 📝 note khi tạo base source-code cho Angular - phần 2 - eslint

Tiếp nối [phần 1 - ✅ Check-list và 📝 note khi tạo base source-code cho Angular](https://loclv.hashnode.dev/check-list-va-note-khi-tao-base-source-code-cho-angular-phan-1-cli-packages-va-unit-test), phần này mình sẽ tập chung vào `eslint`.

Chú ý trong bài viết mình sẽ sử dụng alias của 3 mức độ của rule trong eslint. Ví dụ dùng `2` chứ không dùng `"error"`:

- "off" or 0 - turn the rule off
- "warn" or 1 - turn the rule on as a warning (doesn't affect exit code)
- "error" or 2 - turn the rule on as an error (exit code will be 1)

## angular-eslint

[angular-eslint](https://github.com/angular-eslint/angular-eslint)

Đối với phiên bản v12 trở đi, hãy để `ng` làm hết cho ta:

```sh
ng add @angular-eslint/schematics
```

Và thế là xong, ta đã có `.eslintrc.json` xịn bao gồm cả các plugin:

```json
// "*.ts"
{
  "extends": [
    "plugin:@angular-eslint/recommended",
    "plugin:@angular-eslint/template/process-inline-templates"
  ],

// "*.html"
  "extends": [
    "plugin:@angular-eslint/template/recommended"
  ],
}

```

Từ giờ ta có thể lint toàn project bằng:

```sh
pnpm lint
# or
yarn lint
# or
npm run lint
```

Ngoài ra còn có thể dùng thêm [eslint-plugin-rxjs](https://github.com/cartant/eslint-plugin-rxjs).

### Linting HTML files và inline-templates với VSCode extension

Trước hết `inline-templates` là kiểu viết template bên trong `.ts` code.

Để [eslint extention](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) chạy tốt thì ta thêm setting vào `settings.json`:

```json
// ... more config

"eslint.options": {
  "extensions": [".ts", ".html"]
},

// ... more config

"eslint.validate": [
  "javascript",
  "javascriptreact",
  "typescript",
  "typescriptreact",
  "html"
],

// ... more config
```

## Các rule nên thêm

```json
{
  "overrides": [
    {
      "files": ["*.ts"],
      // ... more config

      "rules": {
        "no-console": 1,
        "no-alert": 2,
        "no-useless-concat": 2,
        "prefer-template": 2,
        "template-curly-spacing": 2

        // ... more config
      }

      // ... more config
    },
}
```

- `"no-console": 1` là warning khi dùng `console`
- `"no-alert": 2` là báo lôi khi dùng `alert`
- `"no-useless-concat": 2` báo lỗi khi dùng toán tử `+` để làm những việc vô nghĩa, ví dụ:

```js
// đừng :(
const str = "Hello, " + "World!"

// viết luôn thế này đi :)
const greeting = "Hello, World!"
```

- ` "prefer-template": 2` không cho dùng:

```js
// đừng
var str = "Hello, " + name + "!";
var str = "Time: " + (12 * 60 * 60 * 1000);

// dùng thế này đi (kiểu template)
var str = `Hello, ${name}!`;
var str = `Time: ${12 * 60 * 60 * 1000}`;
```

Cách viết kiểu `template` đúng chuẩn ES đời mới mà dễ đọc và nhanh hơn chuẩn cũ. Phép `template` cũng chỉ dùng với String, type cũng chặt hơn.

### Hạn chế code dài, khó bảo trì, khó hiểu

```json
        "max-lines": [
          2,
          400
        ]
```

Giới hạn số lượng dòng code tối đa là 400 dòng (ví dụ trên). Nếu lớn hơn thì cần tách code ra file khác.

```json
        "max-len": [
          2,
          {
            "code": 120
          }
        ]
```

Giới hạn số lượng ký tự 1 dòng code, tối đa là 120 ký tự 1 dòng chẳng hạn. Dự án cá nhân thì mình để 80 ký tự thôi để code chia đôi màn hình cho dễ nhìn.
Nếu lớn hơn thì cần tách code xuống dòng. Khi lượng code 1 dòng không quá lớn thì tiện đọc code hơn rất nhiều, bạn cứ thử mà xem!

Thường thì cả team đều sử dụng [prettier](https://prettier.io/) và không có thực tập sinh thì có thể bỏ qua rule này vì prettier đã xuống dòng cho mình rồi. Trong trường hợp đó, xóa rule này đi cho đỡ nặng eslint. Tuy nhiên, nhỡ có thanh niên nào không chịu bật prettier plugin ở editor lên thì phải bật rule này lên.

```json
"max-lines-per-function": [2, 127]
```

Giới hạn số lượng dòng code tối đa 1 function là 127 dòng (ví dụ trên). Nếu lớn hơn thì cần tách code ra function khác.

```json
"@typescript-eslint/no-empty-interface": 2
```

Không cho phép `interface` rỗng.

```json
        "@angular-eslint/directive-selector": [
          2,
          {
            "type": "attribute",
            "prefix": "app",
            "style": "camelCase"
          }
        ]
```

Luật dành riêng cho Angular, `directive-selector` - tên của `directive` phải có tiền tố là `app` để phân biệt với các `directive` không được tạp ra bởi App, ví dụ `directive` từ thư viện bên thứ 3.

```json
        "@angular-eslint/component-selector": [
          2,
          {
            "type": "element",
            "prefix": "app",
            "style": "kebab-case"
          }
        ]
```

Tương tự với `component`.

[no-else-return](https://eslint.org/docs/rules/no-else-return):

```json
"no-else-return": 2
```

Ví dụ, đoạn code dưới đây khá là rườm rà:

```js
function foo() {
    if (x) {
        return y;
    } else {
        return z;
    }
}
```

Thực ra chỉ cần:

```js
function foo() {
    if (x) {
        return y;
    }

    return z;
}
```

Nếu bạn muốn check xem có biến nào không được sử dụng từ bước coding trên editor mà chưa cần TypeScript build ra lỗi đó thì có thể dùng [no-unused-vars](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/no-unused-vars.md) từ `typescript-eslint`.

```json
"no-unused-vars": 0,
"@typescript-eslint/no-unused-vars": [2],
```

Ngoài ra, còn rất nhiều rule hay ho mà mình chưa thể nói hết ở bài này!

![magic](https://media.giphy.com/media/WU8nnAdxZWeM8/giphy.gif)

## Cách đặt tên

Luật đặt tên là cần thiết nếu team hoặc khách hàng yêu cầu đặt tên theo chuẩn, ví dụ `interface` phải dùng chữ `I` (viết hoa) trước mỗi tên interface. Việc viết tên như thế khiến ta hiểu ngay đó là 1 interface chứ không nhầm với `type` hoặc class chẳng hạn.

Ta sử dụng `@typescript-eslint`:

```json
        "@typescript-eslint/naming-convention": [
          2,
          {
            "selector": "interface",
            "format": ["StrictPascalCase"],
            "custom": {
              "regex": "^I[A-Z]",
              "match": true
            }
          },
          {
            "selector": "variable",
            "format": ["strictCamelCase", "UPPER_CASE", "snake_case"]
          },
          {
            "selector": "typeParameter",
            "format": ["PascalCase"],
            "prefix": ["T"]
          },
          {
            "selector": "variable",
            "types": ["boolean"],
            "format": ["PascalCase"],
            "prefix": ["is", "should", "has", "can", "did", "will"]
          },
          {
            "selector": "enum",
            "format": ["PascalCase"]
          },
          {
            "selector": "enumMember",
            "format": ["PascalCase"]
          }
        ]
```

## Dùng eslint để bắt buộc viết doc/comment cho method/function

Nếu khách hàng yêu cầu viết doc cho toàn bộ method/function thì mình nên dùng cái này. Ngược lại nếu không yêu cầu thì chỉ nên viết khi cần thiết, tiện và linh hoạt hơn, nên bạn có thể bỏ qua phần này.

Bạn có thể dùng [eslint-plugin-require-jsdoc-except](https://github.com/MaienM/eslint-plugin-require-jsdoc-except).

Sau khi cài đặt như hướng dẫn bên trên thì ta có thể config:

```json
{
        "plugins": [
          // other plugin
		  "require-jsdoc-except"
	    ]
  // other config

        "require-jsdoc-except/require-jsdoc": [2, {
          "require": {
            "FunctionDeclaration": true,
            "MethodDefinition": true,
            "ClassDeclaration": false,
            "ArrowFunctionExpression": false,
            "FunctionExpression": false
          },
          "ignore": [
            "constructor",
            "ngOnChanges",
            "ngOnInit",
            "ngDoCheck",
            "ngAfterContentInit",
            "ngAfterContentChecked",
            "ngAfterViewInit",
            "ngAfterViewChecked",
            "ngOnDestroy"
          ]
        }],
        "valid-jsdoc": [2, {
          "requireReturn": false,
          "requireReturnType": false,
          "requireParamType": false
        }],
}
```

Trong đó:

- `ClassDeclaration` quyết định xem có cần viết comment hay không. Tương tự với `MethodDefinition`, `FunctionDeclaration`...
- `ignore` sẽ loại bỏ tên những method không cần viết jsdoc.

---

Photo by <a href="https://unsplash.com/@daniele71043?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Daniele Colucci</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
