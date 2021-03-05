# 部分テンプレート

ビューの一部を別ファイルに記述し、使い回すことができる。<br>
[Railsガイド](#https://railsguides.jp/layouts_and_rendering.html#パーシャルを使用する)

## ファイル名

ファイル名の前にアンダーバー(`_`)をつける。

<span style='color: crimson;'>**_**</span><ファイル名>

```ruby
app
└── views
    └── users
        ├── index.html.erb
        ├── new.html.erb
        └── _form.html.erb  # 部分テンプレート
```

## 呼び出し

`render`を使用し、viewファイル内に記載。<br>

- 呼び出しの際のファイル名にはアンダーバー(`_`)はつけない<br>
- ファイル名の拡張子は不要。

```ruby
render '<ファイル名>'

# 別フォルダにあるときはパス
render '<ディレクトリ>/<ファイル名>'
```

### 変数を使う

```ruby
render partial: '<ファイル名>', locals: { <変数名>: '<値>', <変数名>: '<値>', <変数名>: '<値>' }
```
