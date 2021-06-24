## Mock dynamic data API với OpenAPI/Swagger và @stoplight/prism-cli ✨

## Mong muốn

Giá trị mock API trả về mỗi lần randomly và thay đổi mỗi lần khi call lại API.

## Điều kiện

- Cài [Prism](https://meta.stoplight.io/docs/prism/README.md) để mock API

```sh
npm install -g @stoplight/prism-cli

# OR

yarn global add @stoplight/prism-cli
```

- chạy mock API

```sh
prism mock ./swagger.yaml
```

Chú ý là thiết kế API của bạn phải viết theo chuẩn `openapi`.  Ví dụ về 1 file openapi (hay swagger) có tại [đây](https://editor.swagger.io/).

## Yêu cầu API trả về dynamic data

Search Google với từ khóa: `extension header set chrome`.

Bạn sẽ thấy [Chrome extention ModHeader](https://chrome.google.com/webstore/detail/modheader/idgpnmonknjnojddfkpgkljpfnnfcklj/related?hl=en).


![ext-name.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1618477815679/UKiIdGUFn.png)

Sau khi cài extention trên, click vào icon của extention đó trên thanh điều khiển của Chrome.


![ext-bar.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1618477835067/_hsVS6tj-.png)

Set header với key `Prefer` và value `dynamic=true`.


![ext-header.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1618477865694/aV3PKC0HL.png)

Cuối cùng vào web của bạn để thấy API trả về dynamic và randomly mỗi lần reload lại web (call lại API).

Bạn có thể mở tab netwwork của Chrome để xem giá trị API trả về.

## Tài liệu

Từ `prism`: [mocking dynamic-response-generation](https://meta.stoplight.io/docs/prism/docs/guides/01-mocking.md#dynamic-response-generation)
