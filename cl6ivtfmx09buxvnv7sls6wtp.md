## Mind-map 🍁 cho nguyên tắc SOLID trong OOP dễ nhớ

Định nghĩa và ví dụ các bạn có thể tham khảo ở bài viết [
SOLID PRINCIPLES USING TYPESCRIPT](https://samueleresca.net/solid-principles-using-typescript/).

## Lý do cần mind-map 🍁

Thực ra nguyên tắc này trong OOP mình đã đọc từ lâu. Nhưng qua thời gian dài không động tới, mình lại không thể nhớ nổi các nguyên tắc này nội dung là gì!

Thế nên đây là lúc ta sử dụng mind-map để kết nối nó thành cách dễ nhớ hơn.

## Cơ sở của SOLID

SOLID giúp ta thực hiện nhuần nhuyễn, hiệu quả 4 tính chất của OOP:

- Abstraction - tính trừu tượng
- Encapsulation - tính đóng gói
- Inheritance - tính kế thừa
- Polymorphism - tính đa hình

Vì vậy có thể coi SOLID là 1 "phong cách coding" dành cho OOP.

## Mind-map 🍁

### 1 - Single Responsibility Principle - nguyên tắc chuyên biệt

SOLID, hay solid tiếng Anh ở đây tạm dịch là "vững chắc". Muốn "vững chắc" ta cần 1 tập hợp các class đơn lẻ có nhiệm vụ riêng.

>Nhất nghệ tinh nhất thân vinh.

Giống như trong xã hội, mỗi người 1 nhiệm vụ, nghề nghiệp, tiến tới chuyên nghiệp hóa thì mới có thể thành người tài ở 1 lĩnh vực nào đó.

mind-map 🍁:

Root: SOLID - "vững chắc"

-> mỗi thành viên/thành phần chịu trách nhiệm 1 nhiệm vụ duy nhất

-> nguyên tắc chuyên biệt Single Responsibility Principle.

### 2 - Open-closed Principle - nguyên tắc đóng mở

Để chuyên biệt hóa, không ôm đồm quá nhiều việc trong 1 class thì ta cần sử dụng tính kế thừa và đa hình. Như vậy ta "open" với việc "mở rộng" - extension, "closed" với sự "thay đổi" - modification.

mind-map 🍁:

Root: Nguyên tắc chuyên biệt

-> "open" với việc "mở rộng" - extension, "closed" với sự "thay đổi" - modification.

-> Open-closed Principle -  nguyên tắc đóng mở.

### 3 - Liskov Substitution Principle - Kiểu của con (ADN) luôn kế thừa từ cha

Giống như ADN - mã gen di truyền của cha con ở đây là type hay functionality - "chức năng".

mind-map 🍁:

Root: Sự "mở rộng" - extension hay kế thừa

-> Giữ lại mã gen di truyền ADN

-> Liskov Substitution Principle.

### 4 - Dependency inversion principle

High-level classes không nên phụ thuộc - dependency vào các thành phần cấp thấp, thay vào đó nên phụ thuộc vào các thành phần trìu tượng.

mind-map 🍁:

Root: Sự "mở rộng" - extension hay kế thừa

-> Khi sự kế thừa không hiệu quả bằng sự vay mượn từ các class khác

-> class này dùng đến tính năng của các class khác

-> ta bị phụ thuộc, hay class này bị phụ thuộc vào class khác

-> thay vì phụ thuộc duy nhất 1 class, ta phụ thuộc tập hợp các class có cùng tính năng đó

-> phụ thuộc vào sự trừu tượng - abstraction

-> Dependency inversion principle.

### Interface segregation principle - nguyên tắc phân tách interface

Các interface cần chuyên biệt hóa và được chia nhỏ ra để dễ quản lý. Hay các nhóm class cần được chia nhỏ. Các nhóm class này ta có thể hiểu là 1 interface - sự trừu tượng - abstraction. Việc phân nhóm tương đương với việc implements 1 interface.

mind-map 🍁:

Root: Sự trừu tượng sử dụng Abstract classes và interfaces

-> cần sử dụng đúng và đủ 1 interface khi mô tả 1 sự phụ thuộc của Dependency inversion principle.

-> cần chia nhỏ interface

-> phân tách interface - Interface segregation principle.
