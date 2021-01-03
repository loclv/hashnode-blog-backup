## So sánh 2 package phổ biến khi sử dụng webrtc peerjs và simple-peer 🤔

## Mở đầu

Chú ý:

- bài viết yêu cầu người đọc phải có hiểu biết cơ bản về `WebRTC` (Web Real-Time Communication).
- số liệu trong bài viết là tại thời điểm viết bài.

Khi sử dụng webrtc, để tránh những phiền hà và dễ sử dụng, người ta tạo ra những package bao bên ngoài những API native webrtc của trình duyệt.

### Vậy tại sao lại chỉ có `peerjs` vs `simple-peer`, trong khi còn những package khác?

Dựa vào tìm hiểu của bản bân thì đã có khoảng 4 package phổ biến khi tham khảo tại [đây](https://www.npmtrends.com/easyrtc-vs-peerjs-vs-simple-peer-vs-simplewebrtc)

- `easyrtc` thì dường như đã không còn open source và có repository khác tại [đây](https://github.com/open-easyrtc/open-easyrtc) với tên `open-easyrtc`. Số lượng star khá ít (119) nên tôi đánh giá là không phổ biến.

- [SimpleWebRTC](https://github.com/simplewebrtc/SimpleWebRTC) thì như thông báo ở phần `README` thì đã không còn được bảo trì ở thời điểm hiện tại nữa.

- [peerjs](https://github.com/peers/peerjs) thì có số star là `7.9k`.

- [simple-peer](https://github.com/feross/simple-peer) thì có số star là `4.5k`.

Vậy thì có nên chỉ đơn thuần dựa vào số star trên github để sử dụng `peerjs` luôn không?

## npm trending download

<https://www.npmtrends.com/easyrtc-vs-peerjs-vs-simple-peer-vs-simplewebrtc>

`simple-peer` có số lượng download nhiều hơn gần 8 lần!

Điều đó chứng tỏ nó đã được thực sự sử dụng nhiều hơn.

## issues

tại thời điểm 2020/07/23:

<https://github.com/feross/simple-peer/issues>

`simple-peer`: 44 issues is open

<https://github.com/peers/peerjs/issues>

`peerjs`: 74 issues is open

## Basic issues

`peerjs`:

<https://github.com/peers/peerjs/issues/630>

Mình đã theo dõi issue cơ bản này khá lâu, cho tới hiện tại là tháng 9 mà issue này đã có từ tháng 3.

Theo đánh giá bản thân thì issue này khá cơ bản mà mãi chưa thấy chủ repo support, chứng tỏ dự án không được thường xuyên maintain.

## Basic difference

### simple-peer

Sử dụng 1 object từ mỗi peer để khởi tạo kết nối bao gồm token định danh... Còn việc cho 2 peer trao đổi object đó như thế nào thì tùy bạn.

Hỗ trợ (hướng dẫn) [cách kết nối 2 peer trở lên](https://github.com/feross/simple-peer#connecting-more-than-2-peers) và [quản lý việc sử dụng bộ nhớ](https://github.com/feross/simple-peer#memory-usage).

### peerjs

Cần 1 `peerjs-server` mà package này đã tạo sẵn (khác với signaling server, turn, stun server). Điểm bất lợi là bạn phải không được tự do chọn cách trao đổi như `simple-peer`.

## Những ai đang sử dụng

`simple-peer` có chỉ ra [các tổ chứ đang dùng nó](https://github.com/feross/simple-peer#who-is-using-simple-peer) còn `peerjs` thì không.

Trong đó có `WebTorrent - Streaming torrent client in the browser`. Torrent thì khá nổi tiếng rồi đúng không :D