# 制御構造

- [条件分岐](#conditional_branch)
    - [if](#if)
    - [unless](#unless)
    - [case](#case)

<br>

<span id='conditional_branch'></span>
## 条件分岐

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
条件式 if 処理(true) : 処理(false)
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
