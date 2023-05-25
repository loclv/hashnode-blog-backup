---
title: "Hiểu rõ bản chất tại sao Prime Video audio/video monitoring service tại sao lại giảm 90% chi phí khi chuyển sang kiến trúc monolith"
datePublished: Thu May 25 2023 03:08:28 GMT+0000 (Coordinated Universal Time)
cuid: cli2k173g000e09jtbask81up
slug: hieu-ro-ban-chat-tai-sao-prime-video-audiovideo-monitoring-service-tai-sao-lai-giam-90-chi-phi-khi-chuyen-sang-kien-truc-monolith
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/NQ6Lh81BTRs/upload/cb13e949194dfa1e0633a91c86147584.jpeg
tags: microservices-vietnamese, monolith-vietnamese, aws-vietnamese

---

Chúng ta không nên phán xét điều gì khi chưa hiểu rõ bản chất của nó.

Bài viết tham khảo từ video giải thích [How and Why Prime Video Tech Switched From Serverless to "Monolith" - by Be A Better Dev](https://www.youtube.com/watch?v=xflakXiwkD0), diễn giải tóm tắt lại.

## Vấn đề của Prime Video

Hãy nhìn ảnh dưới đây, khi phát sóng trực tiếp các trận cầu từ các nguồn khác như đài truyền hình, chắc hẳn bạn đã từng nhìn thấy vấn đề này.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684982201211/73c354b9-d376-42c5-9a49-cbbf15b3fc8c.webp align="center")

Nguồn ảnh: [https://www.primevideotech.com/video-streaming/how-prime-video-ingests-processes-and-distributes-live-tv-to-millions-of-customers-around-the-world-while-reducing-costs](https://www.primevideotech.com/video-streaming/how-prime-video-ingests-processes-and-distributes-live-tv-to-millions-of-customers-around-the-world-while-reducing-costs).

Có những loại vấn đề như:

* video đóng băng
    
* hình ảnh bị hư hỏng (như ảnh trên)
    
* sự cố đồng bộ hóa âm thanh/video
    
* ...
    

Như vậy cần thiết 1 audio/video monitoring service phân tích từng giây 1 của stream để alert về hệ thống, nhằm đưa cảnh báo và cần phải khắc phục.

Mỗi 1 stream - dòng chảy video/audio ở đây là tương ứng với mỗi 1 luồng: audio/video source =&gt; người dùng.

## Giải pháp tốn kém mà Prime Video đã dùng

Kiến trúc sử dụng AWS Step Function:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684982784315/0dff9c68-eb2a-4131-acad-37eea1845022.webp align="center")

Nguồn ảnh: [https://www.primevideotech.com/video-streaming/scaling-up-the-prime-video-audio-video-monitoring-service-and-reducing-costs-by-90](https://www.primevideotech.com/video-streaming/scaling-up-the-prime-video-audio-video-monitoring-service-and-reducing-costs-by-90).

Ta thấy mỗi AWS Step Function chứa 1 Detector, mỗi Detector là 1 monitor kiểm soát chất lượng Video. Xem thêm tại [https://www.amazon.science/blog/how-prime-video-uses-machine-learning-to-ensure-video-quality](https://www.amazon.science/blog/how-prime-video-uses-machine-learning-to-ensure-video-quality).

Sơ đồ trên được đơn giản hóa như sau:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684982959112/2d547036-e0e5-4b4c-bb63-33e0117b11b4.png align="center")

Nguồn ảnh: [How and Why Prime Video Tech Switched From Serverless to "Monolith" - by Be A Better Dev](https://www.youtube.com/watch?v=xflakXiwkD0).

Mỗi 1 giây của 1 stream sẽ được vận hệ thống monitor này phân tích, lưu kết quả vào S3 (write). Nó cũng có input lấy từ S3 (read). Khi có cảnh báo thì sử dụng Amazon SNS.

Ta để ý có 4 mũi tên màu xanh lá cây trong ảnh trên, mỗi mũi tên đó được tính là 1 state transition - sự chuyển đổi trạng thái. Vấn đề là AWS Step Function tính tiền theo mỗi 1 state transition.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684983486011/5d0777b5-2613-43d9-b3d2-cf840a242281.png align="center")

Nguồn ảnh: [https://aws.amazon.com/vi/step-functions/pricing/](https://aws.amazon.com/vi/step-functions/pricing/).

Cứ cho là có 100 user tương ứng 100 stream, mỗi stream chỉ 10 giây thì có (100 stream x 10 seconds x 4 state transition) = 4000 state transitions rồi. Như vậy với lượng user cực lớn kèm theo mỗi stream kéo dài nhiều tiếng đồng hồ thì chi phí phải cự kỳ lớn. Ở đây ta đã hiểu lý do tại sao chi phí lại lớn vậy.

## Giải pháp

Loại bỏ AWS Step Function:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684983719701/60b8f2e2-0149-4dd7-851e-bc2d1c0e9575.webp align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684983744471/2e0d3c33-9020-4857-a0af-6b55ee621673.webp align="center")

Đó là của Prime Video, họ đã chuyển sang monolith, tuy nhiên đây chỉ là các detector service mà thôi!

Còn có giải pháp khác như video [How and Why Prime Video Tech Switched From Serverless to "Monolith" - by Be A Better Dev](https://www.youtube.com/watch?v=xflakXiwkD0) đã mô tả, bạn có thể xem thêm tại video.

## Kết luận

Chúng ta không nên phán xét điều gì khi chưa hiểu rõ bản chất của nó.

Mọi phương pháp / công nghệ đều có ưu nhược điểm và sự đánh đối. Tùy từng trường hợp mà ta sẽ sử dụng phương pháp / công nghệ nào.

Không nên có cái nhìn ghét bỏ kiến trúc microservices hay monolith.