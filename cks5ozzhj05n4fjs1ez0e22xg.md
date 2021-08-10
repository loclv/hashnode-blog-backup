## Cách dùng từ khóa 📖 `readonly` trong class, type, interface của TypeScript

## 🧐 Dùng như thế nào

Trong 1 `class`, `type` hoặc `interface`, nếu 1 thuộc tính không bao giờ thay đổi thì ta có thể sử dụng.

Khi 1 thuộc tính được đinh nghĩa là `readonly` và được gán lại bằng 1 giá trị khác thì ngay tại bước coding,
thì Compiler của TypeScript sẽ báo lỗi `không thể gán giá trị mới cho thuộc tính này`.

>error TS2540: Cannot assign to XXX because it is a constant or a read-only property.

Khi muốn khởi tạo giá trị cho thuộc tính này, thì ta có thể khởi tạo ở chỗ khai báo thuộc tính hoặc bên trong `constructor` của `class`.

Ví dụ trong 1 component có thuộc tính:

```ts
  public readonly columnTitles = columnTitles;
  public readonly cancelClicked = new EventEmitter<void>();
  public readonly nameMaxLength = nameMaxLength;
  public readonly role = this.authService.currentUserRole;
```

Ví dụ về khởi tạo giá trị trong `constructor` của `class`:

```ts
class Employee {
    readonly code: number;
    name: string;

    constructor(code: number, name: string)     {
        this.code = code;
        this.name = name;
    }
}

let emp = new Employee(10, "John");
emp.code = 20; // Compiler Error
emp.name = 'Bill';
```

Mã nhân viên `code` nếu thay đổi thì không thể định danh đó làm nhân viên nào được.

Ví dụ về thuộc tính `readonly` của `interface`:

```ts
interface IEmployee {
    readonly code: number;
    name: string;
}

let empObj: IEmployee = {
    code: 1,
    name: 'Steve';
}

empObj.code = 100; // Compiler Error: Cannot change readonly 'code'
```

Ví dụ về thuộc tính `readonly` của `type`:

```ts
// or `interface IEmployee`
type Employee = {
    empCode: number;
    empName: string;
}

let emp1: Readonly<Employee> = {
    empCode: 1,
    empName: 'Steve'
}

emp1.empCode = 100; // Compiler Error: Cannot change readonly 'empCode'
emp1.empName = 'Bill'; // Compiler Error: Cannot change readonly 'empName'

let emp2: Employee = {
    empCode: 1,
    empName: 'Steve'
}

emp2.empCode = 100; // OK
emp2.empName = 'Bill'; // OK
```

Chú ý là với cách tạo  `Readonly` với `type` như trên thì tất cả các thuộc tính của `type` đêu là `readonly`.

Như vậy có 3 cách tạo ra 1 object có thuộc tính `không được thay đổi` tính từ lúc giá trị của nó được khởi tạo.

## 🎯 Mục đích

Việc dùng `readonly` chỉ nhằm mục đích tránh những nhầm lẫn về logic, như việc đáng ra nó là biến không được thay đổi nhưng lại bị gán lại chẳng hạn.

Thế nên việc sử dụng là hoàn toàn tùy tâm, không dùng cũng chẳng sao. 😁

Chính bởi vậy nên tôi thấy trong dự án của mình, tôi thấy mọi người rất ít dùng. 😢

## 🧩 Tham khảo

- [tutorialsteacher typescript-readonly](https://www.tutorialsteacher.com/typescript/typescript-readonly)

---

Photo by <a href="https://unsplash.com/@romankraft?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Roman Kraft</a> on <a href="https://unsplash.com/s/photos/read?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
