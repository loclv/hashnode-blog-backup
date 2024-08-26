---
title: "E2E（End-to-End）テスト/Playwrightの紹介"
datePublished: Mon Aug 26 2024 02:27:11 GMT+0000 (Coordinated Universal Time)
cuid: cm0ado3p400000ajp8djkg5hq
slug: e2eend-to-endplaywright
tags: test-automation

---

## E2Eとは？

**E2E テスト (エンドツーエンド テスト)** は、アプリケーション全体をユーザーの視点からテスト手法するです。これは、システムの異なる部分（フロントエンド、バックエンド、データベースなど）、幼児データや機能E2E に正しく連携しているかどうかを検証し、ユール動作を模倣します。

## Playwrightとは？

Playwrightは、Microsoftによって開発されたオープンソースのE2Eテストフレームワークで、Webアプリケーションの自動テストを行うために使用されます。Playwrightは以下の特徴を持っています：

- クロスブラウザサポート: Playwrightは、Chromium、Firefox、WebKit（Safariのエンジン）など、複数のブラウザでテストを実行できます。

- ヘッドレスモード: ヘッドレスモードでテストを実行でき、リソースを節約しながら高速にテストを行えます。

- 自動化: ユーザーの操作（クリック、入力、ナビゲーションなど）をスクリプトで自動化し、繰り返しテストを行えます。

- 高度な機能: Playwrightは、ページ間の複雑なナビゲーション、ファイルのアップロード/ダウンロード、ネットワークのインターセプションなどの高度な機能をサポートしています。

以下は、Playwrightがブラウザと対話する様子をテキストで図示したものです。

```txt
+---------------------+         +---------------------------------+
|  Playwright Script  |         |            Browser              |
+---------------------+         +---------------------------------+
          |                                |
          | 1. Open Login Page             |
          +-------------------------------->
          |                                |
          | 2. Enter Username              |
          +-------------------------------->
          |                                |
          | 3. Enter Password              |
          +-------------------------------->
          |                                |
          | 4. Click Login Button          |
          +-------------------------------->
          |                                |
          | 5. Verify Login Success        |
          +-------------------------------->
          |                                |
          |        6. Return Result        |
          <--------------------------------+
          |                                |
+---------------------+         +---------------------------------+
```

このテキスト図では、左側に「Playwright Script」、右側に「Browser」があり、Playwrightがブラウザに対してログイン操作を順番に指示していく流れを示しています。

- Open Login Page: Playwrightがログインページを開く指示を出します。
- Enter Username: Playwrightがユーザー名を入力します。
- Enter Password: Playwrightがパスワードを入力します。
- Click Login Button: Playwrightがログインボタンをクリックします。
- Verify Login Success: Playwrightがログイン成功を確認します。
- Return Result: ブラウザが結果をPlaywrightに返します。

この順に、Playwrightがブラウザを操作し、E2Eテストを実行します。

以下は、Playwrightを使用したシンプルなE2Eテストの例です。このスクリプトは、Googleの検索ページを開き、検索を行い、結果を確認します。

```js
const { chromium } = require('playwright');

(async () => {
  // ブラウザを起動
  const browser = await chromium.launch();
  const page = await browser.newPage();
  
  // Googleのページを開く
  await page.goto('https://www.google.com');
  
  // 検索ボックスにテキストを入力し、Enterキーを押す
  await page.fill('input[name="q"]', 'Playwright E2E testing');
  await page.press('input[name="q"]', 'Enter');
  
  // 検索結果が表示されるのを待つ
  await page.waitForSelector('#search');
  
  // ブラウザを閉じる
  await browser.close();
})();

```

## 参照

- <https://playwright.dev/>
- chatGPT からのレビュー付きの回答
