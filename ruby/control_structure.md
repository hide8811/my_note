# 制御構造

- [条件分岐](#conditional_branch)
    - [if](#if)
    - [unless](#unless)
    - [case](#case)

<br>

<span id='conditional_branch'></span>
## 条件分岐

<span id='if'></span>
### if

条件式が`false`・`nil`以外のとき処理。

<details>

```ruby
'hoge' if true     # => "hoge"
'hoge' if 1        # => "hoge"
'hoge' if 0        # => "hoge"
'hoge' if 'fuga'   # => "hoge"
'hoge' if 'false'  # => "hoge"


'hoge' if false    # => nil
'hoge' if nil      # => nil
```

</details>

<br>

```ruby
if 条件式
  処理
  処理
end

# 処理が1行
処理 if 条件式
```

```ruby
# 分岐
if 条件式
  処理(true)
else
  処理(false)
end

# 同上
条件式 ? 処理(true) : 処理(false)
```

```ruby
# 分岐が複数
if 条件式[1]
  処理[1](true)
elsif 条件式[2]
  処理[2](true)
elsif 条件式[3]
  処理[3](true)
else
  処理(false)
end
```

<br>

<span id='unless'></span>
### unless

条件式が`false`・`nil`のとき処理。<br>
使用方法は`if`と同じ。<br>
三項演算子(` ? : `)・`elsif`はない。

<details>

```ruby
'hoge' unless false    # => "hoge"
'hoge' unless nil      # => "hoge"

'hoge' unless true     # => nil
'hoge' unless 1        # => nil
'hoge' unless 0        # => nil
'hoge' unless 'fuga'   # => nil
'hoge' unless 'false'  # => nil
```

</details>

<br>

```ruby
unless 条件式
  処理
  処理
end

# 処理が1行
条件式 unless 処理
```

```ruby
# 分岐
unless 条件式
  処理(false)
else
  処理(true)
end
```

<br>

<span id='case'></span>
### case

一つの式に対し、`===`で確認して条件分岐。<br>
`when`で比較項目、`else`でそれ以外。<br>
`when`の式に`*`をつけると、

<details>

[リファレンスマニュアル](https://docs.ruby-lang.org/ja/latest/method/Module/i/=3d=3d=3d.html)

等しいとき、サブクラスのインスタンスであるときに`true`。

```ruby
1 == 1         # true
1 === 1        # true

1 == '1'       # false
1 === '1'      # false

Integer == 1   # false
Integer === 1  # true

1 === Integer  # false
```
</details>

<br>

```ruby
case 式0
when 式1       # 式0 === 式1
  処理
when 式2, 式3  # 式0 === 式2 or 式0 === 式3
  処理
else           # それ以外
  処理
end
```

```ruby
ary = [1, 2, 3]

case 式
when ary    # [1, 2, 3] => 式 === [1, 2, 3]
  処理
when *ary   # 1, 2, 3 => 式 === 1 or 式 === 2 or 式 === 3
  処理
end
```

<details>
</details>
