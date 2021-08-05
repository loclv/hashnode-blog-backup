## ✍️ Bài học rút ra khi làm dự án trong thời gian dài gần 1 năm trở lên

Bài viết này chỉ là suy nghĩ từ cá nhân, chưa chắc đã đúng, cũng có thể khó áp dụng cho các dự án vì các lý do đặc thù của từng khách hàng!

Vừa qua tôi mới xong 1 phase của 1 dự án lớn và kéo dài gần 1 năm. Phase sau của nó thì không biết chạy đến khi nào luôn.

Qua đó, có 1 số điểm tốt tôi muốn chia sẻ về cách vận hành dự án dành cho các dự án về sau học tập.

Chú thích:

- spec: đặc tả của dự án
- QA: question and answer để làm rõ đặc tả dự án
- swagger: tài liệu thiết kế API theo chuẩn openAPI

## 🥲 Chia để trị với tài liệu dự án

Chia tài liệu dự án dạng Excel ra từng sheet không quá 100 rows.

Mà 30 rows là tôi cảm thấy đã quá nhiều rồi. Nhìn thấy cái sheet bị nhồi nhét lượng data hàng trăm rows thì nản thực sự! 🥲

### Đánh dấu trạng thái tài liệu

Ví dụ về tài liệu QA, các sheet nào trả lời chưa xong, chưa trả lời, đã trả lời hết đều phải đánh dấu theo 3 màu khác nhau.

## 🤷‍♀️ Tài liệu nhiều thì nên dùng tools dịch

Không nên khiến công việc của Comtor trở nên nhàm chán!

Việc dịch đi dịch lại các cụm từ đơn giản làm giảm hiệu suất công việc và gây nhàm chán cho Comtor.

Về mảng dịch thuật tài liệu, tương lai công việc của Comtor chỉ nên là kiểm tra lại bản đã dịch bằng tools xem đã OK hay chưa thôi.

Nếu khách hàng có phàn nàn về bản dịch thì vấn đề nằm ở phần kiểm soát chất lượng dịch chứ vấn đề không nằm ở chuyện dịch bằng tools.

Mục đích nữa là tiết kiệm công số cho dự án.

Ví dụ 1 số tool dành cho file Excel đó là:

