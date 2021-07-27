## 🧪 SonarQube - Tìm hiểu Rules cho TypeScript - về các lỗ hổng bảo mật 🔓 - phần 2

Chi tiết rule tham khảo tại [sonarsource rules for typescript - vulnerabilities](https://rules.sonarsource.com/typescript/type/Vulnerability/RSPEC-6096).

Rule này thuộc loại lỗ hổng có thể bị lợi dụng - vulnerabilities.

## 🤤 Việc giải nén không nên dẫn tới lỗ hổng `zip slip`

>Extracting archives should not lead to zip slip vulnerabilities

Khái niệm `zip slip` là khi kẻ tấn công truyền command line của OS (operating system)
hay `file system` thông qua các tên file bên trong 1 file zip.

Mục đích là đọc, sửa, xóa các dữ liệu nhạy cảm.

Lỗ hổng này bị lợi dụng do thông thường người dùng hay code không kiểm soát tên các file bên trong 1 file đã được nén lại.

### 🤔 Ví dụ đoạn code vi phạm

```ts
const AdmZip = require('adm-zip');
const fs = require('fs');

const zip = new AdmZip("zip-slip.zip");
const zipEntries = zip.getEntries();
zipEntries.forEach(function (zipEntry) {
  fs.createWriteStream(zipEntry.entryName); // Noncompliant 😨
});
```

Phần `Noncompliant` nghĩa là không được tuân thủ.

`entryName` hồn nhiên được sử dụng lại, đây chính là lỗ hổng bị khai thác.

### Giải pháp tuân thủ rule

Valid URL trước khi redirect.


```ts
const AdmZip = require('adm-zip');
const pathmodule = require('path');
const fs = require('fs');

const zip = new AdmZip("zip-slip.zip");
const zipEntries = zip.getEntries();
zipEntries.forEach(function (zipEntry) {
  let resolvedPath = pathmodule.join(__dirname + '/archive_tmp', zipEntry.entryName); // join will resolve "../"

  if (resolvedPath.startsWith(__dirname + '/archive_tmp')) {
    // the file cannot be extracted outside of the "archive_tmp" folder
    fs.createWriteStream(resolvedPath); // Compliant 😌
  }
});
```

Phần `Compliant` nghĩa là đã tuân thủ.

Với `pathmodule.join`, ta không cho phép các kẽ hở `../` liên quan tới string bị khai thác.
Kẻ tấn công không đưa commands vào được.

`resolvedPath.startsWith` đảm bảo rằng file không thể bị upzip bên ngoài thư mục đã chỉ định sẵn mà ở đây là ``archive_tmp.

---

Photo by <a href="https://unsplash.com/@kfc0105?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Kenta Miyahara</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
