## dependency injection - phần 1 - giải thích căn cơ

Photo by [finnysz](https://unsplash.com/@finnysz) on [unsplash](https://unsplash.com/photos/ONjUYQ8CMnY)

Bài viết tham khảo từ bài viết [này](https://www.smashingmagazine.com/2020/12/practical-introduction-dependency-injection/) của [jamie-corkhill](https://www.smashingmagazine.com/author/jamie-corkhill/) - developer chỉ mới 18 tuổi.

## Giải thích căn cơ

`Dependency injection` hay gọi tắt ở nhiều nơi là `DI`, là 1 khái niệm về cách viết / thiết kế source code.

Dịch tiếng Anh thì `Dependency` là `phụ thuộc`, còn `injection` là `sự tiêm vào`.

Vậy thì cái gì phụ thuộc và cái gì được tiêm vào!?

### Ví dụ đơn giản trong thực tế

Hít 1 hơi thật sâu và tưởng tượng bạn đang ở trong nhà máy lắp ráp Ô-tô, xe máy đi. 🤔

Để so sánh, ta cùng xem đoạn code (typescript) dưới đây không phải là `DI`:

```typescript
import { Engine } from './Engine';

class Car {
    private engine: Engine;

    constructor () {
        this.engine = new Engine();
    }

    startEngine(): void {
        this.engine.fireCylinders();
    }
}
```

Còn đây mới là `DI`:

```typescript
import { Engine } from './Engine';

class Car {
    private engine: Engine;

    constructor (engine: Engine) {
        this.engine = engine;
    }

    startEngine(): void {
        this.engine.fireCylinders();
    }
}
```

Bạn có thấy chỗ khác nhau không nhỉ?

OK, bắt đầu từ câu chuyện thực tế rằng ta phải chế tạo 1 chiếc xe và sử dụng nó.

Cách làm thứ nhất là `Car` tự quyết định sẽ sử dụng `Engine` cho tính năng `startEngine` của nó.

Với cách làm này, tất nhiên là `Car` sẽ chạy. Tuy nhiên, câu hỏi ở đây là:

> Nếu nhà máy không tự sản xuất được động cơ `Engine` hoặc là mua của 1 nhà cung cấp `Engine` khác cho rẻ và tốt?

<iframe src="https://giphy.com/embed/a5viI92PAF89q" width="480" height="331" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/reaction-a5viI92PAF89q">via GIPHY</a></p>

Câu chuyện giống với cách mà hầu hết nhà máy cũng như sản phẩm được tạo ra. Câu chuyện mà năm 2020 cũng được nhắc tới nhiều, đó là sản phẩm được tạo ra bao nhiêu phần trăm ở Việt Nam thì mới được coi là `Made in Vietnam` đúng không?!

Giải pháp là `Dependency injection`! `Dependency` ở đây là sự phụ thuộc của `Car` vào `Engine`, còn `injection` là bất cứ `engine` nào theo đúng kiểu (type) `Engine` cũng có thể được `tiêm` vào `Car`.

Thời điểm `injection` thích hợp nhất tất nhiên là lúc còn đang lắp ráp `Car` đúng không? Mở banh 1 `Car` để thay thế phụ tùng / engine bao giờ cũng khó khắn hơn lúc lắp ráp. Chưa kể 1 số không thể thay thế phụ kiện như Macbook đời mới chẳng hạn. Thế nên, tương đương với điều đó là `engine` sẽ được gán vào trong `constructor` - lúc khởi tạo / lắp ráp.

Đôi với typescript thì cũng có thể viết tắt phần `constructor` thành:

```typescript
constructor (private engine: Engine) {}
```

## Mục đích

<iframe src="https://giphy.com/embed/cPKWZB2aaB3rO" width="480" height="408" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/cPKWZB2aaB3rO">via GIPHY</a></p>

Ở ngoài đời thì `DI` có vai trò tạo ra chuỗi cung ứng, còn trong programming thì sao? Hầu hết các trường hợp là để viết Test. Bản thân mình cho đến bây giờ cũng chỉ dùng nó để test.

Để bài viết sau mình viết rõ về mục đích của nó nhé! Sẽ update link ở đây.
