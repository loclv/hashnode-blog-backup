---
title: "Lý do bạn nên dùng thử Supabase Auth service"
datePublished: Sun Nov 05 2023 08:47:25 GMT+0000 (Coordinated Universal Time)
cuid: clol8cs9j000109lbc35c28aa
slug: ly-do-ban-nen-dung-thu-supabase-auth-service
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/s8Y1LRd49Vk/upload/c4d9ecebfd5b5769ae9f6758096e4544.jpeg
tags: postgresql

---

## Làm quen với Supabase

[https://supabase.com/](https://supabase.com/) là gì?

Ta sẽ đến với định nghĩa từ docs:

\&gt;Supabase is a hosted platform which makes it very simple to get started without needing to manage any infrastructure.

Nó là 1 nền tảng lưu trữ, đơn giản hóa các công việc của developer, developer không cần quan tâm tới phần infra mà sẽ tập chung tối đa thời gian vào logic sản phẩm.

Tất nhiên nó có ưu và nhược điểm, nhưng đối với các startup luôn cần tối ưu hóa thời gian thì có thể đây là lựa chọn phù hợp.

Các tính năng chính:

* A dedicated [Postgres database](https://supabase.com/docs/guides/database)
    
* [Auto-generated APIs](https://supabase.com/docs/guides/database/api)
    
* [Auth and user management](https://supabase.com/docs/guides/auth)
    
* [Edge Functions](https://supabase.com/docs/guides/functions)
    
* [Realtime API](https://supabase.com/docs/guides/realtime)
    
* [Storage](https://supabase.com/docs/guides/storage)
    

Để ý rằng nếu như bạn muốn dùng MySQL hay NoSQL thì đây không phải lựa chọn cho bạn, vì Supabase chú trọng vào [Postgres database](https://supabase.com/docs/guides/database).

## Supabase Auth service giúp tiết kiệm thời gian ra sao?

Hỗ trợ nhiều bên cung cấp thứ 3 để giúp user login nhanh chóng như Google, Facebook...

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699172898751/3a53d314-0d88-4590-ab88-256072e8859e.png align="center")

Hỗ trợ Email Templates giúp Auth thông qua Email dễ dàng hơn.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699172920911/0c5b6459-0a02-44ae-b431-058f3f2a273f.png align="center")

Share Database dễ dàng với Team thông qua URL vì trong quá dình develop, ta có thể dùng remote DB thay vì chạy DB trên local.

\&gt;[Policies](https://www.postgresql.org/docs/current/sql-createpolicy.html) are PostgreSQL's rule engine

Không cần check như sau mỗi lần có request tới nữa:

```javascript
const loggedInUserId = 'd0714948'
const { data, error } = await supabase
  .from('users')
  .select('user_id, name')
  .eq('user_id', loggedInUserId)

// console.log(data)
// => { id: 'd0714948', name: 'Jane' }
```

Đơn giản chỉ cần định nghĩa rule trong tables: `auth.uid() = user_id` thì công việc check quyền hạn mỗi user sẽ được đẩy về phía DB.

## Giá cả phù hợp startup

Vì gói Free của Supabase đủ dùng cho 1 khởi đầu đơn giản. Thông tin thêm tại [https://supabase.com/pricing](https://supabase.com/pricing).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699173271888/3896b0ee-980e-42f8-99a6-8e286c262f81.png align="center")

Auth service không giới hạn số lượng user:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699173358642/ae413f7a-52af-4879-a180-e97b3ee41db7.png align="center")

## Supabase là dự án hoàn toàn Opensource

[https://github.com/supabase](https://github.com/supabase)

Do vậy nên cộng đồng hỗ trợ đông đảo.