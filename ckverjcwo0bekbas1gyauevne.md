# Node.js - lỗi Header overflow khi dùng HTTP request
😞

Nếu bạn dùng HTTP request trong `Node.js` mà gặp lỗi `Header overflow` khi chạy `node` command, thì bạn đã gặp đúng vấn đề của bài viết này rồi.

## Nguyên nhân

Kể từ node `v13.13.0` HTTP protocol parser đã được set cứng:

>Change maximum default size of HTTP headers from 8 KB to 16 KB

Để cho chắc, ta log luôn giá trị mặc định đó ra luôn:

```sh
node
# Welcome to Node.js vxx.x
const http = require("http");
http.maxHeaderSize
# Output: 16384
```

Đây là điều bình thường khi mà các web server khác đều có giới hạn tương tự:

- Apache - 8K
- Nginx - 4K-8K
- IIS - 8K-16K
- Tomcat - 8K – 48K

Mục đích là tránh cho người dùng header lạm dụng header để nhồi nhét quá nhiều thông tin.

Vấn đề là có những khi bạn vẫn phải sử dụng 1 API si-đa nào đó buộc header size rất lớn. 🙄🤔

![confused](https://media.giphy.com/media/lkdH8FmImcGoylv3t3/giphy.gif)

API đó đang cố nhồi nhét thật nhiều thông tin, ngoài những cái hay được set đó là:

- Authorization: thông tin về xác thực tài khoản
- Content-Type: ví dụ `application/json`
- Accept-Charset: ví dụ `utf-8`
- Cache-Control: thông tin có thể tái sử dụng (cache) hay không

## Cách tháo bỏ giới hạn này khi cần thiết

Giới hạn này có thể tháo bỏ bằng cách set params khi chạy node trên command:

```sh
node --max-http-header-size 80000 src/index
# or
node --max-http-header-size=80000 src/index
# giới hạn bây giờ là ~ 80 KB khi chạy `src/index.js`

# cùng kiểm tra lại:
node --max-http-header-size 80000
# or
node --max-http-header-size=80000
# Welcome to Node.js vxx.x
const http = require("http");
http.maxHeaderSize
# Output: 80000
```

Nếu dùng [ts-node](https://typestrong.org/ts-node/) - TypeScript execution and REPL for node.js và [tsconfig-paths](https://github.com/dividab/tsconfig-paths):

```sh
node --max-http-header-size 80000 -r ts-node/register -r tsconfig-paths/register src/index
```

Có 1 vấn đề mà ta thấy ngay đó là command để chạy ứng dụng node trở nên quá dài, nên ta sẽ đặt tên cho nó thông qua `package.json`:

```json
{
  "name": "typescript-node-project",
  "version": "1.0.0",
  "main": "dist/index.js",
  "types": "dist/index.d.ts",
  "engines": {
    "node": ">=14",
    "yarn": ">=1.22"
  },
  "license": "MIT",
  "scripts": {
    "start": "node --max-http-header-size 80000 -r ts-node/register -r tsconfig-paths/register src/index",
    "prod": "node --max-http-header-size 80000 dist/index.js",
  }
}
```

Giờ ta chỉ cần chạy:

```sh
yarn start
yarn prod
```

Để ý là ở đây ta sử dụng `yarn`, ngoài ra các bạn có thể sử dụng `npm`, [pnpm](https://pnpm.io/)...

## Tham khảo

- [tutorial.tips max-http-header-size-in-nodejs](https://tutorial.tips/what-is-the-max-http-header-size-in-nodejs-server/)

- [stackoverflow - nodejs-max-header-size-in-http-request](https://stackoverflow.com/questions/24167656/nodejs-max-header-size-in-http-request)

- [newbedev - nodejs-max-header-size-in-http-request](https://newbedev.com/nodejs-max-header-size-in-http-request)

- [node.js - CLI max HTTP header size](https://nodejs.org/api/cli.html#cli_max_http_header_size_size)

- [Maximum on HTTP header values?](https://stackoverflow.com/questions/686217/maximum-on-http-header-values)

- [apipheny.io/api-headers](https://apipheny.io/api-headers/)

---

Photo by <a href="https://unsplash.com/@refargotohp?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">refargotohp</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
