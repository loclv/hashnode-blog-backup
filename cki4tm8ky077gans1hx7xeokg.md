## PHP - Một số thứ lặt vặt cho người mới

## Test các lệnh hay logic cơ bản từ terminal

```sh
php -a
```

Sau đó `php shell` sẽ hiện ra cho bạn thoải mái test.

Chạy 1 file để test:

```sh
php -f my_script.php
```

Xem thêm:

<https://www.php.net/manual/en/features.commandline.usage.php>

## Kiểm tra timezone

```php
echo 'date_default_timezone_set: ' . date_default_timezone_get();
```

## PHP Extension

Xem những PHP Extension nào đang được cài đặt:

```sh
php -m
```

Khi bạn muốn kiểm tra xem môi trường cài đặt framework `laravel` đã OK chưa chẳng hạn, trong framework laravel cần cài `extentions` như trong link dưới đây:

<https://laravel.com/docs/8.x#server-requirements>

## PHP xdebug

### Trên môi trường Linux

Thư viện `xdebug.so` sẽ thay đổi đường dẫn khi thay đổi PHP version.

Ví dụ với php 7.2 thì:

`/usr/local/lib/php/extensions/no-debug-non-zts-20170718/xdebug.so`

Còn php 7.3 là:

`/usr/local/lib/php/extensions/no-debug-non-zts-20180731/xdebug.so`

Thế nên, ta cần chú ý thay đổi đường dẫn trong `php.ini` khi thay đổi php version trpng `Docker` chẳng hạn.
