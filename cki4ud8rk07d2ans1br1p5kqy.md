## 🐧 Tools cho Ubuntu sau khi mới cài

Bài viết dành cho những người mới với `Ubuntu` (bản dành cho máy tính cá nhân), thời điểm mới cài Ubuntu xong.

Thời điểm viết bài mình đã thử `ubuntu 21.04` và không gặp vấn đề gì cả.
`ubuntu 21.04` có thư viện đồ họa được nâng cấp và tối ưu khiến tốc độ nhanh hơn, điển hình là khi scroll trong danh sách các App.

## Upgrade lên Ubuntu bản mới nhất

```sh
sudo do-release-upgrade
```

Sau khi download lượng lớn dữ liệu, cài đặt và restart, việc của ta là loại bỏ những thư viện / app phiên bản cũ:

```sh
sudo apt --purge autoremove
```

Trong quá trình upgrade Ubuntu thì để an toàn Ubuntu tự động disable các repo của bên thứ 3.
Các repo này vốn là nơi chứa bản update của những phần mềm bên thứ 3 (không phải phần mềm của Ubuntu).
Enable lại các repo này, giúp việc update thông qua command `sudo apt update` trở lại như cũ.

Để enable lại thì ta:

1. vào danh sách các App
2. search `update`
3. chọn `Software & Updates`
4. vào tab `Other Software`
5. Enable lại các repo có ghi chú `disabled on upgrade to ${ubuntu-version-name}`

![update-repo.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629534955375/sBtTL8u2ay.png)

Cũng từ phiên bản này, nếu máy ta dùng là Laptop thì có thêm lựa chọn mức độ nguồn điện - power dành cho hiệu năng hoặc tiết kiệm điện. Mình chọn tối ưu cho hiệu năng:

![ubuntu-power.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629532529207/2ywbxXvVVC.png)

## 📦 deb installer - `gdebi-gtk`

Mô tả `gdebi-gtk` nguyên văn dưới đây.

>gdebi  lets  you install local deb packages resolving and installing its dependencies.
apt does the same, but only for remote (http, ftp) located packages.

