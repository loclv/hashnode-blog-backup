## VSCode extentions dành cho AWS - phần 1 - edit CloudFormation template YAML 🧘‍♀️

## [CloudFormation Linter](https://marketplace.visualstudio.com/items?itemName=kddejong.vscode-cfn-lint)

Khi mới bắt đầu edit [AWSTemplateFormat](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-formats.html) trên vscode, nếu bạn gặp lỗi do vscode báo chỗ `!Ref` là `unknow tag` trong file `AWSTemplateFormatVersion` yaml thì bạn hãy cài thêm [CloudFormation Linter](https://marketplace.visualstudio.com/items?itemName=kddejong.vscode-cfn-lint) extention đi nhé.
Đó là do bạn đang cài [redhat.vscode-yaml](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml) exention.
Mặt khác `redhat.vscode-yaml` cũng chính là 1 dependencies - cái xây dựng nên `CloudFormation Linter` extension.

Ta phải cài dependencies của extention này, không đơn gian chỉ là ấn install trên mục extensions của vscode đâu. Đầu tiên là [redhat.vscode-yaml](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml) extention.

Sau đó ta phải cài `python3` đã, sau đó cài `pip` và [cfn-lint](https://github.com/aws-cloudformation/cfn-lint):

```sh
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py

# test
pip --version
# if ok, delete unused `get-pip.py`
rm get-pip.py

# for lint
pip install cfn-lint

# for graph
pip install pydot
```

Đối với môi trường Ubuntu, mình đã thử cài và gặp vấn đề PIP package không tự động được thêm vào PATH nên trên vscode - file yaml vẫn hiển thị cảnh báo không tìm thấy `cfn-lint`. Đối với trường hợp này, có nhiều cách thêm `cfn-lint` vào PATH nhưng cách đơn giản nhất là dùng `sudo`:

```sh
sudo pip install cfn-lint
```

Vậy là ta có thể dựa vào `cfn-lint` để đọc và hiển thị các vấn đề về file template.

Còn 1 tính năng rất hay ho đó là render sơ đồ khối cấu trúc AWS mà CloudFormation này đang mô tả, thật sự hữu ích khi debug và rất trực quan. Để sử dụng ta cài `pip install pydot` như trên và:

- `ctrl` + `shift` + `P`
- gõ `cloud`
- chọn `Preview CloudFormation template as graph`

Kết quả là:

![graph](https://raw.githubusercontent.com/aws-cloudformation/cfn-lint-visual-studio-code/072292a6b4c0f8263a2204c07953692cfe25dee5/images/features.png)

![hair flip](https://media.giphy.com/media/8gUuSM6DgGLtYIBsOK/giphy.gif)

## [aws-cloudformation-yaml](https://marketplace.visualstudio.com/items?itemName=DanielThielking.aws-cloudformation-yaml)

`aws-cloudformation-yaml` cung cấp cho ta tính năng gõ tắt để gen ra 1 file template hoàn chỉnh, thêm vào nữa là khả năng gợi ý cú pháp cho `CloudFormation`.

Ví dụ ta gõ `!And` ta sẽ có gợi ý như sau:

![recommended](https://cdn.hashnode.com/res/hashnode/image/upload/v1631381538153/6lLMfrazg.png)

Extention này sẽ tự động thêm `Condition1` và `Condition2` cho bạn tương ứng với cú pháp của [AWS CloudFormation Fn::And](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-conditions.html#intrinsic-function-reference-conditions-and).

Danh sách hỗ trợ gợi ý cú pháp cho các [function](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html) bao gồm:

Functions có sẵn:

- !FindInMap
- !GetAtt
- !GetAZs
- !Cidr
- !ImportValue
- !Join
- !Select
- !Split
- !Sub
- !Ref

Condition Functions:

- !And
- !Equals
- !If
- !Not
- !Or

![like a boss](https://media.giphy.com/media/4QFAH0qZ0LQnIwVYKT/giphy.gif)

Vậy là ta đã có đủ bộ linter - check chính tả, review, gõ tắt cú pháp dành cho `CloudFormation`. 

## Tham khảo

- [stackoverflow - AWS SAM YAML template - Unknown Tag !Ref](https://stackoverflow.com/questions/53470329/aws-sam-yaml-template-unknown-tag-ref)

- [stackoverflow - Adding installed PIP package to path automatically](https://stackoverflow.com/questions/36092388/adding-installed-pip-package-to-path-automatically)

---

Photo by <a href="https://unsplash.com/@anniespratt?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Annie Spratt</a> on <a href="https://unsplash.com/s/photos/draw?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
