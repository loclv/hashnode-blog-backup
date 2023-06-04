---
title: "Tìm hiểu AWS job definition revision là gì"
datePublished: Sun Jun 04 2023 07:00:26 GMT+0000 (Coordinated Universal Time)
cuid: clih2q0nq000109mndlut81kr
slug: tim-hieu-aws-job-definition-revision-la-gi
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/sn87TQ_o7zs/upload/a557eaa64c720df20d1bcf583c559ad1.jpeg
tags: aws-vietnamese, aws-batch-vietnamese

---

## 👀 Kiến thức cần có trước khi đọc bài

* [AWS Batch](https://aws.amazon.com/batch/)
    
* Tại sao lại sử dụng AWS Batch?
    
* AWS job definition
    

## 👌 Hỏi chatGPT

Câu hỏi: `"revision" dịch là gì?`

> Từ "revision" có thể được hiểu là "sự đánh giá lại, sửa đổi" hoặc "phiên bản sửa đổi của một tài liệu hoặc sản phẩm"...

Câu hỏi: `aws job definition revision là gì?`.

### Câu trả lời của ChatGPT:

---

Trong Amazon Web Services (AWS), job definition là một tài nguyên quản lý công việc trong AWS Batch, giúp bạn định nghĩa và cấu hình các công việc để chạy trên Batch. Mỗi job definition bao gồm thông tin về container image, command line arguments, resource requirements và nhiều thuộc tính khác.

Các revisions của job definition là các phiên bản khác nhau của job definition, mỗi revision được đánh số thứ tự tăng dần. Khi bạn cập nhật job definition, AWS Batch sẽ tạo ra một phiên bản mới và giữ lại phiên bản cũ như một lịch sử. Việc sử dụng các revisions cho phép bạn theo dõi các thay đổi và khôi phục lại các phiên bản trước đó nếu cần thiết.

---

Vẫn chưa hiểu lắm đúng không ạ. 😂

## 😘 Tìm hiểu trên AWS docs - Google

Tìm kiếm trên Google với từ khóa "aws job definition revision", ta sẽ thấy link sau:

[https://docs.aws.amazon.com/batch/latest/userguide/job\_definition\_parameters.html](https://docs.aws.amazon.com/batch/latest/userguide/job_definition_parameters.html)

Tìm kiếm trong docs trên về "revision" ta sẽ thấy nội dung sau:

---

### **Job definition name**

`jobDefinitionName`

When you register a job definition, you specify a name. The name can be up to 128 characters in length. It can contain uppercase and lowercase letters, numbers, hyphens (-), and underscores (\_). The first job definition that's registered with that name is given a revision of 1. Any subsequent job definitions that are registered with that name are given an incremental revision number.

Type: String

Required: Yes

---

## 😎 Đọc hiểu và từ kinh nghiệm bản thân

Từ docs trên ta có thể hiểu rằng để giải quyết vấn đề nhiều phiên bản của 1 job mà trùng tên thì cần 1 thứ để định danh, đó chính là `revision`. 👏

Từ kinh nghiệm bản thân, trong quá trình development, việc fix, update code là thường xuyên. Như vậy khi 1 job được update vẫn với tên cũ thì cái thay đổi ở đây là `revision`.

Việc phải trỏ vào 1 revision cũ hay phiên bản cũ để revert code, cũng là ít khi xảy ra nên AWS khi trỏ tới 1 job definition sẽ mặc định là revision mới nhất được trỏ tới.

✅ Vậy là chúng ta đã hiểu kỹ hơn về khái niệm `aws job definition revision`.