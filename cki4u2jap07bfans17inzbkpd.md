## Dùng tools để check coding convention php

## PHPCS

Phổ biến nhất là thư viện/plugin mà có thể dùng với text editer: `phpcs`.

Tên đầy đủ là `PHP_CodeSniffer`.

### Cách cài đặt

Tham khảo tại README của [repo này](https://github.com/squizlabs/PHP_CodeSniffer).

### Chọn chuẩn coding-style

Kiểm tra các chuẩn đã được cài đặt:

```sh
phpcs -i
# The installed coding standards are MySource, PEAR, PSR1, PSR12, PSR2, Squiz and Zend
```

Sau khi cài đặt thì đặt lại chuẩn convention theo mong muốn.

Dưới đây thì mình dùng chuẩn `PSR2`.

```sh
phpcs --config-set default_standard PSR2
```

Chuẩn này cảm giác khá thoải mái nhất là không khắt khe về chuyện phải comment mỗi file/function không.

Mỗi lần không cần viết comment mà cứ gặp mess: `Missing doc comment for file/function`.

[Good code can self document what it does, but it cannot document why it does it. This is where comments come in.](https://www.reddit.com/r/programming/comments/ayv9jt/good_code_documents_itself_and_other_hilarious/)

### Rules theo Framework

#### `Phalcon`

framework `Phalcon` dùng chuẩn `PSR12` thì là:

```sh
phpcs --config-set default_standard PSR12
```

#### `Laravel`

Theo như docs của laravel:

<https://laravel.com/docs/8.x/contributions#coding-style>

Thì dùng chuẩn sau:

- [PSR-2-coding-style-guide](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md)
- [PSR-4-autoloader](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md)

Tuy nhiên theo như trang chuẩn `PSR-2` bên trên đã nói, rằng chuẩn này đã không còn được hô trợ nữa từ 2019 mà chuyển sang chuẩn [PSR-12](https://www.php-fig.org/psr/psr-12/).

### Tự đặt chuẩn convention của mình

<https://ncona.com/2012/12/creating-your-own-phpcs-standard/>

### Tự động fix lỗi cho mình 1 hoặc nhiều file

<https://github.com/squizlabs/PHP_CodeSniffer/wiki/Fixing-Errors-Automatically>

Ta dùng `phpcbf` vốn là viết tắt của `PHP Code Beautifier and Fixer`.

Trước tiên là xem nó định fix code của mình thành như thế nào đã:

```sh
phpcs --report=diff /path/to/code
```

Giờ sử dụng `phpcbf` sửa các file trong thư mục:

```sh
phpcbf /path/to/code
```

## intelephense

intelephense - thư viện/ plugin text editer hỗ trợ việc coding.

Mình hay dùng để kiểm tra xem trong src code thư viện nào khai báo mà lại không dùng.

Thư viện này nếu trả phí sẽ có thêm vài chức năng khác nữa.

## Code Spell Checker

Check xem đã đúng ngữ pháp, từ vựng tiếng Anh/code chưa.

Link cho vscode:

<https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker>

## Các editor có extentions hỗ trợ

- Atom
- vscode