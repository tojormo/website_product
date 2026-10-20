# とうじょう米 公式サイト

兵庫県・特A地区で育てる食用米ブランド「とうじょう米」の静的ウェブサイトです。
ヘッダー・フッターを共通化し、STORES（オンラインストア）のリンクを外部設定ファイルに集約しています。

## フォルダ構成

```
tojo-kome/
├── index.html          … トップページ
├── products.html       … 商品一覧
├── hinohikari.html     … ヒノヒカリ 商品ページ
├── konohoshi.html      … コノホシ 商品ページ
├── about.html          … 特A地区について
├── contact.html        … お問い合わせ
├── legal.html          … 利用規約・プライバシー・特商法表記
├── sitemap.xml         … サイトマップ（検索エンジン向け）
├── robots.txt          … クローラー向け設定（サイトマップの場所を通知）
├── css/
│   └── style.css       … スタイルシート（変更なし）
├── js/
│   ├── config.js       … ★STORESリンクの外部設定（ここだけ編集すればOK）
│   └── main.js         … 共通ヘッダー／フッター生成・リンク注入・挙動
└── images/             … 画像を配置（README.txt にファイル名一覧）
```

## STORESリンクの変更方法

`js/config.js` の値を書き換えるだけで、全ページ・全リンクに反映されます。

```js
window.SITE_CONFIG = {
  stores: {
    base: "https://tayui-kome.stores.jp/",          // ストアのトップ
    items: {
      hinohikari: "https://tayui-kome.stores.jp/items/hinohikari",
      konohoshi:  "https://tayui-kome.stores.jp/items/konohoshi"
    }
  }
};
```

## ヘッダー／フッターの編集方法

共通パーツは `js/main.js` が生成しています。文言やリンクを直す場合は main.js の1か所を編集すれば全ページに反映されます。
各HTML側はプレースホルダーを置くだけです。

```html
<div id="site-header" data-current="products" data-variant="solid"></div>
   ... 本文 ...
<div id="site-footer"></div>
<script src="js/config.js"></script>
<script src="js/main.js"></script>
```

- data-current … ナビの現在地ハイライト（home / products / about）
- data-variant … hero＝透過ヘッダー（トップ用）、省略時＝不透明固定（下層ページ用）
- data-image-note="false"（フッター）… 写真注記を非表示（公開版では全ページで指定済み）

## 公開方法

このフォルダ一式をそのままWebサーバーにアップロードしてください。
ヘッダー・フッターはJavaScriptで描画されるため、JavaScriptを有効にした状態でご利用ください。

## SEO設定について

- 各ページの `<head>` に canonical URL、OGP／Twitterカード、構造化データ（JSON-LD）を設定しています。
- 基準URLは `https://store.yamadanishiki.com/` です。ドメインを変更する場合は、各HTMLの canonical・og:url・og:image・JSON-LD、および `sitemap.xml`・`robots.txt` のURLをあわせて変更してください。
- SNSシェア用画像として `images/og-image.jpg`（推奨 1200×630px）を配置してください。
- ページを追加・更新した際は `sitemap.xml` の `<lastmod>` を更新し、Google Search Console からサイトマップを送信してください。
