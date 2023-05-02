---
title: "Việc điền coding review checklist mỗi lần tạo pull-request có thực sự cần thiết?"
datePublished: Tue May 02 2023 16:40:11 GMT+0000 (Coordinated Universal Time)
cuid: clh6hwh8w000909kzekti9uek
slug: viec-dien-coding-review-checklist-moi-lan-tao-pull-request-co-thuc-su-can-thiet
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/RLw-UC03Gwc/upload/bc89483fbaee42286b42f448196dee6d.jpeg
tags: review-code-vietnam

---

Quy trình điền coding review checklist nếu có sẽ là:

* Dev tạo ra mỗi PR 1 bản rồi check vào.
    
* Sau đó reviewer lại check lại và xác nhận đúng chưa?
    
* Manager sẽ kiểm tra xem các PR có checklist tương ứng hay không, việc này có thể được thực hiện hàng ngày.
    

Về coding review checklist mỗi lần tạo pull-request (viết tắt là PR). Có 3 vấn đề sau đây:

## Tính hiệu quả

Trung bình, mỗi dev sẽ tạo 2 PR 1 ngày. Mỗi ngày 1 team 4 dev thì có khoảng 8 PR. Mỗi 1 checklist tốn trung bình 4 phút tạo và check cho cả dev và reviewer, nếu là review nghiêm túc. Còn mình check cho có, check không có tâm thì chỉ vài giây thôi. Như vậy thời gian để tạo và check của 1 team 4 người là 4 phút x 8 PR = 32 phút tất cả. Tuy việc thời gian như vậy là nhỏ đối 1 team, nhưng mình thử suy nghĩ xem bình thường 1 user sử dụng 1 app, việc thêm thao tác dù chỉ mất thêm vài giây đã gây khó chịu rồi... Tất nhiên là gây khó chịu cho dev, nhưng mình xem hiệu quả đến đâu nhé.

Có dev thì coi đó như 1 thủ tục thôi. Thậm chí còn có chuyện 1 tiêu chí đã check trong checklist rồi, nhưng soi ra source-code vẫn vi phạm. Bởi vì hầu hết chỉ điền cho có, chưa ăn sâu vào thực hành.

Thế làm thế nào ăn sâu vào thực hành? Reviewer comment và bắt sửa thì mới cho merge, lần sau chừa, thì mới được merge, tự khắc sẽ ăn sâu vào thực hành.

Đối với 1 dev với vào ngành, mình không thể bắt bạn đó điền OK hết mà trong PR không có lỗi được, thực tế là điều đó nó không xảy ra được. Thậm chí với người nhiều năm kinh nghiệm.

## Tính bao phủ - coverage

Tính bao phủ của checklist trả lời câu hỏi là checklist này đã đầy đủ, bao phủ các công nghệ liên quan, coding-style, security hay chưa. Nếu tạo chung cho tất cả các dự án thì tất nhiên là các check-list phải chung nhất, tuy nhiên không thể sâu vào công nghệ. Nếu như từng dự án, tech-stack tạo ra cho mình 1 checklist riêng thì số lượng phải checking item thông thường rất lớn khoảng 50 vấn đề đầu mục. Nếu bỏ thời gian đọc từng mục, điền thực sự nghiêm túc thì cần nhiều thời gian hơn nữa.

Có thực sự cần thiết hay không?

Không có checklist thì vẫn review và develop như thường thôi. Tại sao lại vậy?

Nếu 1 team được có review cẩn thận thì họ sẽ học ngay từ comment trong PR rồi. Còn những vấn đề về security thì được học, có nhận thức từ các buổi học định kỳ hàng năm rồi. Các buổi học này các công ty ở Nhật rất hay tổ chức, ngay cả công ty không thuần tech. Checklist có giảm được các lỗi về security không? Có, có giảm được, tuy nhiên checklist đó người ta hay dùng là checklist khi release. Ở 1 số công ty production mà mình biết, trong đó có công ty cũ thì việc làm checklist khi release là điều rất chặt chẽ và bắt buộc. Buộc phải có ít nhất 2 người làm, review các bước trong kịch bản, khoanh vùng ảnh hưởng. Người ta làm rất nghiêm túc nên hiệu quả cao. Không nghiêm túc thì hiệu quả làm sao được?

## Như vậy giải pháp thay thế là gì?

* tạo checklist khi release
    
* các buổi học định kỳ hàng năm về security, thông tin cá nhân hằng năm
    
* đối với dev mới thì tổ chức cả techtalk nâng cao chất lượng code