- [memoQ](https://www.memoq.com/)
- [Microsoft Excel for Windows natively supports translation through the Microsoft Translator ribbon menu](https://www.microsoft.com/en-us/translator/business/excel/)
- [redokun](https://redokun.com/)
- [smartcat](https://www.smartcat.com/) - [How to translate Multilingual Excel files in Smartcat](https://youtu.be/kOhLgKJ89Bc)

## ✍️ Tài liệu nào đẩy lên git - công cụ quản lý version được thì đẩy hết lên

Khi đẩy tài liệu lên git hay các công cụ quản lý version, giúp dễ dàng quản lý thay đổi, dễ dàng biết được ai thay đổi, thay đổi những gì, thay đổi vào ngày nào.

Lịch sử thay đôi sẽ được tạo tự động, cụ thể thêm sửa xóa cái gì, đều có thể nắm được.

Ví dụ đối với dự án này đó là tài liệu thiết kế API - swagger.

Ngoài ra, dùng chung source-code repo, nơi để tài liệu, file QA với khách hàng được thì càng tốt.
Điều này giúp tiết kiệm được thời gian BrSE đồng bộ tài liệu dự án giữa 2 bên.

## 🧘🏽‍♀️ Coi trọng phần common - phần chung - phần shareable trong source-code

Dự án rất coi trọng phần common - phần base - code chung hay gọi cách khác là phần shareable trong source code của các màn hình / tính năng.

Dựa vào đó, coding rất nhanh và hiệu quả do đã tái sử dụng được logic / source-code.

Ở một số dự án khác, thậm chí các task về common rất ít. Phần common của 1 số dự án khác không được dành thời gian.

Thay vào đó app bị xé ra, mỗi ông chỉ lo xong task của mình. Dẫn tới phần common không tốt. Trái với phương trâm `clean code` hay nguyên lý SOLID trong lập trình, gây over công số 1 số dự án khác.

## 🛌🏽 Nên thêm Test-case không gọi 1 API 2 lần liên tiếp - gọi API vô nghĩa

Ủa thế điên hay sao mà gọi 2 lần?! Thực tế là chuyện này vẫn xảy ra.

Về mặt UI/UX, chẳng có gì xảy ra hết! Thậm chí ở 1 số dự án thì còn kệ, cũng chẳng coi là bug được vì lý do: `có làm sao đâu!`.

Tuy nhiên về mặt hiệu năng hệ thống thì giảm xuống khi call API không cần thiết.

Thực tế dự án này cũng đã gặp vài bug này liên quan tới chuyện xử lý bất đồng bộ nhất là khi xử lý API.

Ngoài ra còn gọi API để update data, tuy nhiên lại không update data y như cũ!

## 🤹🏽‍♀️ Nắm vững kỹ thuật trong quản lý

PM nắm được hết các logic phần coding ở mức `Detail Design`, nên task sao lại chậm, sao lại chưa xong đều hiểu.

Nếu như các dự án khác PM không nắm được logic, các bước để develop thì không thể hiểu được tại sao task lại chưa xong, không hiểu rõ độ khó các task.

Từ đó không nắm được lý do lại over công số để tìm hướng khắc phục.

Các PM khác nên học hỏi. Suy cho cùng thì PM vẫn phải cứng về kỹ thuật, mặc dù cú pháp, framework có thể chưa rõ.

## ⛹🏽‍♀️ Mô hình nhiều BrSE thời điểm đầu, về sau `spec` đã clear thì có thể sang dự án khác support

>Lấy chỗ thừa bù chỗ thiếu

Ngày trước làm BrSE, giai đoạn đầu, QA nhiều, lại phải trả lời thật nhanh để còn làm.

Bị thúc sấp mặt, OT nhiều và bận kinh khủng. Về sau thì rảnh dần, đến cuối là gần như không còn QA lại rất rảnh.

Vì thế Mô hình nhiều BrSE thời điểm đầu, về sau `spec` đã clear thì có thể sang dự án khác support, cần được khuyến khích.

Tất nhiên là mô hình này chỉ nên áp dụng cho các BrSE phía Việt Nam.

## 🏄🏽‍♀️ Áp dụng tools ngay từ đầu, đừng ngại tạo ra tools

Đối với dự án lớn, nên dùng tool giải quyết các vấn đề gặp phải lặp đi lặp lại ngay từ đầu sẽ tiết kiệm nhiều công số.

## 🏌🏽‍♀️ Khi gặp dự án có `Spec` sơ sài

Thiết kế các màn hình ban đầu khi mới nhận dự án còn sơ sài, thế nên các BrSE sẽ vào clear tất cả spec trước.

Tránh để đến lúc coding mà vẫn còn phải QA, làm delay dự án.

Việc đưa BrSE vào clear spec giai đoạn đầu hoặc viết `Detail Design` trước khi coding tránh được thời gian chờ QA được trả lời xong thì mới code được tiếp.

## 👩🏽‍🏫 Regex hóa thông tin validation trong `Spec` được thì tốt

Thông tin validation trong `Spec` được mô tả bằng lời nói, thế nên khách hàng có thể hiểu mô tả đó 1 kiểu, team dự án cũng hiểu 1 kiểu.

Đặc biệt với dự án Team backend và frontend là tách biệt. Thì việc Regex hóa là việc nên làm.

Dựa vào bộ công cụ mô hình hóa Regex, ví dụ như [ihateregex](https://ihateregex.io/) thì tester cũng hoàn toàn nắm được logic và logic cụ thể được thực thi trong source-code.

Ngoài ra, nếu sử dụng swagger thì càng nên dùng vì regex có thể được định nghĩa trong thuộc tích `pattern`. Ví dụ:

```yaml
abcName:
  description: 'abc name'
  type: string
  pattern: '^[a-zA-Z0-9!-/:-@[-`{-~]{0,256}$'
```

## 👩🏽‍💻 Nâng cao trình độ chuyên môn bằng các buổi TechTalk hàng tuần

>"Học, học nữa, học mãi" - của V.I.Lê-nin

Trước đây mình đã ở trong team mà mỗi tuần sẽ luân phiên từng người phải thuyết trình về 1 vấn đề kỹ thuật đã được team lựa chọn.

Lần này cũng được trải nghiệm lại khi `rảnh task`, thấy có ích rất nhiều với trình độ chuyên môn, tạo thêm hứng thú tìm hiểu công nghệ.

Nếu dự án nào không bị `lụt task` thì có thể xem xét tổ chức hàng tuần hoặc hàng tháng.

Những buổi chia sẽ như thế, ai trong công ty cũng có thể joint.

---

Các dự án khác cũng nên học hỏi! 🙏🏽

---

Photo by <a href="https://unsplash.com/@jimmydean?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Jimmy Dean</a> on <a href="https://unsplash.com/@jimmydean?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
