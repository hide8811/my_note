# %記法

**文字列**、**コマンド出力**、**正規表現**、**配列**、**シンボル** を%で始まる形式で表記。

囲みには記号(`!`, `$`, `&`など)や括弧(`()`, `[]`, `{}`など)が使用可能。(英数字以外)

<br>

## %

ダブルクォート文字列 `"　"`

```ruby
%(hoge)  # => "hoge"

# 式展開 可
var = 'hoge'
%(#{var})  # => "hoge"
```

<br>

## %Q

ダブルクォート文字列 `"　"`

```ruby
%Q(hoge)  # => "hoge"

# 式展開 可
var = 'hoge'
%Q(#{var})  # => "hoge"
```

<br>

## %q

シングルクォート文字列 `'　'`

```ruby
%q(hoge)  # => "hoge"

# 式展開 不可
var = 'hoge'
%q(#{var})  # => "#{var}"
```

<br>

## %r

正規表現。

```ruby
%r(hoge)  # => /hoge/

# 式展開 可
var = 'hoge'
%r(#{var})  # => /hoge/
```

<br>

## %w

文字列の配列。(半角スペース区切り)<br>
式展開は不可。

```ruby
%w[hoge fuga piyo]  # => ["hoge", "fuga", "piyo"]

# 式展開 不可
var = 'hoge'
%w[#{var} fuga piyo]  # => ["\#{var}", "fuga", "piyo"]
```

<br>

## %W

文字列の配列。(半角スペース区切り)<br>
式展開は可。

```ruby
%W[hoge fuga piyo]  # => ["hoge", "fuga", "piyo"]

# 式展開 可
var = 'hoga'
%W[#{var} fuga piyo]  # => ["hoge", "fuga", "piyo"]
```
