## Tại sao chip M1 của Apple 🍏 lại nhanh đến vậy? Giải thích ngắn gọn

Với review của hàng nghìn Youtuber về hiệu năng của Apple M1, chắc bạn cũng phải tự hỏi Tại sao chip M1 của Apple lại nhanh đến vậy?

Mình xin giải thích ngắn gọn điều đó dựa vào bài viết [này](https://debugger.medium.com/why-is-apples-m1-chip-so-fast-3262b158cba2) trên [medium](https://medium.com/).

## Bản chất của M1

> The M1 is not a CPU, it is a whole system of multiple chips put into one large silicon package. The CPU is just one of these chips.

`M1 KHÔNG CHỈ là CPU!`

Bất ngờ chưa?! M1 là 1 tấm silicon được tích hợp nhiều `máy tính`!

Trong Video giới thiệu M1 chính thức từ Apple thì tại [đây - giây thứ 36](https://youtu.be/umoEDgl_xBo)

Ảnh các thành phần riêng biệt trên mainboard của Apple (lấy ra từ video):


![base.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615024476652/RU9nXoiZC.png)

Ảnh các thành phần được ghép lại chip M1:

![merged.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615024487939/nw0JP65Ck.png)

## Chiến lược của Apple 🦄

Không giống như phong trào thêm thật nhiều CPU `general-purpose cores` - hay nhiều CPU `cái gì cũng biết làm nhưng mỗi thứ biết có 1 tý`, thì Apple lại chọn lối đi riêng. Đó là tạo ra thật nhiều bộ xử lý chuyên biệt có 1 nhiệm vụ cụ thể, giống như các cụ có câu:

> Một nghề cho chín còn hơn chín nghề.

Giống như trong xã hội, mỗi người 1 chuyên môn thì tựu chung lại năng suất lao động toàn xã hội sẽ cao hơn là ai cũng biết làm 1 tý nhưng không chuyên.

Tất nhiên là trong số các bộ xử lý trong M1 cũng có 1 khối CPU chuyên để chạy những đoạn code OS, APP giống như CPU truyền thống, nhưng ngoài ra còn có:

- Graphics processing unit (GPU) - Quá quen với các Game thủ, xử lý đồ họa.
- Image processing unit (ISP) - xử lý hình ảnh.
- Digital signal processor (DSP) - xử lý hàm toán học phức tạp hơn so với CPU thông thường, bao gồm giải mã file âm nhạc.
- Neural processing unit (NPU) — xử lý các task về machine learning (AI).
- Video encoder/decoder — xử lý video files, do đó mà các thử nghiệm xử lý video luôn cho kết quả đáng kinh ngạc.
- Secure Enclave — mã hóa và giải mã hiệu quả phục vụ vấn đề authentication.
- Unified memory — cho phép CPU, GPU và các core khác trao đổi thông tin với nhau.

Các bạn thấy đấy, các core bên trên giống như 1 xã hội thu nhỏ vậy.

## M1 Unified RAM - Bộ nhớ hợp nhất

Tất cả các chip vi xử lý như CPU, GPU, NPU... đều dùng chung vùng nhớ này. Không cần phải copy để chuyển data từ RAM sang bộ nhớ của GPU như kiến trúc máy tính truyền thống. Như vậy tốc độ truyền tải thông tin sẽ nhanh hơn rất nhiều!

Tham khảo [8GB vs 16GB vs 24GB for M2 Mac — The TRUTH about RAM!](https://youtu.be/UMW4w6wMdL8)

## 🤔 Ơ thế sao những nhà sản xuất khác không thể làm như vậy?

Khác biệt đến từ mô hình kinh doanh!

Đối với máy tính truyền thống ta phải lắp ráp từng phần của máy tính từ các nhà cung cấp như CPU của Intel, GPU của NVIDIA lại. Điều đó khiến mỗi nhà sản xuất không thể hàn chết RAM chung lại với nhau như Apple.

Apple thì khác, tự chủ toàn bộ các loại chip, có thể hợp nhất tất cả thành phần từ phần cứng lẫn phần mềm. Nói đúng hơn là họ phải làm vậy khi thiết kế iPhone. Thành ra M1 cũng là kết quả của việc phát triển iPhone ngần ấy năm.
