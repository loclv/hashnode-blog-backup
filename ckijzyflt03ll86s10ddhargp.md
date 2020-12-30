## 多言語対応に関してAPIの設計 🛩

多言語対応に関して、相談したいです。

## HTTP ヘッダーについて

HTTP ヘッダーには、クライアントやサーバーが HTTP リクエストやレスポンスで追加情報を渡すことができます。
詳細情報は[こちら](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers)です。

多言語対応するため、共通方法があります。HTTP ヘッダーの「Accept-Language」と「Content-Language」値で設定できます。
「Accept-Language」と「Content-Language」の詳細情報は下記となります。

<https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Accept-Language>

> HTTP の Accept-Language リクエストヘッダーは、クライアントがどの言語を理解できるか、どの種類のロケールが推奨されるかを示します。 (言語というのは、英語のような自然言語を意味し、プログラミング言語ではありません。) コンテンツネゴシエーションを使用して、サーバーは提案されたものから一つを選択して使用し、 Content-Language レスポンスヘッダーを使用してクライアントに選択結果を知らせます。ブラウザーはユーザーインターフェイスの言語に従って、このヘッダーに適切な値を設定し、ユーザーはこれを変更することができますが、稀です (そして指紋につながるとして難色を示されます)。

<https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Content-Language>

> Content-Language は エンティティヘッダー で、ユーザが自分の好みの言語に応じて区別できるように、オーディエンス向けの言語を記述するために使用されます。

---

つまり、リクエストのヘッダー場合は、 「Accept-Language」を使用します。
レスポンスのヘッダー場合は、 「Content-Language」を使用します。

たとえば、

1. 「Accept-Language: ja」をリクエストのヘッダーに設定する
2. サーバーは日本語テキストを返却し、「Content-Language: ja」をレスポンスのヘッダーに設定する

英語(en)と中国語(zh)/中国語簡略化(zh-Hans)/中国語伝統的(zh-Hant)は同じです。

## メリット

### API設計：不要な値を省略する

・全部多言語データをレスポンスに渡す例：

```JSON
// 必要
"helloText": "おはよう",
// 不要
"helloTextEn": "hello",
// 不要
"helloTextZh": "你好",
```

-> 👌

```JSON
// header: Accept-Language: ja
"helloText": "おはよう",
```

API設計も省略できます。（それぞれAPIには「英語・中国語・・」キーが切り替える）

・パラメーターに設定不要になる

例：`get-data?lang=en&data-id=1`

-> 👌

```txt
// header: Accept-Language: en
get-data?data-id=1
```

### パフォーマンス

- 返却データ量を減らす(テキスト量による)
- バックエンドの処理を減らす(データベースに関する)
- フロントエンドの処理が減らす（if/elseで設定した言語あり・なしことを確認必要）

### 3言語以上対応の場合、便利になる

将来に3言語以上対応の場合、全部多言語データをレスポンスに渡す場合は無理になる

例：

```JSON
// 必要
"helloText": "おはよう",
// 不要
"helloTextEn": "hello",
// 不要
"helloTextZh": "你好",
...

// 不要
"helloTextVn": "xin chào",
```

---

多言語対応に関しては、HTTP ヘッダーの方法を検討してください。

画像のソース：

<https://unsplash.com/photos/jhtPCeQ2mMU>