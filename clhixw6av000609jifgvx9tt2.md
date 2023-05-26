---
title: "node package manager - Vì sao nên định kỳ chạy npm audit? Một lý do khiến ta phải lưu package lock file trong source code với git"
datePublished: Thu May 11 2023 09:41:05 GMT+0000 (Coordinated Universal Time)
cuid: clhixw6av000609jifgvx9tt2
slug: node-package-manager-vi-sao-nen-dinh-ky-chay-npm-audit-mot-ly-do-khien-ta-phai-luu-package-lock-file-trong-source-code-voi-git
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/aIYFR0vbADk/upload/338e2b48f553342164b209571f314f9b.jpeg
tags: npm-audit-vietnamese, npm-vietnamese

---

## Phát hiện vấn đề

Một hôm đẹp trời, khi nhìn vào log CICD, chỗ output của `npm i`:

```markdown
xxx packages are looking for funding
  run `npm fund` for details

x vulnerabilities (x moderate, x high)

To address all issues, run:
  npm audit fix

Run `npm audit` for details.
```

Oh shit! Rõ ràng 1 tháng trước mình vừa chạy `npm audit` và đã fix hết các lỗ hổng bảo mật rồi mà hôm nay lại lòi ra? Đó là vì dự án không thường xuyên chạy `npm audit`. Ta thử chạy lại xem sao:

```bash
npm audit
```

Output:

```markdown
# npm audit report

engine.io  5.1.0 - 6.4.1
Severity: moderate
engine.io Uncaught Exception vulnerability - https://github.com/advisories/GHSA-q9mw-68c2-j6m5
fix available via `npm audit fix`
node_modules/engine.io
  socket.io  4.1.0 - 4.6.0-alpha1
  Depends on vulnerable versions of engine.io
  node_modules/socket.io

yaml  2.0.0-5 - 2.2.1
Severity: high
Uncaught Exception in yaml - https://github.com/advisories/GHSA-f9xv-q969-pqx4
fix available via `npm audit fix`
node_modules/yaml

3 vulnerabilities (2 moderate, 1 high)

To address all issues, run:
  npm audit fix
```

Đơn giản là chạy:

```bash
npm audit fix
```

Ta thấy `package-lock.json` đã update với `git diff`. Xác nhận lại bằng cách chạy `npm audit` 1 lần nữa, vấn đề được giải quyết! Đến đây có thể xác định rằng `npm audit` nên được chạy định kỳ 1 khoảng thời gian nhất định.

Expected output:

> found 0 vulnerabilities

## Tìm hiểu sâu hơn

Ta thấy `package-lock.json` đã được update mà không phải `package.json` là do ta hay viết `devDependencies` or `dependencies`:

```json
{
    "devDependencies": {
        "xxx-package-name": "^1.1.1"
    }
}
```

`"^1.1.1"` chấp nhận `"^1.1.x"` với `x >= 1`, thế nên `package-lock.json` rất quan trọng và cần phải lưu lại trong source code với git.

Tìm hiểu thêm `npm audit` output thì ta thấy:

[https://github.com/advisories/GHSA-q9mw-68c2-j6m5](https://github.com/advisories/GHSA-q9mw-68c2-j6m5)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683797179424/89ec3fdf-aad9-4197-92d1-f952e9ac3044.png align="center")

Dò theo `git diff` thì ta thấy `yaml` package được update là dependencies requires của `lint-staged`.

Vào releases note của [https://github.com/okonet/lint-staged/releases/tag/v13.2.2](https://github.com/okonet/lint-staged/releases/tag/v13.2.2):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683797413246/0bf79ea2-c105-4354-bd89-c51b95b9a9b1.png align="center")

Như vậy ta có thể set luôn `"lint-staged": "^13.2.2"` trong `package.json` rồi chạy:

```bash
npm i
# fix other vulnerabilities
npm audit fix
# expected output: found 0 vulnerabilities
```

## Tổng kết

* Các lỗ hổng bảo mật có thể chưa được phát hiện, nó có thể được phát hiện vào tương lai, vậy nên để an toàn chúng ta cần thiết nên audit định kỳ, điều mà các github bot vẫn làm thay chúng ta.
    
* Việc đặc tả version chính xác cũng quan trọng không kém, đó là lý do tại sao `package-lock.json` (đối với npm) ra đời.