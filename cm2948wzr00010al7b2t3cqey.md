---
title: "Giải thích staleTime trong @tanstack/react-query"
datePublished: Mon Oct 14 2024 14:35:04 GMT+0000 (Coordinated Universal Time)
cuid: cm2948wzr00010al7b2t3cqey
slug: giai-thich-staletime-trong-tanstackreact-query
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/zNN6ubHmruI/upload/f0139e521f4438b9aad7803f57e843a9.jpeg

---

## Định nghĩa

Trong thư viện `@tanstack/react-query`, thuộc tính `staleTime` là một trong những tùy chọn quan trọng khi cấu hình các query. Nó quyết định thời gian mà dữ liệu được xem là cũ (stale) sau khi được lấy từ cache.

`staleTime` là khoảng thời gian (tính bằng milliseconds) trong đó dữ liệu từ cache được coi là tươi mới (fresh) và không cần phải được làm mới (refetch) từ server.

## Ví dụ

- Thông thường: sang màn detail screen -> call API detail 1 lần -> back to home -> detail screen ->  call API detail 2 lần.

- Sử dụng Cached response hay `staleTime`: sang màn detail -> call API detail 1 lần -> back to home -> detail screen ->  sử dụng lại API detail response trong 1 phút trước đó, sau 1 phút mới call lại.

Cách sử dụng Cached response hay `staleTime` giúp giảm bớt request tới API, tăng hiệu suất, giảm chi phí cho phần Backend.
