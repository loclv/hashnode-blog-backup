## Golang 🎽 - Dùng Go Version manager — gobrew

## Tại sao ta nên dùng Version manager?

Cũng như các ngôn ngữ khác như Node.js, việc chuyển đổi version giữa các dự án, test các môi trường có version khác nhau luôn mất nhiều thời gian upgrade ngôn ngữ lên version mới, hay thậm chí khi muốn downgrade thì chỉ còn cách xóa đi cài lại bản cũ.

Việc của Version manager là giúp ta chỉ cần gõ switch version là xong, nhanh gọn!

## Tại sao lại là gobrew?

Theo như bài viết [medium - Go Version manager — gobrew](https://medium.com/web-developer/go-version-manager-gobrew-c8750157dfe6), thì so với 2 version manager khác là [gvm](https://github.com/moovweb/gvm) và [goenv](https://github.com/syndbg/goenv) thì [gobrew](https://github.com/kevincobain2000/gobrew) được viết bằng chính golang. Điều này giúp cho chính những Go-developer sẽ cảm thấy thoải mái khi đóng góp và đọc hiểu `gobrew`. Bản thân `golang` cũng mạnh mẽ hơn `shell script` thứ được sử dụng để viết 2 Version manager kia rôi.

> Lấy độc trị độc - lấy golang để cài golang :v

## Cách sử dụng gobrew

```sh
curl -sLk https://git.io/gobrew | sh -
```

Thêm `GOPATH` vào `.bashrc` hoặc `.zshrc`

```sh
export PATH="$HOME/.gobrew/current/bin:$HOME/.gobrew/bin:$PATH"
```

Nếu bạn dùng [fishshell](https://fishshell.com/) thì thêm như sau:

```sh
echo $PATH
# chưa có GOPATH

set PATH $PATH $HOME/.gobrew/current/bin:$HOME/.gobrew/bin

echo $PATH
# đã có GOPATH: .gobrew/bin
```

### Cài version

Để cài đặt version ta cần biết version mới nhất là gì. Ta có thể vào trang chủ golang cũng được hoặc liệt kê bằng gobrew:

```sh
gobrew ls-remote
# tại thời điểm viết bài ver mới nhất là 1.17.3

gobrew install 1.17.3
go version
# go version go1.17.3 linux/amd64

gobrew ls
# 1.17.3*
```

Okey, chạy ngay đi!

---

Photo by <a href="https://unsplash.com/@matreding?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Mathias P.R. Reding</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
