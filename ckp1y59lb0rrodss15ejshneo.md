## Cách tạo nhiều examples cho swagger (openapi) và config @stoplight/prism-cli trả về đúng example mong muốn  🦥

Tóm tắt:

1. Thêm nhiều examples theo hướng dẫn ở [swagger docs](https://swagger.io/docs/specification/adding-examples/).
2. [response-examples](https://meta.stoplight.io/docs/prism/docs/guides/01-mocking.md#response-examples).
3. Dùng [modheader](https://bewisse.com/modheader/) để custom header request gửi lên từ trình duyệt. Ví dụ call URL với `Prefer` header `example=dog`.
4. Nhận về đúng example mà mình đã mô tả trong `modheader`.

## 🧱 Cài đặt @stoplight/prism-cli

Use [this tool](https://meta.stoplight.io/docs/prism/README.md) for HTTP mock server simulates.

```sh
npm install -g @stoplight/prism-cli
prism mock ./media/api_docs/swagger.yaml
```

## 📓 swagger editor

Cho [vscode](https://code.visualstudio.com/) thì sử dụng [extention này](https://marketplace.visualstudio.com/items?itemName=Arjun.swagger-viewer).

## 🎶 Thêm examples cho swagger

Tạo 1 thuộc tính `examples` đồng cấp với `schema`. Điều khác biệt với chỉ 1 `example` là:

- `example` là 1 thuộc tính của `schema`.
- `examples` có 1 hoặc nhiều thuộc tính đại diện cho tên của 1 example, mỗi thuộc tính đó (tên example) có thuộc tính là `value`, trong thuộc tính `value` mới mô tả nội dung example.

Bên trong examples sẽ có các example - phân biệt bằng tên riêng của từng example:

```yaml
examples: # Multiple examples
  zero: # Distinct name
    value: 0 # Example value
    summary: A sample limit value # Optional description
  max: # Distinct name
    value: 50 # Example value
    summary: A sample limit value # Optional description
  short-list: # Distinct name
    value: 25 # Example value
    summary: A sample limit value # Optional description
```

## 🌧 Set header để controll response nào được trả về

### Dùng browser extention - [modheader](https://bewisse.com/modheader/)

Ví dụ set `Prefer` header `example=short-list`, với `short-list` là example đã được định nghĩa trong file swagger.

![modheader](https://cdn.hashnode.com/res/hashnode/image/upload/v1621820179271/DPRcKSL0c.png)

### Dùng API testing client

Ví dụ dùng vscode extention:

![Screenshot from 2021-06-02 11-28-25.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1622608339558/sYTE8ROwp.png)

Dùng Open source API development: [hoppscotch.io](https://hoppscotch.io/).

---

Photo by <a href="https://unsplash.com/@katetrysh?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Kate Trysh</a> on <a href="https://unsplash.com/s/photos/mock-api?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
