---
title: "bunx wpress-extract を使って WordPress の .wpress バックアップを展開する方法"
seoTitle: "bunx wpress-extract を使って WordPress の .wpress バックアップを展開する方法"
seoDescription: "bunx wpress-extract を使って WordPress の .wpress バックアップを展開する方法"
datePublished: Sun May 04 2025 10:32:56 GMT+0000 (Coordinated Universal Time)
cuid: cma9ijlhc000y09jrbd4u8ao3
slug: bunx-wpress-extract-wordpress-wpress
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/ANICl9V7BUA/upload/4b892878ee3493e9990f06f7479cfcb8.jpeg
tags: wordpress

---

以下は、WordPress の `.wpress` バックアップファイルを `bunx wpress-extract` を使って展開する方法について解説した日本語ブログ記事です。

---

# `bunx wpress-extract` を使って WordPress の .wpress バックアップを展開する方法

## はじめに

**All-in-One WP Migration** プラグインを使って WordPress サイトをバックアップすると、`.wpress` という拡張子のファイルが作成されます。この `.wpress` ファイルは独自形式で圧縮されているため、通常の解凍ソフト（WinRAR や 7-Zip など）では中身を取り出すことができません。

この記事では、コマンドラインツール `wpress-extract` を `bunx` 経由で使って、`.wpress` ファイルを展開する手順を解説します。

---

## 必要なもの

開始する前に以下を準備してください：

* Node.js と [Bun](https://bun.sh/) がインストールされた環境
    
* All-in-One WP Migration によって作成された `.wpress` バックアップファイル
    

まだ Bun をインストールしていない場合は、以下のコマンドで導入可能です：

```bash
curl -fsSL https://bun.sh/install | bash
```

---

## ステップ 1：`bunx` で `wpress-extract` を実行

npm や yarn でグローバルにインストールする必要はなく、`bunx` を使えば即座に実行できます：

```bash
bunx wpress-extract ./backup-file.wpress
```

`./backup-file.wpress` は展開したい `.wpress` ファイルのパスです。

### オプション：出力先を指定

出力フォルダを指定するには `--output` オプションを使用します：

```bash
bunx wpress-extract ./backup-file.wpress --output ./output-folder
```

---

## ステップ 2：展開されたファイルを確認

コマンドの実行後、指定したフォルダに以下のような内容が展開されます：

* **wp-content**：プラグイン、テーマ、アップロード画像など
    
* **database.sql**：WordPress サイトのデータベース内容
    
* その他の WordPress 関連ファイル
    

---

## `wpress-extract` はどんなときに便利？

* サイト全体を復元せず、一部のファイル（例：画像やテーマ）だけを取り出したいとき
    
* 開発環境でデータを取り出して個別に確認したいとき
    
* `.wpress` ファイルのインポートに失敗したが、どうしても中身を取り出したいとき
    

---

## 注意点

* `.wpress` ファイルはサイズが非常に大きい場合があります（数 GB 以上）
    
* 解凍にはディスク容量と時間がかかる場合があるので注意
    
* `wpress-extract` は「復元」ツールではなく「抽出」ツールです（復元は手動で行う必要があります）
    

---

## まとめ

`bunx wpress-extract` を使えば、All-in-One WP Migration の `.wpress` バックアップファイルから中身を簡単に抽出することができます。これは、開発者や技術的なユーザー、または部分的にデータを取り出したいユーザーにとって非常に便利なツールです。

---