Đại khái `gdebi` dùng để cài `deb packages` - tương ứng với `.exe` bên `window` hay `.dmg` bên `MacOS`. Nó cũng giống với công cụ `apt` được tích hợp sẵn trong `Ubuntu` chỉ trừ là có giao diện UI và cài `deb packages` đã được tải về máy. Không thì bạn sẽ phải dùng `dpkg` 1 cách manual và phức tạp. Thông tin này tham khảo tại [đây](https://itsfoss.com/install-deb-files-ubuntu/).

Cũng là để tránh `dependency error` mà `default Software Center` có thể gây ra.

Cách dùng `gdebi-gtk` tại [đây](https://itsfoss.com/gdebi-default-ubuntu-software-center/)

### Cài Chrome thông qua file đuôi `.deb`

Do `snap store` (sẽ giới thiệu dưới đây) không có `chrome` mà chỉ có `chromium`, nên ta lên [trang chủ Chrome](https://www.google.com/intl/en/chrome/) rồi tải file đuôi `.deb` về để cài với `gdebi-gtk`.

Trong quá trình cài đặt thì `official Google repository` sẽ được add vào danh sách repo mỗi khi update Ubuntu. Để xác nhận:

```sh
cat /etc/apt/sources.list.d/google-chrome.list
```

Output mong đợi sẽ là dòng `deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main` không bị comment lại (không có `#` đằng trước). Nếu không, ta xóa ký tự comment - `#` đó đi:

```sh
sudo nano /etc/apt/sources.list.d/google-chrome.list
```

`Ctrl` + `X` để save và chạy lại update:

```sh
sudo apt update
```

Output của `update` command sẽ thông báo đã lấy data từ repo URL ví dụ:

```txt
Get:1 http://dl.google.com/linux/chrome/deb stable InRelease [1.811 B]
Get:2 http://dl.google.com/linux/chrome/deb stable/main amd64 Packages [1.100 B] 
```

## 🎒 Dùng [snap store](https://snapcraft.io/store) thay thế cho `Ubuntu Software` - Ubuntu store

Đi chợ Apps bằng cách lên [snap store](https://snapcraft.io/store) - Linux app store. Search tên app. Ấn nút `install`, thấy hiển thị ra command. Copy command đó và chạy trên terminal.

```bash
sudo snap install <app-name>
# list all apps
snap list
```

## 📓 Editor for coding

[vscode](https://code.visualstudio.com/):

Update 04/01/2021: theo issue [này](https://github.com/BambooEngine/ibus-bamboo/issues/49) thì các tool gõ tiếng Việt sẽ không hoạt động với vscode nếu cài bằng snap như dưới đây. Thế nên, ta down file .deb tại [trang chủ](https://code.visualstudio.com/download) rồi cài bằng deb installer - `gdebi-gtk` thì sẽ gõ được tiếng Việt. Ngược lại nếu bạn không muốn gõ tiếng Việt khi đang bật chế độ gõ tiếng Việt thì lại dùng snap. 😅

```sh
sudo snap install code
```

or [vscode-insiders](https://code.visualstudio.com/insiders/) - phiên bản dùng thử trước của `vscode`:

```sh
sudo snap install code-insiders
```

or [VSCodium](https://vscodium.com/) - phiên bản nguồn mở không dính dáng gì đến Microsoft:

```sh
sudo snap install codium
```

Mình dùng mỗi phiên bản đó của `vscode` để code mỗi 1 Framework. Ví dụ `vscode-insiders` để code Vue, `vscode` dùng để code Angular. Đỡ phải switch profile tương ứng từng extention dành cho từng framework.

[Atom](https://atom.io/):

```sh
sudo snap install atom
```

## 🌏 Terminal

### Command-line interface

Default terminal của Ubuntu nhanh, đơn giản. Như vậy là đủ.

Nhưng đối với những bạn thích custom hay vọc vạch thì hãy thử dùng các terminal client bên dưới xem nhé: 🌂

- [hyper](https://hyper.is/): [đây](https://gist.github.com/loclv/67477636e417e974a07f930d72495eaa) là settings dành cho `hype` của mình.

```json
plugins: [
    'hyper-font-ligatures',
    'hypercwd',
    'hyper-active-tab'
  ],
```

Plugin `hypercwd` mở tab mới giữ nguyên đường dẫn `path`, thay vì thư mục `HOME`.
Plugin `hyper-active-tab` để đánh dấu tab đang active ở vị trí nào.

- [tabby](https://tabby.sh/) - Tabby is an infinitely customizable cross-platform terminal app for local shells, serial, SSH and Telnet connections.

Ảnh UI của tabby:

![Screenshot from 2022-03-15 16-41-32.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647357703712/OSMZIfgpxx.png)

### Command-line shell

[fish shell](https://fishshell.com/) + [Oh my fish](https://github.com/oh-my-fish/oh-my-fish) - quản lý packages dành cho `fish shell`.

Đây là các alias được config thông qua `fish shell`:

```config
alias g='git'
alias gs='git status'
alias ga='git add .'
alias gd='git diff'
alias gp='git push'

alias cf 'code ~/.config/fish/config.fish'

alias update 'sudo apt-get update && sudo apt-get upgrade && sudo apt dist-upgrade'
alias install 'sudo apt-get install'
alias remove 'sudo apt-get remove --purge'

alias l 'exa --long --header'

set --universal fish_greeting
```

## 🌈 exa

[exa](https://the.exa.website/) A modern replacement for `ls`.

![exa.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628595995985/GKmnpBAY-.png)

```sh
sudo apt install exa
exa --long --header
```

Tạo alias cho `exa` thông qua `fish sheel` (ở đây mình để alias là duy nhất chữ e-lờ -`l`):

```sh
alias l "exa --long --header"
# test alias
l
```

## 🏢 Office

<https://www.wps.com/>

[wps office](https://www.wps.com/), đẹp, siêu nhẹ, siêu nhanh, đa nền tảng

Nếu mở những file có dung lượng lớn (>20MB) nhất là định dạng `xlsx` thì nó nhanh hơn [libreOffice](https://www.libreoffice.org/) hơn hàng trăm lần (cảm nhận của mình).

Sở hữu tính năng tìm kiếm tên sheet trong trường hợp 1 `workbook` có tới hàng chục `sheet`.

`wps` cũng có bản web như `Microsoft Office` nhưng hạn chế dùng do thường có yêu cầu bảo mật không thể upload tài liệu lung tung lên cloud được.

Nên tải trực tiếp ở [đây](https://linux.wps.com/) và cài file đã được tải về bằng `gdebi` bên trên nhé, thay vì dùng dùng [snap store](https://snapcraft.io/store). Vì mình đã dùng thử bản ở `snap` không được update và nhiều bug.

## 📂 launcher

<https://ulauncher.io/>

Vấn đề là công cụ search app trên Ubuntu hơi kém, search không đúng kết qủa mong muốn.

Với tổ hợp phím default `ctrl` + `space` mở mọi thứ mọi nơi. Tuy nhiên nó lại trùng với tổ hợp phím `ctrl` + `space` trên vscode nên với tôi thì set nó thành `alt` + `X`.

## 🐚 SSH client

[termius](https://termius.com/) - tên khá dễ nhầm với `terminus` :D

Đa nền tảng Desktop kể cả iOS và android nên ngồi ị 🍰 vẫn có thể check status của server nhé.

Download tại [đây](https://termius.com/linux).

## 🚀 API testing tools

Lựa chọn nền web thay thế cho `postman`: [hoppscotch](https://hoppscotch.io/).

`hoppscotch` đẹp đơn giản và hỗ trợ `graphQL`.

## ✏ Bộ gõ tiếng Việt

Tại thời điểm viết bài, thì bộ gõ [teni-ime/ibus-teni](https://github.com/teni-ime/ibus-teni) đã bị đóng băng trên github (không được update thêm nữa).

Bạn có thể dùng [IBus Bamboo - Bộ gõ tiếng Việt cho Linux](https://github.com/BambooEngine/ibus-bamboo). Bộ gõ được viết bằng `Golang`.

Hãy cần thận tắt bộ gõ tiếng Việt trước khi gõ password trên `terminal` nhé. Do bộ gõ sẽ hiện phần text bị gạch chân (tạm) trên màn hình và có nguy cơ người bên cạnh nhìn thấy. Như vậy, tính năng nhập pass 1 cách âm thầm không hiển thị cả số lượng ký tự sẽ không còn ý nghĩa trong trường hợp này nữa.

## ✍️ Font

### Font để coding

Fira Code được opensource tại [đây](https://github.com/tonsky/FiraCode).

![Screenshot from 2021-08-10 18-35-18.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628595347994/HPGfgH-S2.png)

Font setting: `'Fira Code'`

### Font dành riêng cho tiếng Việt

`Be Vietnam Pro` download tại [đây](https://github.com/bettergui/BeVietnamPro/blob/main/fonts/ttf/BeVietnamPro-Regular.ttf).

![be-vietnam-pro-font.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628595376936/HJxVNLc9N.png)

Ngoài ra danh sách các kiểu chữ font này đều có tại [github repo](https://github.com/bettergui/BeVietnamPro).

Font setting: `'Be Vietnam Pro'`

![hair](https://media.giphy.com/media/8gUuSM6DgGLtYIBsOK/giphy.gif)

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

## Custom UI

Mặc định Ubuntu sẽ hiển thị 2 icon trên desktop.
Để desktop `sạch sẽ` hơn, ta ẩn `home` và `trash` icon đi.
Với version Ubuntu 20.XX bằng terminal:

```sh
gsettings set org.gnome.shell.extensions.desktop-icons show-trash false
gsettings set org.gnome.shell.extensions.desktop-icons show-home false
```

Tuy nhiên ở Ubuntu 21.04, sẽ có lỗi: `No such schema "org.gnome.shell.extensions.desktop-icons"`. Ta phải dùng `Extensions` app (Search trong danh sách App), disable phần `Desktop Icons NG (DING)`:

![Desktop Icons NG (DING).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629536115623/GzGFiartu.png)

## Tham khảo

- <https://www.ubuntupit.com/best-things-to-do-after-installing-ubuntu/>
- <https://www.lifewire.com/updated-software-for-ubuntu-with-ppas-2202103>
- [omgubuntu - Use Terminal to Remove Trash Icon](https://www.omgubuntu.co.uk/2020/03/remove-trash-from-desktop-ubuntu):
- [cyberciti.biz upgrade-ubuntu](https://www.cyberciti.biz/faq/upgrade-ubuntu-18-04-to-20-04-lts-using-command-line/)
- [askubuntu ubuntu-21-04-remove-trash-user-and-drive-icon-from-desktop](https://askubuntu.com/questions/1335398/ubuntu-21-04-remove-trash-user-and-drive-icon-from-desktop)
- [linuxconfig.org/how-to-install-tweak-tool](https://linuxconfig.org/how-to-install-tweak-tool-on-ubuntu-20-04-lts-focal-fossa-linux)
- [install-chrome-ubuntu](https://itsfoss.com/install-chrome-ubuntu/)

---

Còn nhiều thứ có thể nghịch với Ubuntu nữa, cơ mà sức mình có hạn :v

Wallpaper: [wallpaperaccess - skyrim](https://wallpaperaccess.com/skyrim-4k)

Photo at [pngegg](https://www.pngegg.com/en/png-zfazu)