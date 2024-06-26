---
title: "🐧 Tools cho Ubuntu sau khi mới cài"
seoTitle: "🐧 Tools cho Ubuntu sau khi mới cài"
seoDescription: "🐧 Tools cho Ubuntu sau khi mới cài
editor, terminal, deb installer, office, launcher, ssh, api tools, bộ gõ, update upgrade ubuntu"
datePublished: Mon Nov 30 2020 17:43:54 GMT+0000 (Coordinated Universal Time)
cuid: cki4ud8rk07d2ans1br1p5kqy
slug: tools-cho-ubuntu-sau-khi-moi-cai
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1630402501140/piNkD_5KE.png
tags: ubuntu, linux

---

Bài viết dành cho những người mới với `Ubuntu` (bản dành cho máy tính cá nhân), thời điểm mới cài Ubuntu xong.

Thời điểm viết bài mình đã thử `ubuntu 21.04` và không gặp vấn đề gì cả. `ubuntu 21.04` có thư viện đồ họa được nâng cấp và tối ưu khiến tốc độ nhanh hơn, điển hình là khi scroll trong danh sách các App.

## 🎈 Upgrade lên Ubuntu bản mới nhất

```sh
sudo do-release-upgrade
```

Sau khi download lượng lớn dữ liệu, cài đặt và restart, việc của ta là loại bỏ những thư viện / app phiên bản cũ:

```sh
sudo apt --purge autoremove
```

Trong quá trình upgrade Ubuntu thì để an toàn Ubuntu tự động disable các repo của bên thứ 3. Các repo này vốn là nơi chứa bản update của những phần mềm bên thứ 3 (không phải phần mềm của Ubuntu). Enable lại các repo này, giúp việc update thông qua command `sudo apt update` trở lại như cũ.

Để enable lại thì ta:

1. vào danh sách các App
    
2. search `update`
    
3. chọn `Software & Updates`
    
4. vào tab `Other Software`
    
5. Enable lại các repo có ghi chú `disabled on upgrade to ${ubuntu-version-name}`
    

![update-repo.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629534955375/sBtTL8u2ay.png align="left")

## 🪫 Power mode

Cũng từ phiên bản này, nếu máy ta dùng là Laptop thì có thêm lựa chọn mức độ nguồn điện - power dành cho hiệu năng hoặc tiết kiệm điện. Mình chọn tối ưu cho hiệu năng:

![ubuntu-power.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629532529207/2ywbxXvVVC.png align="left")

## 📦 deb installer - `gdebi-gtk`

Mô tả `gdebi-gtk` nguyên văn dưới đây.

> gdebi lets you install local deb packages resolving and installing its dependencies. apt does the same, but only for remote (http, ftp) located packages.

