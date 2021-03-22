## 🐧 Tools cho Ubuntu sau khi mới cài

Bài viết dành cho những người mới với `Ubuntu` (bản dành cho máy tính cá nhân), thời điểm mới cài Ubuntu xong.

Điều đầu tiên cần làm là update lên version mới nhất của Ubuntu. Thời điểm viết bài mình đã thử `ubuntu 20.04` và không gặp vấn đề gì cả.

## 📓 Editor for coding

`vscode` || `vscode-insiders`

`Atom`

## 🌏 Terminal

Default terminal của Ubuntu nhanh, đơn giản. Như vậy là đủ.

Nhưng đối với những bạn thích custom hay vọc vạch thì hãy thử dùng các terminal client bên dưới xem nhé 🌂

[terminal hyper](https://hyper.is/)

[terminus](https://eugeny.github.io/terminus/)

## 📦 deb installer

`gdebi-gtk`

Mô tả `gdebi-gtk` nguyên văn dưới đây.

```txt
"gdebi  lets  you install local deb packages resolving and installing its dependencies.
apt does the same,
but only for remote (http, ftp) located packages.
```

Đại khái `gdebi` dùng để cài `deb packages` - tương ứng với `.exe` bên `window` hay `.dmg` bên `MacOS`. Nó cũng giống với công cụ `apt` được tích hợp sẵn trong `Ubuntu` chỉ trừ là có giao diện UI và cài `deb packages` đã được tải về máy. Không thì bạn sẽ phải dùng `dpkg` 1 cách manual và phức tạp. Thông tin này tham khảo tại [đây](https://itsfoss.com/install-deb-files-ubuntu/).

Cũng là để tránh `dependency error` mà `default Software Center` có thể gây ra.

Cách dùng `gdebi-gtk` tại [đây](https://itsfoss.com/gdebi-default-ubuntu-software-center/)

## 🌈 exa

[exa](https://the.exa.website/) A modern replacement for `ls`.

## 🏢 Office

<https://www.wps.com/>

`wps office`, đẹp, siêu nhẹ, siêu nhanh, đa nền tảng

Nếu mở những file có dung lượng lớn (>20MB) nhất là định dạng `xlsx` thì nó nhanh hơn [libreOffice](https://www.libreoffice.org/) hơn hàng trăm lần (cảm nhận của mình).

Sở hữu tính năng tìm kiếm tên sheet trong trường hợp 1 `workbook` có tới hàng chục `sheet`.

`wps` cũng có bản web như `Microsoft Office` nhưng hạn chế dùng do thường có yêu cầu bảo mật không thể upload tài liệu lung tung lên cloud được.

Nên tải trực tiếp ở [đây](https://linux.wps.com/) và cài file đã được tải về bằng `gdebi` bên trên nhé, thay vì dùng dùng [snap store](https://snapcraft.io/store). Vì mình đã dùng thử bản ở `snap` không được udpate và nhiều bug.

## 📂 launcher

<https://ulauncher.io/>

Với tổ hợp phím `ctrl` + `space` mở mọi thứ mọi nơi.

## 🐚 SSH client

[termius](https://termius.com/) - tên khá dễ nhầm với `terminus` :D

Đa nền tảng Desktop kể cả iOS và android nên ngồi ị 🍰 vẫn có thể check status của server nhé.

Download tại [đây](https://termius.com/linux).

## 🚀 API testing tools

Lựa chọn nền web thay thế cho `postman`: [hoppscotch](https://hoppscotch.io/).

`hoppscotch` đẹp đơn giản và hỗ trợ `graphQL`.

## ✏ Bộ gõ tiếng Việt

Tại thời điểm viết bài, thì theo trai nghiệm cảu mình thì bộ gõ [teni-ime/ibus-teni](https://github.com/teni-ime/ibus-teni) là có trải nghiệm tốt nhất với các app. Mặc dù nó đã bị đóng băng trên github (không được update thêm nữa).

Hãy cần thận tắt bộ gõ tiếng Việt trước khi gõ password trên `terminal` nhé :D Do nó sẽ hiện phần gạch chân (tạm) trên màn hình đó.

## 👆 Update

Thường xuyên chạy update, nhiều khi thấy cũng chẳng khác gì nhưng mà nghiện mất rồi :v

```sh
sudo apt-get update && sudo apt-get upgrade && sudo apt dist-upgrade
```

## Thêm Repositories cho software & update

Thêm repo thêm nơi để cài đặt các package.

Nhưng tại sao khi đã có defaul repo rồi?

Vì `Canonical Partners repository` hay các repo khác chứa source đóng chứa 1 số app (triết lý linux là open-source).

### Cách thêm

Ấn `super key (Windows key)`, search `software & update`, vào `software tab`, enables `Canonical Partners`, `Community-maintained`, `Proprietary drivers`, ... trừ `Source Code`.

Vào `Other software tab`, enables các Repo trừ phần `Source Code` trừ khi bạn có ý định kéo cả code của package về :D

## Tham khảo

- <https://www.ubuntupit.com/best-things-to-do-after-installing-ubuntu/>
- <https://www.lifewire.com/updated-software-for-ubuntu-with-ppas-2202103>

---

Còn nhiều thứ có thể nghịch với Ubuntu nữa, cơ mà sức mình có hạn :v

Photo at [pngegg](https://www.pngegg.com/en/png-zfazu)