# 正規表現
[リファレンスマニュアル](https://docs.ruby-lang.org/ja/latest/doc/spec=2fregexp.html)

## Regexpクラス

- スラッシュ(`/`)で囲む。
```ruby
/pattern/
```

- %記法(`%r()`)を使用。(`/`がそのまま使用可能)
```ruby
%r(pattern)
```

- `new`メソッドを使用。
```ruby
Regexp.new('pattern')
```

<details>

```ruby
# / /
/https:\/\/www.google.com/
# => /https:\/\/www.google.com/

# %r
%r(https://www.google.com)
# => /https:\/\/www.google.com/

# new
Regexp.new('https://www.google.com')
# => /https:\/\/www.google.com/
```

</details>

## メタ文字

| 記号 | 意味 |
|:----:|:----:|
| [.](#dot) | 任意の一文字 |
| [[ ]](#square_brackets) |いずれか一文字 |
| [^](#caret) | 行頭 |
| [$](#dollar) | 行末 |
