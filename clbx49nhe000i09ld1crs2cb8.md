# Tạo nhanh gitignore với gitignore.io

### Vấn đề

Mỗi khi khởi tạo 1 project với git mà chưa có file `.gitignore` thì trước đây cách mình hay làm là:

*   search Google với từ khóa "github gitignore nodejs".
    
*   Copy code từ [https://github.com/github/gitignore/blob/main/Node.gitignore](https://github.com/github/gitignore/blob/main/Node.gitignore).
    

Việc này gần như là bắt buộc trừ khi 1 số framework đã support sẵn việc tạo `.gitignore` khi chạy CLI khởi tạo dự án.

Vấn đề là template này sẽ có những thứ thiếu, ví dụ như setting cho VS Code. Để ý rằng file bên trên đang không có phần ignore của VS Code:

```markdown
### VisualStudioCode ###
.vscode/*
!.vscode/settings.json
!.vscode/tasks.json
!.vscode/launch.json
!.vscode/extensions.json
!.vscode/*.code-snippets
```

[gitignore.io](http://gitignore.io) giúp ta kết hợp nhiều điều kiện môi trường để tạo 1 file ignore hợp nhất.

### Giới thiệu

Từ [Docs](https://docs.gitignore.io/) của [gitignore.io](http://gitignore.io), ta có thể xem qua các cách dùng của công cụ tạo nhanh file `.gitignore`. Có 3 cách sử dụng thông thường:

*   truy cập [gitignore.io](http://gitignore.io), nhập từ khóa về môi trường.
    
*   dùng kết hợp editor thông qua [editor-extensions](https://docs.gitignore.io/install/editor-extensions).
    
*   dùng thông qua app chạy dưới local với [client-applications](https://docs.gitignore.io/install/client-applications) hoặc [local-server](https://docs.gitignore.io/install/local-server).
    

Khi truy cập [gitignore.io](http://gitignore.io), nó sẽ dẫn ta tới [https://www.toptal.com/developers/gitignore/](https://www.toptal.com/developers/gitignore/).

### Create ví dụ

Dự án với Node.js và editor là VS Code thì ta nhập từ khóa:

*   Node
    
*   VisualStudioCode
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671610745515/9YZSQ0o7N.png align="center")

Ngoài ra thì cũng có thể định nghĩa OS:

*   Linux
    
*   MacOS
    
*   Windows
    

Tuy nhiên, thực tế sử dụng mình thấy không cần thiết.