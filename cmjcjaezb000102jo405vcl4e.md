---
title: "Lệnh Terminal (Command Line) tắt các hiệu ứng chuyển động và độ trong suốt (transparency) trên macOS"
datePublished: Fri Dec 19 2025 07:14:27 GMT+0000 (Coordinated Universal Time)
cuid: cmjcjaezb000102jo405vcl4e
slug: lenh-terminal-command-line-tat-cac-hieu-ung-chuyen-dong-va-do-trong-suot-transparency-tren-macos
tags: macos

---

Lệnh Terminal (Command Line) tắt các hiệu ứng chuyển động và độ trong suốt (transparency) trên macOS không chỉ giúp tiết kiệm pin mà còn làm cho máy có cảm giác phản hồi nhanh hơn (snappy)

Dưới đây là tập hợp các lệnh Terminal (Command Line) hiệu quả nhất để thực hiện việc này.

## ⚠️ Lưu ý trước khi bắt đầu

Bạn cần mở ứng dụng **Terminal** (nhấn `Cmd + Space`, gõ "Terminal") để nhập các lệnh dưới đây. Sau khi nhập lệnh, giao diện có thể nháy nhẹ do các tác vụ như Dock và Finder khởi động lại.

---

## Combo lệnh tắt toàn bộ hiệu ứng (Khuyên dùng)

Bạn có thể copy và paste toàn bộ đoạn mã dưới đây vào Terminal rồi nhấn **Enter**. Nó sẽ tắt các hiệu ứng cửa sổ, hiệu ứng mở ứng dụng, và tăng tốc độ hiển thị.

```bash
# Tắt hiệu ứng mở/đóng cửa sổ
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false

# Tắt hiệu ứng khi mở Quick Look
defaults write -g QLPanelAnimationDuration -float 0

# Tắt hiệu ứng khi điều chỉnh kích thước cửa sổ (Resize)
defaults write NSGlobalDomain NSWindowResizeTime -float 0.001

# Tắt hiệu ứng khi mở ứng dụng từ Dock (icon nhảy tưng tưng)
defaults write com.apple.dock launchanim -bool false

# Tắt hiệu ứng trượt khi chuyển Desktop/Space (giảm motion)
defaults write com.apple.dock expose-animation-duration -float 0.1

# Tắt toàn bộ hiệu ứng trong Finder
defaults write com.apple.finder DisableAllAnimations -bool true

# Tắt độ trễ khi ẩn/hiện Dock (nếu bạn dùng chế độ Autohide)
defaults write com.apple.dock autohide-time-modifier -float 0

# Áp dụng thay đổi ngay lập tức
killall Dock Finder

```

---

### Tắt hiệu ứng "trong suốt" và "chuyển động" (Accessibility)

Hai cài đặt này ảnh hưởng lớn nhất đến GPU và Pin, nhưng thường được chỉnh trong System Settings. Bạn hãy vào:

- System Settings > Accessibility > Display
- Tích chọn thủ công vào `Reduce transparency` và `Reduce motion`.

Tuy nhiên, bạn có thể thử kích hoạt qua dòng lệnh (yêu cầu khởi động lại máy để có hiệu lực hoàn toàn):

```bash
# Giảm độ trong suốt (Reduce Transparency) - Giúp giảm tải GPU
defaults write com.apple.universalaccess reduceTransparency -bool true

# Giảm chuyển động (Reduce Motion)
defaults write com.apple.universalaccess reduceMotion -bool true
```

### Cách khôi phục về mặc định (Undo)

Nếu bạn cảm thấy giao diện quá cứng nhắc và muốn quay lại như cũ, hãy chạy đoạn lệnh sau:

```bash
defaults delete NSGlobalDomain NSAutomaticWindowAnimationsEnabled
defaults delete -g QLPanelAnimationDuration
defaults delete NSGlobalDomain NSWindowResizeTime
defaults delete com.apple.dock launchanim
defaults delete com.apple.dock expose-animation-duration
defaults delete com.apple.finder DisableAllAnimations
defaults delete com.apple.dock autohide-time-modifier
defaults delete com.apple.universalaccess reduceTransparency
defaults delete com.apple.universalaccess reduceMotion
killall Dock Finder

```
