## Cài deno trên Ubuntu 21.04 với fish shell 🐟

Khi tiến hành cài đặt [deno](https://deno.land/) cho Ubuntu + [fish shell](https://fishshell.com/), dù đã làm theo hướng dẫn, đó là tải `install.sh` về chạy, tuy nhiên thì khi mở 1 cửa sổ terminal mới mình vẫn chưa dùng được `deno`. Có thể nguyên nhân nằm ở `install.sh` chưa hỗ trợ tốt cho Ubuntu + `fish shell` chăng?

![tea-time](https://media.giphy.com/media/gLcUFh2TrdySKUnTHD/giphy.gif)

## Kiểm tra môi trường

```sh
lsb_release -a
# Description:    Ubuntu 21.04

fish --version
# fish, version 3.1.2
```

## Cài đặt và set PATH

Theo hướng dẫn:

- cài đặt của deno tại [đây](https://deno.land/#installation)
- cách set biến môi trường cho fish shell tại [đây](https://fishshell.com/docs/current/tutorial.html#path)

```sh
curl -fsSL https://deno.land/x/install/install.sh | sh

# edit with vscode / nano / vim
code ~/.config/fish/config.fish
```

Sau đó sửa file đang mở với nội dung:

```fish
set -gx DENO_INSTALL "/home/$USER/.deno"
set -gx PATH "$DENO_INSTALL/bin" $PATH
```

`config.fish` là file tương tự như `.profile` của các shell khác. Ta nối thêm danh sách các lệnh mà shell có thể gọi bằng cách thêm đường dẫn hay `PATH`. Đường dẫn này trỏ tới nơi mà ta vừa cài `deno`.

`set -gx` là cách ta set 1 biến có giá trị ở mọi nơi mà `fish shell` chạy.

OK, save file và mở cửa sổ terminal mới và thử chạy:

```sh
deno --version
```

Ví dụ output là:

- deno 1.14.0 (release, x86_64-unknown-linux-gnu)
- v8 9.4.146.15
- typescript 4.4.2

Vậy là ta đã cài thành công và có thể sử dụng `deno` command thoải mái.

```sh
deno
```

```ts
const d: string = 'deno'
console.log('test: ', d)
```

---

Photo by <a href="https://unsplash.com/@peterf?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Peter F</a> on <a href="https://unsplash.com/s/photos/sea?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
