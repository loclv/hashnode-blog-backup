## Chuyển YAML sang JSON và ngược lại với vscode extentions - YAML ❤️ JSON và các chú ý

## 🤨 Sao không dùng online web-base tools?

- Khi upload source code lên môi trường online web-base thì không giám chắc rằng dữ liệu đó có bị upload tới đâu không.
- vscode là editor, nên dễ dàng format JSON/YAML code ngay và luôn.

## 👊 Sử dụng [YAML ❤️ JSON](https://marketplace.visualstudio.com/items?itemName=hilleer.yaml-plus-json) vscode extentions

Ví dụ với `yaml` source ([nguồn tại wikipedia](https://en.wikipedia.org/wiki/YAML)):

```yaml
--- # eaxmple
- step1: &id001                   # defines anchor label &id001
    name: 'first step'

- step2: &id002
    name: 'second step'

- step3: *id001                   # refers to the first step (with anchor &id001)
- step4: *id002                   # refers to the second step
- step5: *id002
```

0. Save ví dụ trên vào 1 file có đuôi `yaml`, ví dụ: `test.yaml`.
1. Sử dụng `ctrl` (hoặc `command` với macOS) + `shift` + `p`.
2. Gõ `>convert to JSON` (ngược lại là `>convert to YAML`).
3. Ta thấy file và định dạng đuôi file đã chuyển sang dạng mong muốn.

Ngoài ra, ở bước 2 thay vì gõ command thì ta chuyển đuôi file sang YAML/JSON, extention cũng tự động convert cho chúng ta. Ví dụ `test.yaml` -> `test.json`.

Output ví dụ trên:

```json
[
  {
    "step1": {
      "name": "first step"
    }
  },
  {
    "step2": {
      "name": "second step"
    }
  },
  {
    "step3": {
      "name": "first step"
    }
  },
  {
    "step4": {
      "name": "second step"
    }
  },
  {
    "step5": {
      "name": "second step"
    }
  }
]
```

## 😳 Chú ý

Như ta thấy ở ví dụ trên thì `anchors` trong `yaml` hay con trỏ địa chỉ sẽ không được giữ lại khi convert `yaml` -> `json` -> `yaml`.

`yaml` -> `json` -> `yaml` output:

```yaml
- step1:
    name: first step
- step2:
    name: second step
- step3:
    name: first step
- step4:
    name: second step
- step5:
    name: second step
```


Điều này cũng gặp phải với các online web-base tools, ví dụ [json2yaml](https://www.json2yaml.com/).

Tương tự các comments bên phía `yaml` cũng bị xóa khi chuyển sang `json` vì `json` không support comments.

---

Photo by <a href="https://unsplash.com/@jimmydean?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Jimmy Dean</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
