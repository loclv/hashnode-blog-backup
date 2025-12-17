---
title: "So sánh các Vietnamese Input method - bộ gõ tiếng Việt cho MacOS"
datePublished: Wed Dec 17 2025 03:04:17 GMT+0000 (Coordinated Universal Time)
cuid: cmj9fgzn1000002ld5c37gyfa
slug: so-sanh-cac-vietnamese-input-method-bo-go-tieng-viet-cho-macos
tags: macos, vietnamese

---

Đối tượng: Người dùng Việt Nam khi sử dụng các Input method để gõ tiếng Việt.

Mục đích: So sánh các Input method để tìm ra Input method tốt nhất.

Các Input method được so sánh:

- Vietnamese input method (IM) native mặc định của MacOS sử dụng Unikey engine của bác Phạm Kim Long cho core processing.

> The Vietnamese input method (IM) in macOS is native and uses the UniKey engine for its core processing.

- OpenKey: <https://github.com/tuyenvm/OpenKey>
- PHTV: <https://github.com/PhamHungTien/PHTV>
- XKey: <https://github.com/xmannv/xkey>
- Gõ Nhanh <https://github.com/khaphanspace/gonhanh.org>

Các phiên bản mới nhất tại ngày 17/12/2025.

Không bàn tới có bug hay không vì có thể sẽ được cả thiện trong tương lai.

## Mức độ sử dụng RAM trên MacOS 15.3.2 (M1)

- Vietnamese IM native: 8MB
- OpenKey: 12.4MB
- PHTV: 62.2MB
- XKey: 44.3MB
- Gõ Nhanh: 37.1MB

## Mặc định gõ được trên VSCode/ Windsurf/ Cursor

Đây là app mà mình quan tâm vì đôi khi cần gõ tiếng Việt khi làm dự án.

Với cấu hình mặc định:

- Vietnamese IM native: Có
- OpenKey: Không
- PHTV: Không
- XKey: Không
- Gõ Nhanh: Không

## Về công nghệ

- Vietnamese IM native: Engine gõ là Unikey, UI không có
- OpenKey: Engine gõ là C++, UI là Cocoa
- PHTV: Engine gõ là C++ (tham khảo từ OpenKey), UI là SwiftUI
- XKey: Engine gõ là Swift, UI là SwiftUI
- Gõ Nhanh: Engine gõ là Rust, UI là SwiftUI

### Đánh giá

- Swift thuần: tối ưu nhất cho độ đơn giản, ổn định, bảo trì lâu dài. Đủ nhanh, đủ nhẹ cho bộ gõ tiếng Việt.
- Swift + engine C++: có thể cross platform hơn. Nhưng có thể kéo theo vấn đề FFI bridge (Foreign function interface).

FFI cho phép: Swift call C++ /C. Swift call C++ phải cần C wrapper.

```text
SwiftUI
  ↓
Swift
  ↓
C API (extern "C")
  ↓
C++ engine
```

Vấn đề có thể gặp:

- Mỗi bridge kéo theo:
  - glue code
  - header
  - wrapper
  - ABI compatibility layer

Chuyển đổi dữ liệu (string là hung thần)

IME sống bằng string.

Qua FFI:

- Swift String (UTF-16/UTF-8 hybrid)
- C/C++ char* / std::string
- Rust String (UTF-8)

Muốn qua cầu, phải:

- copy
- encode/decode
- allocate/deallocate

Bạn không chỉ trả giá CPU, mà còn:

- heap churn
- cache miss
- fragment memory

Swift thuần:

- không copy
- không encode
- không bridge

## Ngoài ra còn

- v7 Input Method: <https://github.com/ducngg/v7> - Python - Bộ gõ tiếng Việt tích hợp AI
- EVKey: <https://github.com/lamquangminh/EVKey> - C++
- Vietnamese IM for Neovim: <https://github.com/sontungexpt/vietnamese.nvim> - Lua
- YAIM: <https://github.com/manhhomienbienthuy/yaim> - C#

## Ý tưởng

Hoàn toàn có thể tạo binary chạy được trên macOS mà không dùng SwiftUI.
SwiftUI chỉ là UI framework. Nó không liên quan đến việc một binary có chạy được hay không.

Bạn thậm chí không cần UI, không cần App bundle, thậm chí không cần Swift.

Đối với cần hiệu năng thì sử dụng luôn Vietnamese input method (IM) native mặc định của MacOS.
