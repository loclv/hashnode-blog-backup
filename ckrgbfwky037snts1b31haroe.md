## Giới thiệu tổng quan về 🧪 SonarQube

### 🔥 Vài nét về `SonarQube`

[SonarQube](https://www.sonarqube.org/) là 1 nền tảng open-source đảm bảo chất lượng code được phát triển bởi công ty [SonarSource](https://en.wikipedia.org/wiki/SonarSource) bằng `Java`.

Phải nói thêm rằng tất cả các thành phần liên quan đến nền tảng này đều được opensource tại [đây](https://github.com/SonarSource). Còn [đây](https://github.com/SonarSource/sonarqube) là Repo source-code (src) của chính `SonarQube` trên  Github.

![sonarqube.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627042716614/3-XjZ9nuQ.png)

`SonarQube` được chạy tự động thường trong `CI/CD`, dựa trên kỹ thuật [Static program analysis](https://en.wikipedia.org/wiki/Static_program_analysis) - phân tích code mà không phải thực sự chạy code. Kỹ thuật này tương tự như các linter: `eslint`, `stylelint`, [pylint](http://pylint.pycqa.org/en/latest/)...

Tuy nhiên sự khác biệt ở đây là `SonarQube` có rules riêng focus vào tìm bugs, lỗ hổng bảo mật chứ không riêng gì các linter để đảm bảo chất lượng code. Hơn nữa nó có web và các công cụ để dễ dàng tích hợp với CI/CD hơn là các linter.

Ví dụ các rule dành cho TypeScripts được mô tả tại [đây](https://rules.sonarsource.com/typescript).

### 🌲 Các chỉ số cấu thành nên chất lượng code

- Reliability - độ tin cậy
- Security - bảo mật
- Maintainability ( Code Smells ) - khả năng bảo trì
- Coverage - độ phủ của `Unit test` (UT) hay code UT đã chạy qua bao nhiêu % lượng `src` và branches logic của dự án rồi.
- Duplications - mức độ lặp của code
- Size - dự án có khoảng bao nhiêu dòng

`SonarQube` cung cấp cho người quản lý 1 web để xem được các chỉ số và các đánh giá chi tiết về chât lượng.

### 👨‍💻 Development process

![sonar-dev-cycle.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627042744701/XkTcp1YnO.png)

1. Develop với editor cài [sonarlint](https://www.sonarlint.org/)
2. Khi push src lên repo thì builds src, runs unit tests và tích hợp với `SonarQube scanner` để cho ra báo cáo kết quả.
3. `SonarQube scanner` gửi kết quả đó về cho developers thông qua:


- web của SonarQube

- webhooks

- IDE notifications (thông qua SonarLint) - Ví dụ ta setup cho `SonarLint` trên vscode connect tới SonarQube >= 6.7 hoặc SonarCloud theo các bước tại [đây](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarlint-vscode) - phần `Connected mode`.

- công cụ quản lý src (ví dụ Bitbucket) thông qua pull/merge requests.

Sau đó quay về bước 1, vòng lặp được tiếp tục.

### 📚 Support Languages

Danh sách các ngôn ngữ được hỗ trợ được liệt kê tại [đây](https://docs.sonarqube.org/latest/analysis/languages/overview/).

SonarQube ngoài rules mà nó tự có thì ta có thể [import các linter - công cụ phân tích code của bên thứ 3](https://docs.sonarqube.org/latest/analysis/external-issues/) như [ESLint](https://eslint.org/), [pylint](http://pylint.pycqa.org/en/latest/), [golangci-lint](https://github.com/golangci/golangci-lint)...

Ví dụ đối với dự án Frontend thì có thể sử dụng:

- [JavaScript / TypeScript](https://docs.sonarqube.org/latest/analysis/languages/javascript/):
  - Dựa vào công cụ [SonarJS](https://github.com/SonarSource/SonarJS) để phân tích
    - Bao gồm [~250 rules for JavaScript](https://rules.sonarsource.com/javascript) và [~240 rules for TypeScript](https://rules.sonarsource.com/typescript)
  - Ngoài ra Sonar cũng có plugin dành cho `eslint`, được opensource tại [đây](https://github.com/SonarSource/eslint-plugin-sonarjs)
  - Ta có thể custom rule hay tạo ra rule của riêng mình theo các bước như khi custom rule của `eslint` tại [đây](https://eslint.org/docs/developer-guide/)
  - Đối với TypeScript ta cũng dùng thông qua [TypeScript ESLint](https://github.com/typescript-eslint/typescript-eslint)
  - Về cá rule riêng của các Framework thì ta thêm vào Sonar thông qua `eslint` ví dụ:
    - [Angular ESLint](https://github.com/angular-eslint/angular-eslint)
    - [ESLint-plugin-React](https://github.com/yannickcr/eslint-plugin-react)
    - [ESLint plugin for Vue.js](https://eslint.vuejs.org/)

- [CSS](https://docs.sonarqube.org/latest/analysis/languages/css/):
  - support CSS, SCSS, Less
  - support phần `style` trong PHP, HTML and `VueJS` (rất tiếc là trong docs chưa có nhắc tới `Angular` 😅)
  - Tuy nhiên, nếu dùng custom CSS Rules hay import [stylelint](https://stylelint.io/) ta phải disable rules mặc định này đi

- [HTML](https://docs.sonarqube.org/latest/analysis/languages/html/)

### 💫 CI/CD

Tương thích với các ứng dụng quản lý `src`:

- Bitbucket
- Github
- Azure DevOps
- GitLab

Ví dụ nếu tích hợp với `Bitbucket` thì ta có thể nhìn thấy báo cáo các chỉ số của 1 branch, cảnh báo đỏ hiện lên ngay bên cạnh `src` khi review 1 pull request.

Ví dụ hiển thị tên lỗi hay thông báo `Not covered by unit tests` khi hover vào vùng code có vấn đề:

![Screenshot from bitbucket.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627042783464/6wZUqJd5jE.png)

Pull requests `SonarQube Quality Gate` status:

![SonarQube Quality Gate status.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627042849702/IHUU-SqFf.png)

Ví dụ tích hợp với Pull Requests:

![branches.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627042868883/Dnvm5TQLE.png)

(ảnh công khai tại [SonarQube for visualstudio](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarqube) extention)

Khi review code, các comment của người review chưa được giải quyết thì `Quality Gate` failed:

![pull-request-decoration.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627042890416/SQLII1JsF.png)

(ảnh công khai tại [SonarQube for visualstudio](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarqube) extention)

Tương thích với các CI/CD platform/tool:

- Jenkins: [SonarScanners chạy trên Jenkins](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner-for-jenkins/) có thể tự động detect branches, Merge hoặc Pull Requests.
- Azure DevOps: [SonarScanner for Azure DevOps](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner-for-azure-devops/) được tích hợp trong build pipeline, gồm báo cáo trong bước build và `Quality Gate` sẽ có nhiệm vụ cho ra kết quả `Pass` hay `Fail`.

![azure-sonar-tasks.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627042906829/Lfj4mF2_T.png)

Ví dụ passing Quality Gate:

![sq-analysis-report-passed.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627042919977/0G7QL3Qs9.png)

Ví dụ failing Quality Gate:

![sq-analysis-report-failed.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627042927288/BdrDd_7cS.png)

- [Gradle](https://gradle.org/): dành cho Gradle task
- [Apache Maven](https://maven.apache.org/index.html)
- [Apache Ant](https://ant.apache.org/): Java library và command-line tool
- [MSBuild and Team Build](https://blog.sonarsource.com/announcing-sonarqube-integration-with-msbuild-and-team-build) dành cho .Net

Hỗ trợ [Webhooks](https://docs.sonarqube.org/latest/project-administration/webhooks/), nên ta cũng có thể bắn thông báo về kết quả build về công cụ chat chẳng hạn.

Hỗ trợ [web-api](https://docs.sonarqube.org/latest/extend/web-api/) để lấy thông tin thông qua API và [User token](https://docs.sonarqube.org/latest/user-guide/user-token/).

### 📖 [sonarlint](https://www.sonarlint.org/) - feedback ngay lập tức dựa trên extention của editor

Cũng giống như [eslint extenstion](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint), [sonarlint](https://www.sonarlint.org/) sẽ báo lỗi ngay trên editor bằng cách gạch chân đoạn code có vấn đề.

Sau đó người dùng có thể xem chi tiết lỗi đã vi phạm để biết nguyên nhân và khắc phục ngay.

Các editor được hỗ trợ:

- vscode: opensource tại [đây](https://github.com/SonarSource/sonarlint-vscode). Đây là [extention link](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarlint-vscode).
- IntelliJ: opensource tại [đây](https://github.com/SonarSource/sonarlint-intellij)
- eclipse: opensource tại [đây](https://github.com/SonarSource/sonarlint-eclipse)

![vscode-0.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627142457309/kgzsedE58.png)

![vscode-1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627142478974/jIzLhCQ_V.png)

---

Photo by <a href="https://unsplash.com/@ch49man?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Chapman Chow</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
