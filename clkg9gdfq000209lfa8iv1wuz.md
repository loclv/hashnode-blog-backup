---
title: "react-hook-form - Mô tả về onTouched mode"
datePublished: Mon Jul 24 2023 02:40:32 GMT+0000 (Coordinated Universal Time)
cuid: clkg9gdfq000209lfa8iv1wuz
slug: react-hook-form-mo-ta-ve-ontouched-mode
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/jLwVAUtLOAQ/upload/70595cae5cae9daa59297eddc29fffa2.jpeg
tags: react-vietnamese

---

## Vấn đề

Do mô tả ở [trang chủ react-hook-form về onTouched](https://www.react-hook-form.com/api/useform/#mode) khá dễ nhầm lẫn:

| Name | Type | Description |
| --- | --- | --- |
| onSubmit | string | Validation is triggered on the `submit` event, and inputs attach `onChange` event listeners to re-validate themselves. |
| onBlur | string | Validation is triggered on the `blur` event. |
| onChange | string | Validation is triggered on the `change`event for each input, leading to multiple re-renders. Warning: this often comes with a significant impact on performance. |
| onTouched | string | Validation is initially triggered on the first `blur` event. After that, it is triggered on every `change` event. |
| all | string | Validation is triggered on both `blur` and `change` events. |

Trong đó câu mô tả về onTouched:

> Validation is initially triggered on the first `blur` event. After that, it is triggered on every `change` event.

* Cho tới khi user blur ô input, thì mới trigger validation. Vậy thì trước đó input liên tục sẽ không trigger việc validation. Đây là điểm khác biệt với "onChange" mode.
    
* Change event ở đây nghĩa là change event nào? Đó là input hay blur event. Đây là điểm khó hiểu!
    

## Thực nghiệm

Kết qua là Change event ở đây nghĩa là cả 2 event onBlur và onChange, tức là mode all. Mô tả kỹ hơn về "onTouched":

* Ban đầu input - onChange diễn ra, nhưng không validate.
    
* Chỉ khi click sang phần tử khác trên màn hình - onBlur thì mới validate lần đầu.
    
* Kể từ thời điểm này, user input - onChange diễn ra, thì validate tương ứng (trái ngược với thời điểm ban đầu chưa có onBlur). Ngoài ra onBlur cũng validate.