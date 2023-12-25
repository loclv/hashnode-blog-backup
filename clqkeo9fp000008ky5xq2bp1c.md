---
title: "Khi nào cần git branh cho môi trường STG (staging) hoặc môi trường testing"
seoTitle: "Khi nào cần git branh cho môi trường STG (staging) hoặc testing"
seoDescription: "Khi nào cần git branh cho môi trường STG (staging) hoặc môi trường testing"
datePublished: Mon Dec 25 2023 04:15:56 GMT+0000 (Coordinated Universal Time)
cuid: clqkeo9fp000008ky5xq2bp1c
slug: khi-nao-can-git-branh-cho-moi-truong-stg-staging-hoac-moi-truong-testing
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/OhE6wMahECM/upload/1416f29ce1856ff3cb322b87dae3b874.jpeg
tags: git

---

## Khi nào không cần?

- Khi các task được deploy lên STG là ngay lập tức được deploy lên môi trường PROD (production) luôn. Điều này đòi hỏi làm tới đâu, test tới đó, deploy được PROD luôn. Khả năng này xảy ra thực rất thấp.

## Vấn đề

Có nhiều task đang cần deploy STG nhưng chưa đc merge vào main (để deploy PROD).
Mình cứ deploy STG ở branch mình làm thì sẽ miss mất commit khác ở STG đã được deploy.

Ví dụ:

- branch `feature/a` đã được deploy trong quá khứ
- branch `feature/b` thì do là checkout từ `main` ra, nên miss mất commit của branch `feature/a` nên khi được deploy sẽ không test được `feature/a` ở STG nữa.

Giải pháp là mình sẽ tạo 1 branch `stg` để gộp các commit cần deploy ở STG.
Dẫn đến là branch `feature/a`, `feature/b` phải được merge vào branch `stg`.
Giờ là trước khi deploy stg/prod branch nào thì mình sẽ merge branch đó vào branch `stg`.

Tương tự như deploy branch `main` lên PROD.

Ngoài ra bạn muốn quản lý source-code nào đang nằm trên STG để tiện debug.
