---
title: "Regex - Những thói quen nên làm khi xử lý chuỗi Regex phức tạp 🌵"
datePublished: Fri May 26 2023 07:02:07 GMT+0000 (Coordinated Universal Time)
cuid: cli47tivw000409lahjkyay40
slug: regex-nhung-thoi-quen-nen-lam-khi-xu-ly-chuoi-regex-phuc-tap
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/1MHU3zpTvro/upload/beef48aed4c6044ea64ffa189d58500e.jpeg
tags: regex-vietnamese

---

## Hiểu về nó

Để hiểu về 1 chuỗi regex ta có thể sử dụng biểu đồ tuần tự được tạo ra tự động. Ví dụ ta có thể dùng [regexper.com](https://regexper.com/) hoặc [ihateregex.io/expr/phone/](https://ihateregex.io/expr/phone/) với phone regex:

> **^**\[**\\+**\]**?**\[(\]**?**\[0-9\]**{3}**\[)\]**?**\[-**\\s\\.**\]**?**\[0-9\]**{3}**\[-**\\s\\.**\]**?**\[0-9\]**{4,6}$**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685083942380/95d04b8c-aa0c-490c-aea5-e89123859fec.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685083995481/4dd0a8b4-40d8-47c5-9c5f-0172b39f562b.png align="center")

Nhìn vào các mũi tên trong biểu đồ trên, rất dễ hiểu đúng không?

## Viết test case cho Regex

Viết test case hay Unit Test đơn giản, trực quan với [regexr.com](https://regexr.com/):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685084270453/5d9c4384-c6f4-4c59-bb47-2f7364fe56e0.png align="center")

Bước này đôi khi quan trọng không kém vì Regex logic phức tạp rất nhiều case mà ta khó lường tới.