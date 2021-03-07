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
render 'file_name'

# 別フォルダにあるときはパス
render 'directory_name/file_name'
```

### 変数を使う

```ruby
render partial: 'file_name', locals: { variable_name_1: 'value', variable_name_2: 'value', variable_name_3: 'value' }
```

### 繰り返し

`each`などで繰り返す代わりに使用できる。

【 ファイル名と変数名が同じとき 】

```ruby
render partial: 'example', collection: @examples
```

<br>

【 ファイル名と変数名が違うとき 】

```ruby
render partial: 'file_name', collection: @variable_names, as: 'variable_name'
```


<details>

**collection**: `controller`で定義した変数。<br>
**as**: 部分テンプレートファイル内で使用する変数。

```ruby
app
└── views
    └── users
        ├── index.html.erb
        └── _user.html.erb  # 部分テンプレート
```
```ruby
# models/user.rb
@users = User.all
```

<br>

ビューファイルの

```erb
<%= @users.each |user| do %>
  <%= user.name %>
  <%= user.birthday %>
<% end %>
```

を

```erb
-# _user.html.erb

<%= user.name %>
<%= user.birthday %>
```

```erb
-# index.html.erb

<%= render partial: 'user', collection: @users %>
```

にできる。<br>
`@variables.each |variable| do; end`が必要なくなくる。

<br>

`as`を省略できるときは、

- `collection`で指定した変数が、ファイル名の**複数形** (ディレクトリが違っても良い)
- ファイル内で使用している変数が、`collection`で指定した変数の**単数形**

</details>
