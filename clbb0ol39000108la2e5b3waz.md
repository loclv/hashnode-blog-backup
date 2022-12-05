# Cài nhanh Gradle để khởi tạo dự án Java trên Windows

## Tiền đề

Khi khởi tạo dự án với Java, Gradle là 1 build tool có thể thay thế được Maven, vì nó build nhanh hơn và có UI UX thân thiện hơn Maven. Hơn nữa bản thân Gradle được chạy trên chính JVM.

Vấn đề với môi trường Windows development là [gradle install steps](https://gradle.org/install/) dành cho Windows khá loằng ngằng tốn thời gian. Dưới đây là cách install với [Windows chocolatey](https://chocolatey.org/).

> Chocolatey is software management automation for Windows that wraps installers, executables, zips, and scripts into compiled packages.

Chocolatey tương tự như [HomeBrew](https://brew.sh/) của macOS, giúp ta quản lý, cài đặt các package 1 cách nhanh chóng.

## Install Gradle

Ta sử dụng [microsoft/termina](https://github.com/microsoft/terminal):

```shell
sudo choco install gradle
gradle --version
# output: Gradle 7.5.1

# init a Java project
mkdir gradle-demo
cd .\gradle-demo\
gradle init
```

```txt
Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin
Enter selection (default: basic) [1..4] 2

Select implementation language:
  1: C++
  2: Groovy
  3: Java
  4: Kotlin
  5: Scala
  6: Swift
Enter selection (default: Java) [1..6] 3

Split functionality across multiple subprojects?:
  1: no - only one application project
  2: yes - application and library projects
Enter selection (default: no - only one application project) [1..2] 1

Select build script DSL:
  1: Groovy
  2: Kotlin
Enter selection (default: Groovy) [1..2] 1

Generate build using new APIs and behavior (some features may change in the next minor release)? (default: no) [yes, no]
yes

Select test framework:
  1: JUnit 4
  2: TestNG
  3: Spock
  4: JUnit Jupiter
Enter selection (default: JUnit Jupiter) [1..4] 1

Project name (default: gradle-demo): demo
Source package (default: demo):

> Task :init
Get more help with your project: https://docs.gradle.org/7.5.1/samples/sample_building_java_applications.html

BUILD SUCCESSFUL in 1m 27s
2 actionable tasks: 2 executed
```

```shell
 code .
 ./gradlew run
```

` ./gradlew run` output:

```txt
> Task :app:run
Hello World!

BUILD SUCCESSFUL in 3s
2 actionable tasks: 2 executed
```

Vậy là ta đã có 1 dự án Java với Gradle trên Windows 1 cách nhanh chóng.
