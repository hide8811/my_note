# Scss

- [変数($xxx: ---;)](#variable)
- [共通スタイルの定義(@mixin/@include)](#mixin)
- [ファイル分割(@import)](#partial)

<span id='variable'></span>
## 変数

```scss
$variable: #000;

.class_name {
  color: $variable;
}
```

<span id='mixin'></span>
## @mixin / @include

`@mixin`で共通するスタイルを定義し、`@include`で呼び出す。

```scss
@mixin style_name {
  color: #000;
}

.class_name {
  @include style_name;
  font-size: 1rem;
}
```

<span id='partial'></span>
## @import

ファイルを分割し、`@import`で読み込む。<br>
ファイル名にはアンダーバー(`_`)をつける。<br>
(アンダーバー(`_`)をつけたファイルは個別のCSSファイルとしては出力されないため、ページ読み込みが遅くならない。)

```bash
app
└── stylesheets
    │
    ├── application.scss
    │
    ├── _file.scss
    │
    ├── directory_A
    │   └── _file_a.scss
    │
    └── directory_B
        ├── _file_b.scss
        └── _file_c.scss
```
```scss
// app/stylesheets/application.scss

@import 'file.scss';
@import 'directory_A/file_a.scss';
@import 'directory_B/file_b.scss';
@import 'directory_B/file_c.scss';

// Rails gem 'sass-rails' 使用の場合
// glob が使用可能

@import 'directory_B/*';
```
