## Node.js - TypeScript - dùng ssh2-sftp-client với SFTP server tự tạo trên localhost - phần 1 - kết nối 📂 🍻

Source-code được viết theo phong các `async` - `await`.

## Cài đặt `ssh2-sftp-client` vào project Node.js - TypeScript

Mình đã dựng sẵn 1 base project dành cho Node.js - TypeScript tại [đây](https://github.com/loclv/typescript-nodejs-template).

Cài đặt [ssh2-sftp-client](https://github.com/theophilusx/ssh2-sftp-client):

```sh
pnpm add ssh2-sftp-client
pnpm add -D @types/ssh2-sftp-client
```

Chú ý là bạn có thể thay pnpm - package manager bằng yarn hoặc npm.

Giờ ta sẽ sử dụng `SFTP Servers` được dựng trên ngay chính localhost để test.

## Tạo SFTP server trên localhost

Tham khảo bài viết [setup-a-local-sftp-server-for-development](http://www.niladicpodcast.com/blog/2018/1/setup-a-local-sftp-server-for-development/) trên môi trường Ubuntu:

```sh
sudo apt install openssh-server
sudo groupadd sftponly
sudo mkdir /sftp/
sudo chown root:sftponly /sftp/
sudo chmod 2755 /sftp/
# The 2 is for g+s
```

Thêm đoạn config sau vào cuối file `/etc/ssh/sshd_config`:

```sh
sudo nano /etc/ssh/sshd_config
```

config:

```config
Match Group sftponly
    ChrootDirectory /sftp/
    ForceCommand internal-sftp
    AllowTcpForwarding no
```

```sh
sudo service ssh restart
```

Tự tạo 1 folder `files` để test:

```sh
sudo mkdir /sftp/files/
# Allow sftponly users to upload files
sudo chmod 2775 /sftp/files/
```

Tạo ra 1 file JSON để test và copy nó lên thư mục `files` vừa tạo. Tạo `test.json` với nội dung:

```json
{
  "content": "this is my testing content"
}
```

```sh
sudo cp test.json /sftp/files/
```

Tạo user để SFTP:

```sh
sudo useradd -M -G sftponly newUser
sudo passwd newUser
# set password
sudo -u newUser sftp localhost
```

Thêm user hiện tại vào group đã tạo bên - `sftponly` trên:

```sh
sudo usermod -a -G sftponly $USER
```

## Kết nối

Tại `src/utils/index.ts` viết hàm common:

```sh
import Client from 'ssh2-sftp-client';

export const sftpConnect = async (
  host: string,
  port: number,
  username: string,
  password: string
): Promise<Client> => {
  const sftp = new Client('download-test-json-client');

  await sftp.connect({
    host,
    port,
    username,
    password,
  });

  return sftp;
};
```

## Kiểm tra sự tồn tại của file/folder

Tại `src/index.ts` viết hàm `main` sử dụng `sftpConnect`:

```ts
import { sftpConnect } from '@utils';

const main = async () => {
  try {
    const sftp = await sftpConnect('localhost', 22, 'newUser', 'newUser');

    let path: string;
    let type: string | boolean;

    path = '/files';
    type = await sftp.exists(path);
    console.log(`🌄 ~ ${path} type: `, type);

    path = '/files/test.json';
    type = await sftp.exists(path);
    console.log(`🍻 ~ ${path} type: `, type);

    path = '/files/non-exist-test.json';
    type = await sftp.exists(path);
    console.log(`🌑 ~ ${path} type: `, type);
  } catch (err: any) {
    console.log(err, 'catch error');
  }
};

main();
```

Trong đó `await sftpConnect('localhost', 22, 'newUser', 'newUser')` là thông tin ta vừa tạo SFTP server bên trên.

`sftp.exists` sẽ trả về `Promise<false | FileInfoType>`.

Theo thông tin từ package `@types/ssh2-sftp-client` thì:

```ts
type FileInfoType = 'd' | '-' | 'l';
```

Ta hãy xem output khi chạy đoạn code trên sẽ là gì.

```sh
pnpm start
```

Output:

```text
🌄 ~ /files type:  d
🍻 ~ /files/test.json type:  -
🌑 ~ /files/non-exist-test.json type:  false
```

Như vậy, ta đã xác nhận là đã kết nối thành công tới SFTP server.

- `-` là file
- `d` là directory
- `false` là không tồn tại

[Phần 2](https://loclv.hashnode.dev/nodejs-typescript-ssh2-sftp-client-package-phan-2-fast-download-upload) mình sẽ thử việc download và upload file.

---

Photo by <a href="https://unsplash.com/@drew_beamer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Drew Beamer</a> on <a href="https://unsplash.com/s/photos/link?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
