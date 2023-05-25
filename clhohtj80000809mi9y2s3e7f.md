---
title: "Chuyện Font tiếng Nhật"
datePublished: Mon May 15 2023 06:57:45 GMT+0000 (Coordinated Universal Time)
cuid: clhohtj80000809mi9y2s3e7f
slug: chuyen-font-tieng-nhat
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/OD9EOzfSOh0/upload/8424fa2f0c60ffb6af222c6806f8c321.jpeg
tags: font-japanese-for-vietnamese

---

## Nếu sử dụng font có sẵn phía client

Mình xin chia sẻ vấn đề sử dụng font tiếng Nhật. Dự án mình đã từng làm sử dụng như sau:

```css
html {
  font-family: メイリオ,meiryo,ヒラギノ角ゴ pro w3,hiragino kaku gothic pro,sans-serif;
}

// or

html {
  font-family: Hiragino Kaku Gothic Pro, ヒラギノ角ゴ Pro W3, メイリオ, Meiryo, ＭＳ Ｐゴシック, Roboto, sans-serif;
}
```

Nguồn tham khảo: [stackoverflow/japanese-standard-web-fonts](https://stackoverflow.com/questions/14563064/japanese-standard-web-fonts).

Thì xảy ra 1 số bug về độ dài và chiều cao của chữ khi dùng ở nhiều OS khác nhau. Cụ thể là Windows và macOS, bị lệch vài pixcel nên nó bị xuống dòng rồi chiều cao của dòng khác nhau... Nguyên nhân là do khi mình set font thế này thì browser sẽ tìm trong máy phía client (máy cá nhân của user) font name phù hợp nhất theo thứ tự mình sắp xếp. Ví dụ thứ tự ưu tiên là:

1. メイリオ
    
2. meiryo
    
3. ヒラギノ角ゴ pro w3
    
4. ...
    

## Hiểu rõ Font có sẵn phổ biến phía client

Về Hiragino:

> Hiragino là một họ kiểu chữ được thiết kế bởi Jiyukobo Limited. và được Screen Graphics Solutions Co., Ltd. bán cho các chuyên gia từ năm 1993. Đây là một trong những phông chữ tích hợp sẵn trong macOS và iOS. [Wikipedia/Hiragino](https://en.wikipedia.org/wiki/Hiragino)

Như vậy Hiragino là của macOS.

Về Meiryo (メイリオ):

> Meiryo là một kiểu chữ gothic sans-serif của Nhật Bản. Microsoft đã gói Meiryo với Office Mac 2008 như một phần của cài đặt tiêu chuẩn và nó thay thế MS Gothic làm phông chữ hệ thống mặc định trên các hệ thống Nhật Bản bắt đầu với Windows Vista. [Wikipedia](https://en.wikipedia.org/wiki/Meiryo)

Như vậy Hiragino là của Windows.

Xem 2 ảnh về 2 loại font này thì thấy rõ sự khác nhau. Nguồn tại [amayadori.cloud/blog/japanese-font-family](https://amayadori.cloud/blog/japanese-font-family).

## Giải pháp - sử dụng font chung

Tóm lại: nếu yêu cầu hỗ trợ nhiều OS thì nên tải font chung, free và open-source. Tuy nhiên chúng ta cũng phải chấp nhận chuyện phải download về máy client lần đầu tiên, vì những lần sau font đó sẽ được trình duyệt cached lại.

Font Roboto nó ko hỗ trợ tốt, hay nói cách khác là không có vector chuyên cho tiếng Nhật, ví dụ font [Zen Kaku Gothic Antique](https://fonts.google.com/specimen/Zen+Kaku+Gothic+Antique?query=Zen+Kaku+Gothic+Antique) thì mình vào web của nó sẽ thấy nó demo tiếng Nhật, nghĩa là nó chuyên cho tiếng Nhật.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684132905979/5794fd42-9735-4489-a842-74e577b6de9e.png align="center")

### Recommended font

[Zen Kaku Gothic Antique](https://fonts.google.com/specimen/Zen+Kaku+Gothic+Antique?query=Zen+Kaku+Gothic+Antique) or [Zen Kaku Gothic New](https://fonts.google.com/specimen/Zen+Kaku+Gothic+New?query=Yoshimichi+Ohira) Designed by Yoshimichi Ohira:

* Ưu điểm là được host trên Google fonts API.
    
* Opensource tại [https://github.com/googlefonts/zen-kakugothic](https://github.com/googlefonts/zen-kakugothic).
    

Source Han Sans:

* Opensource tại [https://github.com/adobe-fonts/source-han-sans](https://github.com/adobe-fonts/source-han-sans).
    
* Hỗ trợ nhiều định dạng như `SourceHanSansJP-VF.ttf.woff2`.
    

[Noto Sans Japanese](https://fonts.google.com/noto/specimen/Noto+Sans+JP):

* được host trên Google fonts API.
    
* Không mang đặc tính chữ viết tay, không có nét thanh nết đậm.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684990293386/dedb7147-cd4b-49d8-b148-8427f27f371f.png align="center")

[Noto Serif Japanese](https://fonts.google.com/noto/specimen/Noto+Serif+JP)

* được host trên Google fonts API.
    
* Mang đặc tính chữ viết tay, có nét thanh nết đậm
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684990203176/c88660c6-8bf5-41bf-a7ca-a508e1eb1e97.png align="center")

## Cách debug tìm Rendered Fonts

Mình muốn debug xem thực sự lúc nó render ra dùng font nào thì làm theo các bước sau:

1. mở browser DevTools
    
2. mở elements tab
    
3. trỏ vào element có text muốn kiểm tra
    
4. chọn tab con "computed" gần tab styles - như ảnh
    
5. xem mục "Rendered Fonts" =&gt; đây mới là font nó thực sự sử dụng.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684133761134/12d864bb-462b-4cd9-b8a0-c8875c1a77d7.png align="center")

Như ảnh trên thì font thực sự được sử dụng để render ra là `Ubuntu`.