Đại khái `gdebi` dùng để cài `deb packages` - tương ứng với `.exe` bên `window` hay `.dmg` bên `MacOS`. Nó cũng giống với công cụ `apt` được tích hợp sẵn trong `Ubuntu` chỉ trừ là có giao diện UI và cài `deb packages` đã được tải về máy. Không thì bạn sẽ phải dùng `dpkg` 1 cách manual và phức tạp. Thông tin này tham khảo tại [đây](https://itsfoss.com/install-deb-files-ubuntu/).

Cũng là để tránh `dependency error` mà `default Software Center` có thể gây ra.

Cách dùng `gdebi-gtk` tại [đây](https://itsfoss.com/gdebi-default-ubuntu-software-center/).

Cách cài đặt tham khảo từ [https://www.ubuntu18.com/install-gdebi-ubuntu-18/](https://www.ubuntu18.com/install-gdebi-ubuntu-18/):

```bash
sudo add-apt-repository universe
sudo apt-get update
sudo apt-get install gdebi-core
# install GDebi GUI
sudo apt-get install gdebi
```

Để xóa 1 package đã cài với `gdebi` ta xóa như thông thường:

```bash
sudo apt purge package-name
```

### 🍄 Cài Chrome thông qua file đuôi `.deb`

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

## 🌏 Terminal

### Command-line interface

Default terminal của Ubuntu nhanh, đơn giản. Như vậy là đủ.

Nhưng đối với những bạn thích custom hay vọc vạch thì hãy thử dùng các terminal client bên dưới xem nhé: 🌂

* [hyper](https://hyper.is/): [đây](https://gist.github.com/loclv/67477636e417e974a07f930d72495eaa) là settings dành cho `hype` của mình.
    

```json
plugins: [
    'hyper-font-ligatures',
    'hypercwd',
    'hyper-active-tab'
  ],
```

Plugin `hypercwd` mở tab mới giữ nguyên đường dẫn `path`, thay vì thư mục `HOME`. Plugin `hyper-active-tab` để đánh dấu tab đang active ở vị trí nào.

* [tabby](https://tabby.sh/) - Tabby is an infinitely customizable cross-platform terminal app for local shells, serial, SSH and Telnet connections.

Ảnh UI của tabby:

![Screenshot from 2022-03-15 16-41-32.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647357703712/OSMZIfgpxx.png align="left")

### 🐚 Command-line shell

[fish shell](https://fishshell.com/) + [Oh my fish](https://github.com/oh-my-fish/oh-my-fish) - quản lý packages dành cho `fish shell`.

Cách cài đặt fish shell bằng command line có tại [đây](https://www.geeksforgeeks.org/how-to-install-and-configure-fish-shell-in-ubuntu/). Tóm tắt:

```bash
sudo apt-add-repository ppa:fish-shell/release-3
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install fish

which fish
# output: `/usr/bin/fish`

# Make fish shell as default shell
sudo chsh -s /usr/bin/fish

# install Oh my fish
curl https://raw.githubusercontent.com/oh-my-fish/oh-my-fish/master/bin/install | fish
omf -v
```

Để config fish shell ta sẽ edit file: `~/.config/fish/config.fish`. Ta có thể dùng editor yêu thích để edit:

```bash
code ~/.config/fish/config.fish
# or
vi ~/.config/fish/config.fish
```

Dưới đây là các alias được config thông qua `fish shell`:

```plaintext
alias g='git'
alias gs='git status'
alias ga='git add .'
alias gd='git diff'
alias gp='git push'
alias gpick='git cherry-pick'

alias cf 'code ~/.config/fish/config.fish'

alias up 'sudo snap refresh && sudo apt-get update && sudo apt-get upgrade && sudo apt dist-upgrade'
alias install 'sudo apt-get install'
alias remove 'sudo apt-get remove --purge'
alias clean 'sudo apt autoremove && sudo apt autoclean -y'
alias c 'clear'

alias l 'exa --long --header -a'

set --universal fish_greeting
```

Ngoài ra còn có 1 tool khá màu mè dành cho shell, đó là:

* [https://github.com/starship/starship](https://github.com/starship/starship)

> [starship](https://github.com/starship/starship) - The minimal, blazing-fast, and infinitely customizable prompt for any shell!

Ảnh demo khi sử dụng:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678184687626/356798ef-125c-4074-b420-33c1fdc4ae54.png align="center")

* [https://github.com/nushell/nushell](https://github.com/nushell/nushell) - A new type of shell.
    

## 🌈 exa

[exa](https://the.exa.website/) A modern replacement for `ls`.

![exa.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628595995985/GKmnpBAY-.png align="left")

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

[https://www.wps.com/](https://www.wps.com/)

[wps office](https://www.wps.com/), đẹp, siêu nhẹ, siêu nhanh, đa nền tảng

Nếu mở những file có dung lượng lớn (&gt;20MB) nhất là định dạng `xlsx` thì nó nhanh hơn [libreOffice](https://www.libreoffice.org/) hơn hàng trăm lần (cảm nhận của mình).

Sở hữu tính năng tìm kiếm tên sheet trong trường hợp 1 `workbook` có tới hàng chục `sheet`.

`wps` cũng có bản web như `Microsoft Office` nhưng hạn chế dùng do thường có yêu cầu bảo mật không thể upload tài liệu lung tung lên cloud được.

Nên tải trực tiếp ở [đây](https://linux.wps.com/) và cài file đã được tải về bằng `gdebi` bên trên nhé, thay vì dùng dùng [snap store](https://snapcraft.io/store). Vì mình đã dùng thử bản ở `snap` không được update và nhiều bug.

## 📂 launcher

[ulauncher.io](https://ulauncher.io)

![demo.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1664266594882/1aCBM00QN.gif align="left")

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

![Screenshot from 2021-08-10 18-35-18.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628595347994/HPGfgH-S2.png align="left")

Font setting: `'Fira Code'`

### 🦜 Font dành riêng cho tiếng Việt

`Be Vietnam Pro` download tại [đây](https://github.com/bettergui/BeVietnamPro/blob/main/fonts/ttf/BeVietnamPro-Regular.ttf).

![be-vietnam-pro-font.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628595376936/HJxVNLc9N.png align="left")

Ngoài ra danh sách các kiểu chữ font này đều có tại [github repo](https://github.com/bettergui/BeVietnamPro).

Font setting: `'Be Vietnam Pro'`

![hair](https://media.giphy.com/media/8gUuSM6DgGLtYIBsOK/giphy.gif align="left")

## 😅 Nếu không thấy emoji hiển thị đúng

Nếu không thấy emoji hiển thị đúng - các ký tự hình chữ nhật thì có lẽ bạn đang gặp cùng vấn đề với bài viết [Emojis Missing from Chrome in Ubuntu](https://medium.com/@harshmaur/emojis-missing-from-chrome-in-ubuntu-9c25fe10867c).

Tóm tắt là xóa đi cài lại `fonts-noto-color-emoji`.

```bash
sudo apt-get remove fonts-noto-color-emoji
sudo apt-get install fonts-noto-color-emoji
```

## 👆 Update

Thường xuyên chạy update các package mới nhất để tăng tính bảo mật:

```sh
sudo apt-get update && sudo apt-get upgrade && sudo apt dist-upgrade
# clean
sudo apt --purge autoremove
```

Đối với `snap` thì đôi khi cũng không tự động update được do ứng dụng cần update lúc nào cũng được mở. Để manual update ta dùng:

```sh
sudo snap refresh
```

## Thêm Repositories cho software & update

Thêm repo thêm nơi để cài đặt các package.

Nhưng tại sao khi đã có defaul repo rồi?

Vì `Canonical Partners repository` hay các repo khác chứa source đóng chứa 1 số app (triết lý linux là open-source).

### Cách thêm

Ấn `super key (Windows key)`, search `software & update`, vào `software tab`, enables `Canonical Partners`, `Community-maintained`, `Proprietary drivers`, ... trừ `Source Code`.

Vào `Other software tab`, enables các Repo trừ phần `Source Code` trừ khi bạn có ý định kéo cả code của package về :D

## 👒 Custom UI

Mặc định Ubuntu sẽ hiển thị 2 icon trên desktop. Để desktop `sạch sẽ` hơn, ta ẩn `home` và `trash` icon đi. Với version Ubuntu 20.XX bằng terminal:

```sh
gsettings set org.gnome.shell.extensions.desktop-icons show-trash false
gsettings set org.gnome.shell.extensions.desktop-icons show-home false
```

Tuy nhiên ở Ubuntu 21.04, sẽ có lỗi: `No such schema "org.gnome.shell.extensions.desktop-icons"`. Ta phải dùng `Extensions` app (Search trong danh sách App), disable phần `Desktop Icons NG (DING)`:

![Desktop Icons NG (DING).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629536115623/GzGFiartu.png align="left")

## Tham khảo

* [https://www.ubuntupit.com/best-things-to-do-after-installing-ubuntu/](https://www.ubuntupit.com/best-things-to-do-after-installing-ubuntu/)
    
* [https://www.lifewire.com/updated-software-for-ubuntu-with-ppas-2202103](https://www.lifewire.com/updated-software-for-ubuntu-with-ppas-2202103)
    
* [omgubuntu - Use Terminal to Remove Trash Icon](https://www.omgubuntu.co.uk/2020/03/remove-trash-from-desktop-ubuntu):
    
* [cyberciti.biz upgrade-ubuntu](https://www.cyberciti.biz/faq/upgrade-ubuntu-18-04-to-20-04-lts-using-command-line/)
    
* [askubuntu ubuntu-21-04-remove-trash-user-and-drive-icon-from-desktop](https://askubuntu.com/questions/1335398/ubuntu-21-04-remove-trash-user-and-drive-icon-from-desktop)
    
* [linuxconfig.org/how-to-install-tweak-tool](https://linuxconfig.org/how-to-install-tweak-tool-on-ubuntu-20-04-lts-focal-fossa-linux)
    
* [install-chrome-ubuntu](https://itsfoss.com/install-chrome-ubuntu/)
    

---

Còn nhiều thứ có thể nghịch với Ubuntu nữa, cơ mà sức mình có hạn :v

Wallpaper: [wallpaperaccess - skyrim](https://wallpaperaccess.com/skyrim-4k)

Photo at [pngegg](https://www.pngegg.com/en/png-zfazu)