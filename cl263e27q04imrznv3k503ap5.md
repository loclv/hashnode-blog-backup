## NodeJs - Update OpenSSL 💌 để vá lỗ hổng bảo mật

## Mở đầu

[OpenSSL](https://www.openssl.org/), ngắn gọn là giao thức mã hóa và bảo mật qua mạng, chống rò rỉ thông tin và xác định đối tượng truyền gói tin.

Trong các phiên bản, phổ biến nhất là *OpenSSL 1.1.1* hay *OpenSSL 1.1.1 Series*.

Ta có thể theo dõi thông tin cập nhập các bản vá lỗ hổng bảo mật tại [OpenSSL 1.1.1 Series Release Notes](https://www.openssl.org/news/openssl-1.1.1-notes.html).

Ví dụ từ OpenSSL 1.1.1m -> OpenSSL 1.1.1n sửa lỗi:

>Fixed a bug in the BN_mod_sqrt() function that can cause it to loop forever for non-prime moduli ([[CVE-2022-0778](https://www.openssl.org/news/vulnerabilities.html#CVE-2022-0778)])

Theo [OpenSSL Security Advisory [15 March 2022]](https://www.openssl.org/news/secadv/20220315.txt) thì đây được đánh giá là 1 lỗ hổng có độ nghiêm trọng cao.

## Các bước kiểm tra bản vá

Ví dụ ta muốn update lên *OpenSSL 1.1.1n* để vá lỗ hổng trên trên NodeJs. Phiên bản này release ngày 15/03/2022. Ta sẽ tiến hành theo các bước sau:

- Ta tiến hành kiểm tra [changelog của NodeJs](https://github.com/nodejs/node/tree/master/doc/changelogs). Chọn phiên bản đang sử dụng, ví dụ [v14 changelog](https://github.com/nodejs/node/blob/master/doc/changelogs/CHANGELOG_V14.md).
- Search từ khóa "OpenSSL".
- Ta thấy mục [2022-03-17, Version 14.19.1 'Fermium' (LTS), @richardlau](https://github.com/nodejs/node/blob/master/doc/changelogs/CHANGELOG_V14.md#2022-03-17-version-14191-fermium-lts-richardlau) có ghi "Update to OpenSSL 1.1.1n, which addresses the following vulnerability". Okey, đây đích thị là phần update *OpenSSL* rồi. Nó tương ứng với *Version 14.19.1*.
-  Công việc còn lại là update NodeJs lên Version 14.19.1 thôi.

Tham khảo [lịch releases + khoảng thời gian support](https://nodejs.org/en/about/releases/) các version lớn của NodeJs. Ví dụ thời điểm hiện tại các version có trạng thái *Maintenance* hoặc *Active* hoặc *Current* là 12, 14, 16, 18 mới có các bản vá về bảo mật như thế này.

## Update NodeJs version

### Môi trường local

Ở môi trường local ta có thể sử dụng [fnm - Fast and simple Node.js version manager, built in Rust](https://github.com/Schniz/fnm).

```sh
# check current version
node -v

fnm use v14.19.1
# Can't find an installed Node version matching v14.19.1.
# Do you want to install it? answer [y/n]: y
# Installing Node v14.19.1 (x64)
# Using Node v14.19.1

# check current version
node -v
# v14.19.1

# Set a version as the default version
fnm default v14.19.1
```

### Môi trường cloud

Đại diện cho các ECR - Amazon Elastic Container của NodeJs thì phổ biến được sử dụng, có lương download lớn nhất [Amazon ECR Public Gallery - NodeJs](https://gallery.ecr.aws/?searchTerm=node)  là [AWS ECR bitnami/node](https://gallery.ecr.aws/bitnami/node) được open source tại [github.com/bitnami/bitnami-docker-node](https://github.com/bitnami/bitnami-docker-node).  Lượng download lên tới hơn 2.5 triệu lượt tải.

Ta có thể xem [lịch sử commit của github/bitnami-docker-node/14/debian-10/Dockerfile](https://github.com/bitnami/bitnami-docker-node/commits/14.19.1-debian-10-r11/14/debian-10/Dockerfile), thì Dockerfile đã có phiên bản 14.19.1. Okey ta sẽ tiến hành update Dockerfile của mình:

```Dockerfile
FROM public.ecr.aws/bitnami/node:14.19.1
```

Bước cuối cùng là download thử image này trên local:

```sh
# Dockerfile.local is docker file name
docker build -t nodejs-14-local-image -f Dockerfile.local .
```

Ta thấy log của docker output ra rằng quá trình build không có lỗi. Vậy là xong!

## Tham khảo

- [vi.wikipedia OpenSSL](https://vi.wikipedia.org/wiki/OpenSSL)
