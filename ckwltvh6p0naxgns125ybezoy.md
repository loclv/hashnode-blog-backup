## Node.js - TypeScript - ssh2-sftp-client package - phần 2 - fast download upload  📂 🍻

Tiếp nối phần 1 - [dùng ssh2-sftp-client với SFTP server tự tạo trên localhost - kết nối](https://loclv.hashnode.dev/nodejs-typescript-dung-ssh2-sftp-client-voi-sftp-server-tu-tao-tren-localhost-phan-1-ket-noi), bài này sẽ nói về cách download và upload file.

## Khởi đầu và kết thúc

Ở phần trước mình quên chưa giải thích đoạn `new Client('download-test-json-client')` thay vì `new Client()`. Đoạn string đó input vào thì ta có thể định danh client mà mình đang làm việc cùng là client nào. Nó hữu ích khi bạn chạy nhiều client cùng 1 lúc mà khi muốn debug rằng client nào đang gặp vấn đề. Thế nên ta cần định danh cho nó. Tuy nhiên nếu chỉ có 1 client instance thì không đặt tên cũng không sao.

Đó là 1 chú ý nhỏ phần khởi đầu, còn phần kết thúc thì tất nhiên chúng ta phải ngắt kết nối tới SFTP server rồi.

Phương thức thực hiện như sau để tóm gọn các lỗi về môi trường:

```ts
let sftp;

try {
  sftp = await sftpConnect('localhost', 22, 'newUser', 'newUser');

  // TODO
} catch (err: any) {
  console.log(err, 'catch error');
} finally {
  if (sftp) {
    sftp.end();
  }
}
```

Khi chạy xong đoạn code trong phần `TODO` ta sẽ thấy tiến trình tự động kết thúc vì connection đã bị ngắt.

## Symbolic link

`Symbolic link` trên linux cũng giống như việc tạo shortcut trên windows vậy, nó tạo 1 lối tắt tới 1 file/folder nằm sâu trong cây thư mục. Ta sẽ thử tạo 1 link xem ssh2-sftp-client package sẽ trả về gì:

```sh
sudo ln -s /sftp/files/test.js /sftp/symlink-test
ll /sftp/
# output: symlink-test -> /sftp/files/test.js
```

Sử dụng:

```ts
path = '/symlink-test';
type = await sftp.exists(path);
console.log(`🔗 ~ ${path} type: `, type);
```

Output là `link ~ /symlink-test type: false`. Đối với `Symbolic link` kết quả kiểm tra kiểu trả về false.

## Download & Upload cơ bản

### Xác định mục tiêu

Bước xác định mục tiêu cần download, ta có thể dùng method `exists(path)` luôn hoặc muốn kiểm tra các thông tin của file chi tiết hơn ta dùng method `stat(path) ==> object`. Trong những thông tin chi tiết đó, những thông tin mình cho là hữu ích hơn cả là:

- mode: 33279, // integer representing type and permissions - phân quyền
- uid: 1000, // user ID
- gid: 985, // group ID - group mà user nằm trong đó
- size: 5, // file size
- accessTime: 1566868566000, // Last access time. milliseconds
- modifyTime: 1566868566000, // last modify time. milliseconds
- isDirectory: false, // true if object is a directory
- isFile: true, // true if object is a file

Nếu bạn chưa có ngay path của file/folder ngay từ đầu, mà cần xác định đối tượng dựa vào chuyện liệt kê, thì cũng giống như lúc ta hay gõ `ls` với terminal cũng vậy, ta dùng method `list(path, pattern) ==> Array[object]`.

### fastGet(remotePath, localPath, options) ===> string

Đây là method đơn giản và dễ sử dụng, có thể download file dưới dạng nhiều tiến trình concurrency thông qua các option. Ví dụ về options:

```ts
{
  concurrency: 64, // integer. Number of concurrent reads to use
  chunkSize: 32768, // integer. Size of each read in bytes
  step: function(total_transferred, chunk, total) // callback called each time a
                                                  // chunk is transferred
}
```

32768 là 2^15.

`concurrency` chỉ hiệu quả khi bộ vi xử lý là đa nhân, nhiều luồng, cộng thêm việc file mà ta phải download là khá lớn. Giống như khi ta vận chuyển đồ cũng vậy, đồ nhỏ thì mắc cớ gì phải chia nhỏ ra, đồ lớn mới cần tháo ra thành từng `chunk` - khối, với độ lớn là `chunkSize`. Mỗi lần tháo dỡ được 1 `chunk` thì làm 1 bước tương ứng với `step` function.

Nhắc lại phần 1 thì ta đã chuẩn bị 1 file test.json với nội dung như sau:

```json
{
  "content": "this is my testing content"
}
```

Cách sử dụng cơ bản:

```ts
const localFolderPath = './down';
const remoteFilePath = '/files/test.json';

await sftp.fastGet(remoteFilePath, `${localFolderPath}/test.json`);
````

Chú ý là thư mục `down` đã được tạo từ trước, nếu không thì ta dùng method `mkdir(path, recursive) ==> string` để tạo thư mục mới. Tất nhiên, nếu chưa biết có thư mục đó hay chưa thì ta lại dùng method `exists(path)`.

Okay, kiểm tra thư mục `./down` xem nội dung có đúng như file test.json không nhé. Nếu chạy lại đoạn code trên, tức là download lại file test.json thì sẽ thấy thời gian modify của file thay đổi, tức là file đã bị replace thay vì thông báo đã tồn tại file trùng tên.

#### Xử lý lỗi

Nếu `remoteFilePath` được trỏ tới lại là 1 folder thì sẽ throw ra lỗi `Error: fastGet: Not a regular file`.

Nếu `localPath` param không phải 1 file mà là 1 folder thì sẽ có lỗi `Error: fastGet: EISDIR: illegal operation on a directory, open './down'`. Còn nếu `remotePath` trỏ tới không phải là 1 file thì sẽ báo lỗi `Error: fastGet: Not a regular file /files/`.

### fastPut(localPath, remotePath, options) ==> string

`fastPut` tương tự `fastGet`, hơi khác chút là `localPath` là điểm khởi đầu, `remotePath` là điểm đích và bên trong options có thêm thuộc tính `mode` - FileMode hay phân quyền của file.

#### Xử lý lỗi với upload thì sao

Về xử lý lỗi, `fastPut` cũng nhả lỗi khi 2 path không phải là 1 file:

- Sai localPath: "Error: fastPut: Bad path: ./down not a regular file".
- Sai remotePath: "Error: fastPut: No such file Local: ./down/test.json Remote: ".

À từ từ, giờ ta phải chú ý đến 1 vấn đề: `Error: fastPut: Permission denied Local: ./down/test.json Remote: files/test.json`. Đó là permission - ghi đè / sửa file.

Lỗi này xảy ra khi mình set remotePath trùng với 1 file trên remote mà user chúng ta đang dùng để connect thì không có quyền `write`. Để đọc permission trên SFTP server ta dùng (chú ý là ta đang dùng SFTP server tự tạo trên localhost ở phần 1 nhé):

```sh
ll /sftp/ -R
```

Hoặc là muốn màu mè, dễ đọc permission hơn thì có thể dùng [exa - replacement for ls](https://github.com/ogham/exa) được viết bằng Rust. Còn nếu muốn đọc permission dạng số thì dùng trang [chmod-calculator](https://chmod-calculator.com/).

Với ví dụ hiện tại thì file `/sftp/files/test.json` có định nghĩa quyền là `-rw-r--r--` thì cùng group sẽ không có quyền `write`, nên ta không có quyền ghi đè file này.

Một cách để up an toàn đó là upload lên 1 file mới hoàn toàn, không replace file cũ. Sau khi upload lên 1 file với cái tên khác đi thì kiểm tra lại bằng `ll /sftp/ -R` ta sẽ thấy phân quyền của file này là `-rw-rw-r--`. `-rw-rw-r--` tức là user hiện tại có quyền sửa. Ta thử chạy lại để replace file mới vừa up đó. Kết quả là Date Modified của file bị thay đổi, chứng tỏ replace thành công.

---

Photo by <a href="https://unsplash.com/@drew_beamer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Drew Beamer</a> on <a href="https://unsplash.com/s/photos/link?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
