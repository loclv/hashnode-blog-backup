# Alpine based Docker 🐋 image - dùng `/bin/sh` thay vì phải cài `bash`

## 🌱 Câu chuyện vào debug bên trong Docker image

Khi mà mới làm quen với `Docker` image, hay đơn giản là vào bên trong nó xem lỗi do đâu,
chắc hẳn bạn cũng sẽ nghĩ ngay trong đầu là phải bật `bash` lên và truy cập vào bên trong image.

Khi build image của [Alpine](https://www.alpinelinux.org/),
chẳng hạn ta set image được kế thừa từ `FROM node:16.8.0-alpine` (version mới nhất của `Node.js` tại thời điểm viết bài).
Tuy nhiên image được kế thừa này thường default sẵn có `/bin/sh`.

Đối với nhu cầu của developer như `cd`, `ls` hay chạy app bên trong image thì `/bin/sh` hoàn toàn có thể đáp ứng được.
Như vậy chúng ta không cần cài `bash` vào image nữa cho mệt.

Việc không phải cài `bash` tuy chỉ tiết kiệm 4MB đối với image chạy Alpine 3.8 nhưng đối với 100 image thì câu chuyện sẽ khác.
Ngoài ra ta còn tăng tốc độ tạo lập 1 `Docker` image mới.

![hair](https://media.giphy.com/media/dXKiD8XysOuhFAJB1f/giphy.gif)

## Cách dùng `/bin/sh`

Trong `Dockerfile` ta thêm `RUN /bin/sh` để chạy `sh`.

Sau đó có thể truy cập vào image như sau:

```sh
# run Dockerfile.dev chẳng hạn
docker build -t node-dev-image -f Dockerfile.dev .

# run sh
docker run -it --rm --name dev -v $(pwd):/code node-dev-image sh
# or if you using fish-shell
docker run -it --rm --name dev -v (pwd):/code node-dev-image sh

# let play with `sh`
ls

# exit sh if needed
exit
```

## Tham khảo

- [câu hỏi làm sao dùng bash trong Alpine based Docker image trên stackoverflow](https://stackoverflow.com/questions/40944479/docker-how-to-use-bash-with-an-alpine-based-docker-image)

---

Photo by <a href="https://unsplash.com/@gerandeklerk?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Geran de Klerk</a> on <a href="https://unsplash.com/collections/2705330/virtues?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
