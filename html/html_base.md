# HTML

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>タイトル</title>
    <meta name="description" content="ページの説明・概要">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
  </head>
  <body>

    -- 要素 --

    <!-- コメント -->

    <script src="script.js"></script>
  </body>
</html>
```

<br>

## DOCTYPE宣言

```html
<!DOCTYPE html>
```

`HTML5`であることを宣言。

<br>

## 文字コード指定

```html
<meta charset="UTF-8">
```

文字コードの指定。

<br>

## タイトル

```html
<title>タイトル</title>
```

ページのタイトル。<br>
タグ内に記載された文字が、**ブラウザのタグ**・**検索結果**・**ブックマーク**などに表示される。

<br>

## ページ概要

```html
<meta name="description" content="ページ概要">
```

ページの概要を`content="〜"`に記載。<br>
**検索結果**に表示される。

<br>

## レスポンシブデザイン

```html
<meta name="niewport" content="width=device-width, initial-scale=1.0">
```

スマホ表示する際に使用。<br>
`content="〜"`で指定。

<br>

## CSS

```html
<link rel="stylesheet" href="style.css">
```

cssファイルを読み込む。<br>
`herf="〜"`にパスを指定。(相対・絶対どちらでも可)

<br>

## JavaScript

```html
<script src="script.js"></script>
```

JavaScriptファイルを読み込む。<br>
`src="〜"`にパスを指定。(相対・絶対どちらでも可)

scriptタグの記載位置は、`<head>`内でも可。

<details>

`<head>`内：bodyより前に読み込み<br>
`<body>`内：bodyの最後に読み込み

```js
// test.js
const p = document.getElementById('test');

console.log(p);
```

```html
<head>

  〜略〜

  <script src="test.js"></script>  <!-- nil -->
</head>
<body>
  <p id="test">test</p>

  <script src="test.js"></script> <!-- <p id="test">test</p> -->
</body>
```

</details>
