# %記法

**文字列**、**コマンド出力**、**正規表現**、**配列**、**シンボル** を%で始まる形式で表記。

囲みには記号(`!`, `$`, `&`など)や括弧(`()`, `[]`, `{}`など)が使用可能。(英数字以外)

- [**%** 《ダブルクォート文字列》](#double_quotes_string)
- [**%Q** 《ダブルクォート文字列》](#q_double_quotes_string)
- [**%q** 《シングルクォート文字列》](#single_quotes_string)
- [**%s** 《シンボル》](#symbol)
- [**%r** 《正規表現》](#regexp)
- [**%w** 《配列(文字列・式展開 不可)》](#array_string)
- [**%W** 《配列(文字列・式展開 可)》](#array_string_expansion)
- [**%i** 《配列(シンボル・式展開 不可)》](#array_symbol)
- [**%I** 《配列(シンボル・式展開 可)》](#array_symbol_expansion)

<br>

<span id='double_quotes_string'></span>
## %

ダブルクォート文字列。`"　"`

```ruby
%(hoge)  # => "hoge"

# 式展開 可
var = 'hoge'
%(#{var})  # => "hoge"
```

<br>

<span id='q_double_quotes_string'></span>
## %Q

ダブルクォート文字列。`"　"`

```ruby
%Q(hoge)  # => "hoge"

# 式展開 可
var = 'hoge'
%Q(#{var})  # => "hoge"
```

<br>

<span id='single_quotes_string'></span>
## %q

シングルクォート文字列。`'　'`

```ruby
%q(hoge)  # => "hoge"

# 式展開 不可
var = 'hoge'
%q(#{var})  # => "#{var}"
```

<br>

<span id='symbol'></span>
## %s

シンボル。`:　`<br>
式展開は不可。

```ruby
%s(hoge)  # => :hoge

# 式展開 不可
var = 'hoge'
%s(#{var})  # => :"\#{var}"
```

<span id='regexp'></span>
## %r

正規表現。`/　/`

```ruby
%r(hoge)  # => /hoge/

# 式展開 可
var = 'hoge'
%r(#{var})  # => /hoge/
```

<br>

<span id='array_string'></span>
## %w

文字列の配列。(半角スペース区切り) `["　"]`<br>
式展開は不可。

```ruby
%w[hoge fuga piyo]  # => ["hoge", "fuga", "piyo"]

# 式展開 不可
var = 'hoge'
%w[#{var} fuga piyo]  # => ["\#{var}", "fuga", "piyo"]
```

<br>

<span id='array_string_expansion'></span>
## %W

文字列の配列。(半角スペース区切り) `["　"] #{　}`<br>
式展開は可。

```ruby
%W[hoge fuga piyo]  # => ["hoge", "fuga", "piyo"]

# 式展開 可
var = 'hoga'
%W[#{var} fuga piyo]  # => ["hoge", "fuga", "piyo"]
```

<br>

<span id='array_symbol'></span>
## %i

シンボルの配列。(半角スペース区切り) `[:　]`<br>
式展開は不可。

```ruby
%i[hoge fuga piyo]  # => [:hoge, :fuga, :piyo]

# 式展開 不可
var = 'hoge'
%i[#{var} fuga piyo]  # => [:"\#{var}", :fuga, :piyo]
```

<span id='array_symbol_expansion'></span>
## %I

シンボルの配列。(半角スペース区切り) `[:　] #{　}`<br>
式展開は可。

```ruby
%I[hoge fuga piyo]  # => [:hoge, :fuga, :piyo]

# 式展開 可
var = 'hoge'
%I[#{var} fuga piyo]  # => [:hoge, :fuga, :piyo]
```
