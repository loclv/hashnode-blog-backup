## TypeScript - tool tự động tạo interface - type 🌱 từ JSON viết bằng JS

## Khi nào bạn cần tool tự động?

Bạn phải sử dụng API của 1 bên thứ 3, từ API đó bạn có file JSON mẫu hoặc example trả về.

Khi mà cấu trức dữ liệu bên trong file JSON quá phức tạp hoặc có quá nhiều JSON.
Theo mình thì JSON trên 10 thuộc tính bao gồm cả thuộc tính con thì được coi là quá phức tạp.
Khi đó, việc copy-paste các thuộc tính chở nên tốn thời gian và nhàm chán.
Đó là lúc mà ta nên dùng tool tự động.

## Bắt tay vào code tool bằng JS

Ở đây cái ta cần là interface hoặc type cho TypeScript, về vài trò check kiểu thì interface hay type đều có thể thay thế cho nhau.
Về sự khác biệt giữa interface và type thì trang chủ của TypeScript cũng đã giải thích tại phần [Differences Between Type Aliases and Interfaces](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces).

### Chuẩn bị

Khởi tạo 1 dự án dùng Node.js hoặc nếu bạn đang có project về frontend, backend, microservice thì có thể bỏ qua.

```sh
mkdir json-to-ts
cd json-to-ts
pnpm init -y
```

Để ý là ở đây ta sử dụng [pnpm](https://pnpm.io/), ngoài ra các bạn có thể sử dụng `npm`, `yarn`...

Ta sẽ dùng [json-to-ts](https://github.com/MariusAlch/json-to-ts).

```sh
pnpm add -D json-to-ts prettier

touch .prettierrc.yaml

# create tool folder
mkdir media/tools
cd media/tools
touch json-to-ts-interface.js

cd ../..

# create example json
mkdir src/mock/json
cd src/mock/json
touch foo.json

cd ../..

# create interface output folder
mkdir data/model

cd ..
```

Thêm nội dung yaml sau vào `.prettierrc.yaml` để code không bẩn nhé:

```yaml
tabWidth: 2
singleQuote: true
printWidth: 80
```

### import từ 1 object thay vì 1 file json

Như ví dụ ở README.md của [json-to-ts](https://github.com/MariusAlch/json-to-ts), ta có thể dùng 1 object thay vì import từ 1 file json.
Thực ra thì khi import từ 1 file json, ta đã phải chuyển nó sang object rồi.

```js
const JsonToTS = require('json-to-ts');

const json = {
  cats: [{ name: 'Kittin' }, { name: 'Mittin' }],
  favoriteNumber: 42,
  favoriteWord: 'Hello',
};

JsonToTS(json).forEach((typeInterface) => {
  console.log(typeInterface);
});

```

Chạy ngay đi:

```sh
node ./media/tools/json-to-ts-interface
```

Output ở `console.log`:

```ts
interface RootObject {
  cats: Cat[];
  favoriteNumber: number;
  favoriteWord: string;
}
interface Cat {
  name: string;
}
```

### import từ 1 file json

Thêm nội dung json sau vào `foo.json` để test (lấy từ [json.org/example.html](https://json.org/example.html)):

```json
{
    "glossary": {
        "title": "example glossary",
        "GlossDiv": {
            "title": "S",
            "GlossList": {
                "GlossEntry": {
                    "ID": "SGML",
                    "SortAs": "SGML",
                    "GlossTerm": "Standard Generalized Markup Language",
                    "Acronym": "SGML",
                    "Abbrev": "ISO 8879:1986",
                    "GlossDef": {
                        "para": "A meta-markup language, used to create markup languages such as DocBook.",
                        "GlossSeeAlso": [
                            "GML",
                            "XML"
                        ]
                    },
                    "GlossSee": "markup"
                }
            }
        }
    }
}
```

Thêm đoạn code sau vào `json-to-ts-interface.js`:

```js
/**
 * Update JSON structure, interface
 *
 * Run: node ./media/tools/json-to-ts-interface
 */

const fs = require('fs');
const os = require('os');

const JsonToTS = require('json-to-ts');

const jsonPath = '../../src/mock/json/';
const fooJson = require(`${jsonPath}foo.json`);

const tsPath = './src/data/model/';

const fooTsPath = `${tsPath}_foo.ts`;

/**
 * JSON to TypeScript Interface
 *
 * @param {object} inputJson - json object
 * @param {string} outputTsPath - output path
 */
const jsonToTsInterface = (inputJson, outputTsPath) => {
  let allTypeInterfaceText = '';
  const strArr = JsonToTS(inputJson);

  // create new lines after each interface
  for (let i = 0; i < strArr.length; i++) {
    const typeInterfaceText = strArr[i];

    console.log(typeInterfaceText);

    /** end of line string */
    let eol;

    // last item or not
    eol = i === strArr.length - 1 ? os.EOL : `${os.EOL}${os.EOL}`;

    // add `export` for using
    allTypeInterfaceText += `export ${typeInterfaceText}${eol}`;
  }

  fs.writeFileSync(outputTsPath, allTypeInterfaceText, 'utf8');
  console.log('🌠 -- done --');
};

jsonToTsInterface(fooJson, fooTsPath);

```

Giải thích thêm về đoạn thêm ký tự xuống dòng (eol), thì package [json-to-ts](https://github.com/MariusAlch/json-to-ts) không tự động xuống dòng với mỗi interface,
nên ta phải tự thêm vào.

![confused](https://media.giphy.com/media/lkdH8FmImcGoylv3t3/giphy.gif)

Chạy ngay đi:

```sh
node ./media/tools/json-to-ts-interface
```

Ta có output là file `_foo.ts`:

```ts
export interface RootObject {
  glossary: Glossary;
}

export interface Glossary {
  title: string;
  GlossDiv: GlossDiv;
}

export interface GlossDiv {
  title: string;
  GlossList: GlossList;
}

export interface GlossList {
  GlossEntry: GlossEntry;
}

export interface GlossEntry {
  ID: string;
  SortAs: string;
  GlossTerm: string;
  Acronym: string;
  Abbrev: string;
  GlossDef: GlossDef;
  GlossSee: string;
}

export interface GlossDef {
  para: string;
  GlossSeeAlso: string[];
}

```

OK, từ `_foo.ts` này ta tự tạo 1 file `foo.ts` theo đúng ý mình, ví dụ thay tên `RootObject` bằng cái tên dễ hiểu hơn.

### Ví dụ khác về loại json

```json
{
    "z": [
        {
            "a": {
                "0": [
                    "3"
                ],
                "1": [
                    "2"
                ],
                "2": []
            }
        },
        {
            "a": {
                "0": [
                    "1"
                ]
            }
        }
    ]
}
```

Output:

```ts
export interface RootObject {
  z: Z[];
}

export interface Z {
  a: A;
}

export interface A {
  '0': string[];
  '1'?: string[];
  '2'?: any[];
}

```

`json-to-ts` cũng xử lý tốt trong trường hợp có thể thuộc tính `undefined` tương ứng dấu `?` trong interface.

---

Photo by <a href="https://unsplash.com/@yauhenihancharenka?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Yauheni Hancharenka</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
