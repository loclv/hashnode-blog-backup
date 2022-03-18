## 🔥 Firebase push notification hay messaging - khi thay đổi Firebase project account những mã lỗi invalid token cũ có thể có

## Mở đầu

Từ token trong bài viết là chuỗi ký tự dài, unique dùng để định danh thiết bị cần notify/messaging.

Môi trường mình đã sử dụng để push notify/messaging là Node.js + [Firebase Admin Node.js SDK](https://github.com/firebase/firebase-admin-node) hay `firebase-admin` trên npm.

Việc thay đổi Firebase project account hay thay đổi private key sang 1 project khác của Firebase là điều không ai mong muốn.
Tuy nhiên nếu như phải làm và tự quản lý token trong DB, bạn sẽ gặp những lỗi invalid token, do token được sử dụng đó là của project cũ.
Vậy thì việc cần làm là xử lý xóa hoặc thay thế các token lỗi. Việc này dựa vào việc xác định các mã lỗi hay `error.code` cụ thể.

Những mã lỗi mình đã gặp có thể có là:

## `messaging/mismatched-credential`

```json
{
  code: "messaging/mismatched-credential",
  message: "SenderId mismatch"
}
```

Nó được đặc tả trong [firebase-admin-node/src/utils/error](https://github.com/firebase/firebase-admin-node/blob/HEAD/src/utils/error.ts) (thời điểm 2022/03):

```ts
  public static MISMATCHED_CREDENTIAL = {
    code: 'mismatched-credential',
    message: 'The credential used to authenticate this SDK does not have permission to send ' +
      'messages to the device corresponding to the provided registration token. Make sure the ' +
      'credential and registration token both belong to the same Firebase project.',
  };
```

Hoặc ta có thể xem code trên [github 1s](https://github1s.com/firebase/firebase-admin-node/blob/HEAD/src/utils/error.ts) cho tiện.

>Make sure the credential and registration token both belong to the same Firebase project.

Câu này cũng đã khẳng định mã lỗi này có thể rơi vào trường hợp thay đổi Firebase project.

## `messaging/registration-token-not-registered`

```json
{
  code: "messaging/registration-token-not-registered",
  message: "Requested entity was not found."
}
```

Nó được đặc tả trong [firebase-admin-node/src/utils/error](https://github.com/firebase/firebase-admin-node/blob/HEAD/src/utils/error.ts):

```ts
  public static REGISTRATION_TOKEN_NOT_REGISTERED = {
    code: 'registration-token-not-registered',
    message: 'The provided registration token is not registered. A previously valid registration ' +
      'token can be unregistered for a variety of reasons. See the error documentation for more ' +
      'details. Remove this registration token and stop using it to send messages.',
  };
```

>The provided registration token is not registered.

Nó chưa được đăng ký tức là có thể thuộc project cũ.

>Remove this registration token and stop using it to send messages.

Nhờ câu này ta cũng chắc chắn hơn về cách xử lý những token thế này.

![delete it!](https://media.giphy.com/media/WV4IUUYJmaSLkN26mx/giphy.gif)
