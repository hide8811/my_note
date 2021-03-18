# model

## scope
[Railsガイド](https://railsguides.jp/active_record_querying.html#%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%97)

<br>

モデルへのメソッド(where, includes, orderなど)を定義することができる。

```ruby
# models/class_name.rb
class ClassName < ApplicationRecord
  scope :scope_name, -> { method }
end
```

### 特徴

- 返り値はActiveRecord::Relationオブジェクトを返す。
- 条件式が`nil`や`false`の場合、`.all`と同じで全てのデータが返る。


### クラスメソッドとの違い
- 基本、どちらでも良い
- 条件式が`nil`の場合
    - スコープ => 全てのデータが返る(`.all`と同じ) => メソッドチェイン時、<span style="border-bottom: 1px crimson solid">エラーが出ない</span>
    - クラスメソッド => nilが返る => メソッドチェイン時、<span style="border-bottom: 1px crimson solid">エラーが出る</span>
- 引数がある場合、クラスメソッド推奨
