---
title: "MongoDB - khi sử dụng upsert làm sao để khi create/insert document mới thì tạo thêm trường createdAt?"
seoDescription: "MongoDB - khi sử dụng upsert làm sao để khi create/insert document mới thì tạo thêm trường createdAt? setOnInsert"
datePublished: Fri Nov 01 2024 03:08:24 GMT+0000 (Coordinated Universal Time)
cuid: cm2y5n6yw000209l2alyybulf
slug: mongodb-khi-su-dung-upsert-lam-sao-de-khi-createinsert-document-moi-thi-tao-them-truong-createdat
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/vkX3X_xNwjQ/upload/8c2208d994b8d7dc4242c0a281cc45d0.jpeg
tags: mongodb, mongodb-vietnam

---

Khi sử dụng `upsert` trong MongoDB, bạn muốn thêm trường `createdAt` với thời gian hiện tại chỉ khi document được tạo mới?

Bằng cách dùng operator `$setOnInsert`. Đây là một operator đặc biệt trong MongoDB chỉ cập nhật giá trị khi tài liệu được chèn mới (tức là khi không tìm thấy tài liệu nào khớp với điều kiện và MongoDB phải tạo tài liệu mới).

Dưới đây là cách sử dụng `$setOnInsert` với `upsert` (ví dụ lấy ra từ docs của MongoDB):

```typescript
db.products.updateOne(
  { _id: 1 },
  {
     $set: { item: "apple" },
     $setOnInsert: { defaultQty: 100 }
  },
  { upsert: true }
)
```

Document mới nếu được tạo ra:

```json
{ "_id" : 1, "item" : "apple", "defaultQty" : 100 }
```

3 việc mà MongoDB đã thực hiện trong trường hợp tạo mới:

* Tạo mới document
    
* set data bằng operation `$set`
    
* set data bằng operation `$setOnInsert`
    

## [Tham](https://www.mongodb.com/docs/manual/reference/operator/update/set/#mongodb-update-up.-set) [khảo](https://www.mongodb.com/docs/manual/reference/operator/update/setOnInsert/#mongodb-update-up.-setOnInsert)

* [htt](https://www.mongodb.com/docs/manual/reference/operator/update/setOnInsert/#mongodb-update-up.-setOnInsert)[ps://www.mongodb.c](https://www.mongodb.com/docs/manual/reference/operator/update/setOnInsert/)[om/docs/manu](https://www.mongodb.com/docs/manual/reference/operator/update/setOnInsert/#mongodb-update-up.-setOnInsert)[al/reference/operator/update/setOnInsert/](https://www.mongodb.com/docs/manual/reference/operator/update/setOnInsert/)