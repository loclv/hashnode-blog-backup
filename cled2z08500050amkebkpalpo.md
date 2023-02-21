# Angular - Khi nào dùng ngIf và hidden với ví dụ

Mặc dù nhiều bạn đã biết công dụng của chúng đều giúp ta ẩn hiện 1 element, tuy nhiên ta phải hiểu về bản chất để sử dụng sao cho tối ưu về hiệu năng.

Đối tượng ẩn hiện thường là đơn giản, ví dụ như chỉ là 1 element để hiển thị text thì trải nghiệm user sẽ không có gì khác nhau. Tuy nhiên, 1 số ít trường hợp ẩn hiện với component lớn, phức tạp thì ta mới thấy sự khác biệt phía user.

## 🌱 Cơ bản về ngIf và hidden

Ôn lại kiến thức cơ bản chút thì ta phải hiểu [https://www.w3schools.com/js/js\_htmldom.asp](https://www.w3schools.com/js/js_htmldom.asp) - The HTML DOM Tree of Objects:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676908276680/ee0c9d60-3ab4-4fce-8e87-5d42643fe37a.gif align="center")

(Ảnh từ [https://www.w3schools.com/js/js\_htmldom.asp](https://www.w3schools.com/js/js_htmldom.asp))

JavaScript thông qua DOM Tree of Objects (hay gọi tắt là DOM Tree) có thể tương tác với UI.

Như vậy có 2 cách để ẩn 1 thành phần (Element hay node) trên UI:

* Loại bỏ 1 node (1 lá) khỏi DOM Tree - tương ứng cách hoạt động của `ngIf`.
    
* Không loại bỏ hẳn mà chỉ dùng style - CSS để ẩn nó đi - tương ứng cách hoạt động của `hidden`.
    

Như vậy ta đã hiểu cơ bản logic hoạt động của `ngIf` và `hidden`.

## 🥦 Vậy thì khi nào nên dùng ngIf và hidden?

Đối với `ngIf`, việc loại bỏ hẳn rồi lại gắn lại vào DOM Tree với tần suất "nhiều" thì tất nhiên "Tree" sẽ phải làm nhiều việc bao gồm:

* Sắp xếp lại các node trên UI tương ứng với Tree vì DOM tree sẽ thay đổi khi điều kiện nằm trong `ngIf` được kích hoạt.
    
* Hiển thị tương ứng với style - CSS đang ảnh hưởng tới node (lá).
    

Đối với `hidden` thì chỉ sử dụng style (css) để ẩn hiện, còn DOM tree không thay đổi. Như vậy, đối với `hidden`, việc ẩn hiện với tần suất "nhiều" thì ít việc cần làm hơn, hay hiệu quả hơn vì không phải render đi, render lại trong DOM Tree mà việc render đã được thực hiện ngay từ đầu khi khởi tạo template (hay UI). Tần suất ẩn hiện nhiều hoặc liên tục thì `hidden` càng đem lại hiêu năng tốt hơn.

Tuy nhiên, nhược điểm của `hidden` là phải render ra DOM Tree ngay từ đầu và trong suốt vòng đời của component rồi. Điều này dẫn tới việc:

* Phải tốn bộ nhớ, mặc dù rất nhỏ để lưu vào DOM Tree phần node này, mặc dù node không được hiển thị.
    
* Mất công sắp xếp các node trên UI mặc dù không hiển thị.
    

Như vậy `hidden` không hiệu quả khi tần suất hiển thị node "ít" hoặc không hiển thị luôn.

Tóm lại:

* Ẩn hiện với tần suất "nhiều" thì nên dùng `hidden`.
    
* Ẩn hiện với tần suất "ít" thì nên dùng `ngIf`.
    

Ngoài ra, việc dùng `hidden` cũng tiện hơn `display: none;` (CSS) vì tương tác với logic ngắn gọn hơn. Output thực sự của `ngIf`, `hidden` và `display: none;` ta có thể xem cụ thể tại: [https://www.angularjswiki.com/angular/difference-between-ngif-and-hidden-or-displaynone-in-angular/](https://www.angularjswiki.com/angular/difference-between-ngif-and-hidden-or-displaynone-in-angular/).

Tất nhiên là khi nào chủ đích muốn loại bỏ hẳn element trong DOM tree thì ta phải dùng `ngIf`.

## 🍌 Ví dụ

Nếu là điều kiện biến environment thì dùng `ngIf` vì nó không thể ẩn / hiện trong suốt quá trình sử dụng hay life cycle của component. Ví dụ tính năng A được enabled:

```xml
<div *ngIf="isThisFeatureEnabled">This will be added to DOM by ngIf</div>
```

Khi phân quyền:

```xml
<div *ngIf="role === Role.Admin">This will be added to DOM by ngIf</div>
```

Khi không phải là Admin, DOM tree nhẹ hơn vì không chứa element. Như vậy nếu trong suốt quá trình sử dụng, không cần ẩn / hiện thì `ngIf` có hiệu năng tốt hơn.

Còn `hidden` chỉ dùng khi chuyện ẩn / hiện là chuyện xảy ra bình thường trong quá trình dùng. Ví dụ loading overlay hiển thị mỗi khi call API:

```xml
<div [hidden]="!isLoading" class="loading-overlay"></div>
```

Một ví dụ khác về tần suất sử dụng bật tắt lại phụ thuộc vào thói quen người dùng:

```xml
<div [hidden]="!isUserLikeThis" class="love-icon">😍</div>
```

Nếu số lượng người dùng có thói quen "thả tim" - 😍 nhiều thì dùng `hidden`, ngược lại có thể dùng `ngIf`. Quyết định chỗ này tùy thuộc vào chúng ta!