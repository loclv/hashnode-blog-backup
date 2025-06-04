---
title: "Kiến trúc cơ bản của một ứng dụng chat với mã hóa đầu-cuối 🔐 (end-to-end encryption), đảm bảo chỉ người dùng mới có thể đọc tin nhắn"
datePublished: Wed Jun 04 2025 06:09:32 GMT+0000 (Coordinated Universal Time)
cuid: cmbhjs9sp000209jv4nkfbfue
slug: kien-truc-co-ban-cua-mot-ung-dung-chat-voi-ma-hoa-dau-cuoi-end-to-end-encryption-dam-bao-chi-nguoi-dung-moi-co-the-doc-tin-nhan
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Jjue0ESkXAU/upload/6645f13d79801c91debffbde7efc0ebb.jpeg
tags: end-to-end-encryption

---

Dưới đây là một sơ đồ Mermaid mô tả kiến trúc của một ứng dụng chat với mã hóa đầu-cuối (end-to-end encryption), đảm bảo chỉ người dùng mới có thể đọc tin nhắn:

```mermaid
sequenceDiagram
    participant UserA
    participant Server
    participant UserB

    Note over UserA, UserB: Khởi tạo khóa
    UserA->>UserA: Tạo khóa công khai & bí mật (A_pub, A_priv)
    UserB->>UserB: Tạo khóa công khai & bí mật (B_pub, B_priv)

    Note over UserA, Server: Chia sẻ khóa công khai
    UserA->>Server: Gửi A_pub
    UserB->>Server: Gửi B_pub

    Note over Server: Server chỉ lưu A_pub & B_pub, không biết khóa bí mật

    Note over UserA, UserB: Trao đổi tin nhắn
    UserA->>Server: Gửi Encrypt("Hello", B_pub)
    Server->>UserB: Relay Encrypt("Hello", B_pub)
    UserB->>UserB: Decrypt(message, B_priv)

    Note over UserB: Chỉ UserB có thể giải mã tin nhắn bằng B_priv
```

Code biểu đồ:

````markdown
```mermaid
sequenceDiagram
    participant UserA
    participant Server
    participant UserB

    Note over UserA, UserB: Khởi tạo khóa
    UserA->>UserA: Tạo khóa công khai & bí mật (A_pub, A_priv)
    UserB->>UserB: Tạo khóa công khai & bí mật (B_pub, B_priv)

    Note over UserA, Server: Chia sẻ khóa công khai
    UserA->>Server: Gửi A_pub
    UserB->>Server: Gửi B_pub

    Note over Server: Server chỉ lưu A_pub & B_pub, không biết khóa bí mật

    Note over UserA, UserB: Trao đổi tin nhắn
    UserA->>Server: Gửi Encrypt("Hello", B_pub)
    Server->>UserB: Relay Encrypt("Hello", B_pub)
    UserB->>UserB: Decrypt(message, B_priv)

    Note over UserB: Chỉ UserB có thể giải mã tin nhắn bằng B_priv
```
````

Sơ đồ này mô tả:

* Mỗi người dùng tạo cặp khóa riêng (public/private).
* Chỉ chia sẻ khóa công khai qua server.
* Tin nhắn được mã hóa bằng khóa công khai người nhận, chỉ có thể giải mã bằng khóa bí mật người nhận.
* Server chỉ trung chuyển dữ liệu đã mã hóa, không thể giải mã.

