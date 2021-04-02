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
# //
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

## オプション

### Ignorecase

大文字小文字を区別しない。

```ruby
# //
/pattern/i

# %r
%r(pattern)i

# new
Regexp.new('pattern', Regexp::IGNORECASE)
```

<details>

```ruby
/pattern/ === 'pattern'
# => true

/pattern/ === 'PATTERN'
# => false

/pattern/i === 'pattern'
# => true

/pattern/i === 'PATTERN'
# => true
```

</details>

### Multiline

`.`が、改行にもマッチ。

```ruby
# //
/pattern/m

# %r
%r(pattern)m

# new
Regexp.new('pattern', Regexp::MULTILINE)
```

<details>

```ruby
/00.00/ === "00\n00"
# => false

/00.00/m === "00\n00"
# => true
```

</details>

### Extended

パターン内の空白やコメントを無視する。

```ruby
# //
/pattern/x

# %r
%r(pattern)x

# new
Pregexp.new('pattern', Regexp::EXTENDED)
```

<details>

```ruby
/pattern  # comment
1234/ === 'pattern1234'
# => false

/pattern  # comment
1234/x === 'pattern1234'
# => true
```

</details>

## メタ文字

| 記号 | 意味 |
|:----:|:----:|
| [.](#dot) | 任意の一文字 |
| [[ ]](#square_brackets) |いずれか一文字 |
| [^](#caret) | 行頭 |
| [$](#dollar) | 行末 |
