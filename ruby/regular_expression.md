# 正規表現
[リファレンスマニュアル](https://docs.ruby-lang.org/ja/latest/doc/spec=2fregexp.html)

- [オプション](#option)
    - [**(?on) (?-off)** 《部分正規表現》](#part)
    - [**i** 《大文字小文字無視》](#ignorecase)
    - [**m** 《`.`の改行マッチ》](#multiline)
    - [**x** 《空白・コメント無視》](#extended)
    - [**o** 《式展開初回のみ》](#o_option)
- [メタ文字](#meta_character)
    - [文字](#character)
        - [**.** 《任意の1文字》](#dot)
        - [**[　]** 《いずれか1文字》](#square_brackets)
            - [**[^　]** 《以外の一文字》](#denial_square_brackets)
            - [**[　-　]** 《連続する範囲》](#range_square_brackets)
        - [**\w** 《英数アンダーバー》](#alphanumeric)
        - [**\W** 《英数アンダーバー以外》](#non_alphanumeric)
        - [**\d** 《数字》](#number)
        - [**\D** 《数字以外》](#non_number)
        - [**\s** 《空白文字》](#blank_character)
        - [**\S** 《空白文字以外》](#non_blank_characther)
    - [アンカー](#anchor)
        - [**^** 《行頭》](#caret)
        - [**$** 《行末》](#dollar)
        - [**\A** 《文字列の先頭》](#string_first)
        - [**\Z** 《文字列の末尾》](#string_last)
        - [**\z** 《文字列の末尾 改行含む》](#string_last_linefeed)
        - [**\b** 《単語の境界》](#boundary)
        - [**\B** 《単語の境界以外》](#non_boundary)
    - [先読み・後読み](#look)
        - [**(?=　)** 《肯定先読み》](#positive_lookahead)
        - [**(?!　)** 《否定先読み》](#negative_lookahead)
        - [**(?\<=　)** 《肯定後読み》](#positive_lookbehind)
        - [**(?\<!　)**  《否定後読み》](#negative_lookbehind)
    - [繰り返し](#repeat)
        - [**\*** 《0回以上》](#zero_times)
        - [**+** 《1回以上》](#one_times)
        - [**?** 《0 or 1回》](#zero_or_one)
        - [**{n}** 《n回》](#n_times)
        - [**{min,}** 《min回以上》](#min)
        - [**{,max}** 《max回以下》](#max)
        - [**{min, max}** 《min回以上、max回以下》](#min_max)
        - [**\*?** 《最小量指定子》](#reluctant_quantifier)
        - [**\*+** 《絶対最大量指定子》](#possessive_quantifier)
    - [キャプチャ & グループ](#capture_and_group)
        - [**(　)** 《グループ》](#group)
        - [**(　)** 《キャプチャ》](#capture)
        - [**(?\<name>　)** 《名前つきキャプチャ》](#name_capture)
        - [**(?:　)** 《キャプチャなしグループ化》](#non_capture)
        - [**(?>　)** 《アトミックグループ》](#atomic_grouping)
    - [部分式呼び出し](#subexpression_call)
        - [**\g\<name>** 《\<name>の呼び出し》](#g_name_call)
        - [**\g\<n>** 《キャプチャの番号で呼び出し》](#g_num_call)
        - [**\g<±n>** 《相対番号での呼び出し》](#g_relative_num_call)
    - [選択・条件分岐](#selection_and_condition)
        - [**|** 《選択》](#selection_meta)
        - [**(?(条件)　)** 《条件分岐》](#condition)
    - [特殊変数](#special_variable)
        - [**$~** 《MatchDataオブジェクト》](#dollar_tilde)
        - [**$&** 《マッチしたテキスト》](#dollar_and)
        - [**$\`** 《マッチしたテキストの手前》](#dollar_back_quote)
        - [**$\'** 《マッチしたテキストの後ろ》](#dollar_single_quote)
        - [**$1** 《キャプチャ文字列》](#dollar_number)
        - [**$+** 《最後のキャプチャ文字列》](#dollar_plus)

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

<span id='option'></span>
## オプション

| / | new | 意味 |
|:-:|:---:|:----:|
| [i](#ignorecase) | Regexp::IGNORECASE | 大文字小文字を無視 |
| [m](#multiline) | Regexp::MULTILINE | `.`が改行マッチ |
| [x](#extended) | Regexp::EXTENDED | 空白・コメント無視 |
| [o](#o_option) | --- | 式展開を初回限定 |

<br>

正規表現リテラルの直後に記載。

```ruby
# //
/pattern/i
/pattern/im

# %r
%r(pattern)i
%r(pattern)im

# new
Regexp.new('pattern', Regexp::IGNORECASE)
Regexp.new('pattern', Regexp::IGNORECASE | Regexp::MULTILINE)
```

<span id='part'></span>
### 部分正規表現

部分的にオプションを反映させる。

#### (?on) (?-off)

**`(?on)`** => 以降全てにオプションを有効化。<br>
**`(?-off)`** => 以降全てのオプションを無効化。

```ruby
/ab(?i)cd/

/ab(?-i)cd/i
```

<details>

```ruby
/hoge(?i)fuga/ === 'hogeFUGA'
# => true

/hoge(?i)fuga/ === 'HOGEfuga'
# => false
```

```ruby
/hoge(?-i)fuga/i === 'hogeFUGA'
# => false

/hoge(?-i)fuga/i === 'HOGEfuga'
# => true
```

</details>

#### (?:(?on)　)

`(?:　)`でグループ化。括弧内のみ反映される。

```ruby
/ab(?:(?i)cd)ef/

/ab(?:(?-i)cd)ef/i
```

<details>

```ruby
/hoge(?:(?i)fuga)piyo/ === 'hogeFUGApiyo'
# => true

/hoge(?:(?i)fuga)piyo/ === 'HOGEfugapiyo'
# => false

/hoge(?:(?i)fuga)piyo/ === 'hogefugaPIYO'
# => false
```

```ruby
/hoge(?:(?-i)fuga)piyo/i === 'hogeFUGApiyo'
# => false

/hoge(?:(?-i)fuga)piyo/i === 'HOGEfugapiyo'
# => true

/hoge(?:(?-i)fuga)piyo/i === 'hogefugaPIYO'
# => true
```

</details>

<br>

<span id='ignorecase'></span>
### i / Ignorecase

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

<br>

<span id='multiline'></span>
### m / Multiline

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

<br>

<span id='extended'></span>
### x / Extended

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

<br>

<span id='o_option'></span>
### o

式展開を1回しかしない。<br>
繰り返しなどのとき、無駄な展開がなくなる。

```ruby
# //
/pattern/o

# %r
%r(pattern)o
```

<details>

```ruby
# o あり
def check(text)
  /#{@pattern}/o === text
end

@pattern = 'hoge'
check('hoge')  # => true

@pattern = 'fuga'
check('fuga')  # => false
check('hoge')  # => true

#-----------------------------
# o なし
def check(text)
  /#{@pattern}/ === text
end

@pattern = 'hoge'
check('hoge')  # => true

@pattern = 'fuga'
check('fuga')  # => true
check('hoge')  # => false
```

</details>

<span id='meta_character'></span>
## メタ文字

特別な働きをする文字列。

<br>

<span id='character'></span>
## 文字

| 記号 | 意味 |
|:----:|:----:|
| [.](#dot) | 任意の一文字 |
| [[　]](#square_brackets) |いずれか一文字 |
| [\w](#alphanumeric) | 英数アンダーバー [a-zA-Z0-9] |
| [\W](#non_alphanumeric) | 英数アンダーバー以外 [^a-zA-Z0-9] |
| [\d](#number) | 数字 [0-9] |
| [\D](#non_number) | 数字以外 [^0-9] |
| [\s](#blank_character) | 空白文字 [\t\r\n\f\v] |
| [\S](#non_blank_characther) | 空白文字以外 [^\t\r\n\f\v] |

<br>

<span id='dot'></span>
### .

任意の1文字。<br>
改行は除く。`m`オプションでマッチ。

```ruby
/aa.bb/
```

<details>

```ruby
/b.t/ === 'bet'  # => true
/b.t/ === 'bat'  # => true
/b.t/ === 'bit'  # => true
/b.t/ === 'bt'  # => false
/b.t/ === 'boot'  # => false
/b.t/ === 'beta'  # => false
```

</details>

<br>

<span id='square_brackets'></span>
### [　]

`[　]`内のいずれか一文字。

```ruby
/a[bcd]e/
```

<details>

```ruby
/b[aei]t/ === 'bat'  # => true
/b[aei]t/ === 'bet'  # => true
/b[aei]t/ === 'bit'  # => true
/b[aei]t/ === 'bot'  # => false
/b[aei]t/ === 'bt'  # => false
/b[aei]t/ === 'beet'  # => false
/b[aei]t/ === 'beat'  # => false
```

</details>

<br>

<span id='denial_square_brackets'></span>
#### [^　]

`[　]`内のいずれか以外の一文字。

```ruby
/a[^bcd]e/
```

<details>

```ruby
/b[^aei]t/ === 'bot'  # => true
/b[^aei]t/ === 'bat'  # => false
/b[^aei]t/ === 'bet'  # => false
/b[^aei]t/ === 'bit'  # => false
```

</details>

<br>

<span id='range_square_brackets'></span>
#### [　-　]

連続した文字や数字は、`-`で省略可。

```ruby
/a[b-f]g/

/0[1-5]6/

/a[b-f1-5]g/
```

<details>

```ruby
/b[a-j]t/ === 'bat'  # => true
/b[a-j]t/ === 'bet'  # => true
/b[a-j]t/ === 'bit'  # => true
/b[a-j]t/ === 'bot'  # => false
```

</details>

<br>

<span id='alphanumeric'></span>
### \w

英小文字・英大文字・数字・アンダーバー。`[a-zA-Z0-9]`と同じ。<br>
半角のみ。全角は含まない。(ASCIIの範囲を対象)

```ruby
/\w/
```

<details>

```ruby
/\w/ === 'a'  # => true
/\w/ === 'A'  # => true
/\w/ === '1'  # => true
/\w/ === '_'  # => true
/\w/ === '-'  # => false
/\w/ === ' '  # => false
/\w/ === "\n"  # => false
/\w/ === 'ａ'  # => false
/\w/ === '１'  # => false

/1\w1/ === '1a1'  # => true
/1\w1/ === '1ab1'  # => false
/1\w1/ === '1a21'  # => false
```

</details>

<br>

<span id='non_alphanumeric'></span>
### \W

英小文字・英大文字・数字・アンダーバー以外。`[^a-zA-Z0-9]`と同じ。
半角のみ。全角は可。(ASCIIの範囲を対象)

```ruby
/\W/
```

<details>

```ruby
/\W/ === 'a'  # => false
/\W/ === 'A'  # => false
/\W/ === '1'  # => false
/\W/ === '_'  # => false
/\W/ === '-'  # => true
/\W/ === ' '  # => true
/\W/ === "\n"  # => true
/\W/ === 'ａ'  # => true
/\W/ === '１'  # => true

/1\W1/ === '1-1'  # => true
/1\W1/ === '1--1'  # => false
/1\W1/ === "1-\n1"  # => false
```

</details>

<br>

<span id='number'></span>
### \d

数字。`[0-9]`と同じ。
半角のみ。全角は含まない。(ASCIIの範囲を対象)

```ruby
/\d/
```

<details>

```ruby
/\d/ === '1'  # => true
/\d/ === 'a'  # => false

/a\da/ === 'a1a'  # =>true
/a\da/ === 'a12a'  # => false
```

</details>

<br>

<span id='non_number'></span>
### \D

数字以外。`[^0-9]`と同じ。
半角のみ。全角は可。(ASCIIの範囲を対象)

```ruby
/\D/
```

<details>

```ruby
/\D/ === 'a'  # => true
/\D/ === '1'  # => false

/1\D1/ === '1a1'  # => true
/1\D1/ === '1ab1'  # => false
```

</details>

<br>

<span id='blank_character'></span>
### \s

空白文字。`[ \t\r\n\f\v]`と同じ。

```ruby
/\s/
```

<details>

| 空白文字 | 意味 |
|:--------:|:----:|
|   | スペース |
| \t | タブ文字 (制御コード 0x09) |
| \r | リターン (制御コード 0x0d) |
| \n | 改行 |
| \f | 改ページ (制御コード 0x0c) |
| \v | 垂直タブ (制御コード 0x0b) |

```ruby
/\s/ === ' '  # => true
/\s/ === "\t"  # => true
/\s/ === "\r"  # => true
/\s/ === "\n"  # => true
/\s/ === "\f"  # => true
/\s/ === "\v"  # => true
/\s/ === '　'  # => false
/\s/ === 'a'  # => false
/\s/ === '1'  # => false

/1\s1/ === '1 1'  # => true
/1\s1/ === "1\n1"  # => true
/1\s1/ === "1\n\n1"  # => false
/1\s1/ === "1\n\f1"  # => false
```

</details>

<br>

<span id='not_blank_character'></span>
### \S

空白文字以外。`[^ \t\r\n\f\v]`と同じ。

```ruby
/\S/
```

<details>

```ruby
/\s/ === ' '  # => false
/\s/ === "\t"  # => false
/\s/ === "\r"  # => false
/\s/ === "\n"  # => false
/\s/ === "\f"  # => false
/\s/ === "\v"  # => false
/\s/ === '　'  # => true
/\s/ === 'a'  # => true
/\s/ === '1'  # => true

/1\s1/ === "1aa1"  # => false
/1\s1/ === "1ab1"  # => false
```

</details>

<br>

<span id='anchor'></span>
## アンカー

| 記号 | 意味 |
|:----:|:----:|
| [^](#caret) | 行頭 |
| [$](#dollar) | 行末 |
| [\A](#string_first) | 文字列の先頭 |
| [\Z](#string_last) | 文字列の末尾 |
| [\z](#string_last_linefeed) | 文字列の末尾 改行含む |
| [\b](#boundary) | 単語の境界 |
| [\B](#non_boundary) | 単語の境界以外 |

<br>

<span id='caret'></span>
### ^

行頭(文字列の先頭・改行の次)。

```ruby
/^pattern/
```

<details>

```ruby
/^hoge/ === 'hogefuga'  # => true
/^hoge/ === 'fugahoge'  # => false

/^hoge/ === "fuga\nhoge"  # => true
/^hoge/ =~ "fuga\nhoge"  # => 5
```

</details>

<br>

<span id='dollar'></span>
### $

行末(文字列の末尾・改行の手前)。

```ruby
/pattern$/
```

<details>

```ruby
/hoge$/ === 'fugahoge'  # => true
/hoge$/ === 'hogefuga'  # => false

/hoge$/ === "hoge\nfuga"  # => true
/hoge$/ === "fugahoge\npiyo"  # => true
/hoge$/ =~ "fugahoge\npiyo"  # => 5
```

</details>

<br>

<span id='string_first'></span>
### \A

文字列の先頭。

```ruby
/\Apattern/
```

<details>

```ruby
/\Ahoge/ === 'hoge fuga'  # => true
/\Ahoge/ === 'hogefuga'  # => true
/\Ahoge/ === 'fuga hoge'  # => false
/\Ahoge/ === "fuga\nhoge"  # => false
```

</details>

<br>

<span id='string_last'></span>
### \Z

文字列の末尾。<br>
改行であった場合、その手前。

```ruby
/pattern\Z/
```

<details>

```ruby
/hoge\Z/ === 'fuga hoge'  # => true
/hoge\Z/ === 'fugahoge'  # => true
/hoge\Z/ === 'hoge fuga'  # => false

/hoge\Z/ === "fuga\nhoge"  # => true
/hoge\Z/ === "fuga hoge\n"  # => true
/hoge\Z/ === "fuga hoge\npiyo"  # => false
```

</details>

<br>

<span id='string_last_linefeed'></span>
### \z

文字列の末尾。<br>
改行も含む。

```ruby
/pattern\z/
```

<details>

```ruby
/hoge\z/ === 'fuga hoge'  # => true
/hoge\z/ === 'fugahoge'  # => true
/hoge\z/ === 'hoge fuga'  # => false

/hoge\z/ === "fuga\nhoge"  # => true
/hoge\z/ === "fuga hoge\n"  # => false
```

</details>

<br>

<span id='boundary'></span>
### \b

単語の境界(先頭・末尾)。

```ruby
/\bpattern/

/pattern\b/
```

<details>

```ruby
/\bho/ === 'hoxx'  # => true
/\bho/ === 'xxxx hoxx xxxx'  # => true
/\bho/ === 'xxho'  # => false

/ho\b/ === 'xxho'  # => true
/ho\b/ === 'xxxx xxho xxxx'  # => true
/ho\b/ === 'hoxx'  # => true
```

</details>

<br>

<span id='non_boundary'></span>
### \B

単語の境界(先頭・末尾)以外。

```ruby
/\Bpattern/

/pattern\B/
```

<details>

```ruby
/\Bho/ === 'xxho'  # => true
/\Bho/ === 'xxxx xxho xxxx'  # => true
/\Bho/ === 'xxhoxx'  # => true
/\Bho/ === 'hoxx'  # => false
/\Bho/ === 'xxxx hoxx'  # => false

/ho\B/ === 'hoxx'  # => true
/ho\B/ === 'xxxx hoxx xxxx'  # => true
/ho\B/ === 'xxhoxx'  # => true
/ho\B/ === 'xxho'  # => false
/ho\B/ === 'xxho xxxx'  # => false
```

</details>

<br>

<span id='look'></span>
## 先読み・後読み

マッチ条件になるが、結果には含めない。

| 記号 | 意味 |
|:----:|:----:|
| [(?=　)](#positive_lookahead) | 肯定先読み |
| [(?!　)](#negative_lookahead) | 否定先読み |
| [(?<=　)](#positive_lookbehind) | 肯定後読み |
| [(?<!　)](#negative_lookbehaind) | 否定後読み |

<br>

<span id='positive_lookahead'></span>
### (?=　)

直後にパターンがある。

```ruby
/pattern(?=pattern)/
```

<details>

```ruby
'hoge'.match(/hoge(?=1234)/)  # => nil
'hoge1234'.match(/hoge(?=1234)/)  # => #<MatchData "hoge">
'1234hoge'.match(/hoge(?=1234)/)  # => nil
```

</details>

<br>

<span id='negative_lookahead'></span>
### (?!　)

直後にパターンがない。


```ruby
/pattern(?!pattern)/
```

<details>

```ruby
'hoge'.match(/hoge(?!1234)/)  # => #<MatchData "hoge">
'hoge1234'.match(/hoge(?!1234)/)  # => nil
'1234hoge'.match(/hoge(?!1234)/)  # => #<MatchData "hoge">
```

</details>

<br>

<span id='positive_lookbehind'></span>
### (?<=　)

直前にパターンがある。

```ruby
/(?<=pattern)pattern/
```

<details>

```ruby
'hoge'.match(/(?<=1234)hoge/)  # => nil
'hoge1234'.match(/(?<=1234)hoge/)  # => nil
'1234hoge'.match(/(?<=1234)hoge/)  # => #<MatchData "hoge">
```

</details>

<br>

<span id='negative_lookbehaind'></span>
### (?<!　)

直前にパターンがない。

```ruby
/(?<!pattern)pattern/
```

<details>

```ruby
'hoge'.match(/(?<!1234)hoge/)  # => #<MatchData "hoge">
'hoge1234'.match(/(?<!1234)hoge/)  # => #<MatchData "hoge">
'1234hoge'.match(/(?<!1234)hoge/)  # nil
```

</details>

<span id='repeat'></span>
## 繰り返し

| 記号 | 意味 |
|:----:|:----:|
| [*](#zero_times) | 0回以上 |
| [+](#one_times)| 1回以上 |
| [?](#zero_or_one) | 0か1回 |
| [{n}](#n_times) | n回 |
| [{min,}](#min) | min回以上 |
| [{,max}](#max) | max回以下 |
| [{min,max}](#min_max) | min回以上、max回以下 |
| [*?](#reluctant_quantifier) | 最小量指定子 |
| [*+](#possessive_quantifier) | 絶対最大量指定子 |

<br>

<span id='zero_times'></span>
### *

直前の文字を**0回以上**繰り返す。

```ruby
/pattern*/
```

<details>

```ruby
/h*/ === ''  # true
/h*/ === 'h'  # true
/h*/ === 'hh'  # true
/h*/ === 'hhh'  # true
/h*/ === 'abc'  # true

/ho*g/ === 'hg'  # true
/ho*g/ === 'hog'  # true
/ho*g/ === 'hoog'  # true
/ho*g/ === 'hooog'  # true
/ho*g/ === 'hoge'  # true
/ho*g/ === 'hooge'  # true
/ho*g/ === 'hoeg'  # false
```

</details>

<br>

<span id='one_times'></span>
### +

直前の文字を**1回以上**繰り返す。

```ruby
/pattern+/
```

<details>

```ruby
/h+/ === 'h' # => true
/h+/ === 'hh' # => true
/h+/ === 'hhh' # => true
/h+/ === ''  # => false
/h+/ === 'abc'  # => false

/ho+g/ === 'hog'  # => true
/ho+g/ === 'hoog'  # => true
/ho+g/ === 'hooog'  # => true
/ho+g/ === 'hoge'  # => true
/ho+g/ === 'hooge'  # => true
/ho+g/ === 'hg'  # => false
/ho+g/ === 'hoeg'  # => false
```

</details>

<br>

<span id='zero_or_one'></span>
### ?

直前の文字が、**0回**か**1回**。

```ruby
/pattern?/
```

<details>

```ruby
/lo?l/ === 'll'  # => true
/lo?l/ === 'lol'  # => true
/lo?l/ === 'lool'  # => false
/lo?l/ === 'logol'  # => false
```

</details>

<br>

<span id='n_times'></span>
### {n}

直前の文字を、`n`で指定した回数ちょうど繰り返す。

```ruby
/pattern{n}/
```

<details>

```ruby
/h{2}/ === 'h'  # => false
/h{2}/ === 'hh'  # => true

/lo{2}l/ === 'll'  # => false
/lo{2}l/ === 'lol' # => false
/lo{2}l/ === 'lool'  # => true
/lo{2}l/ === 'loool'  # => false
/lo{2}l/ === 'logol'  # => false
```

</details>

<br>

<span id='min'></span>
### {min,}

直前の文字を、`min`で指定した回数以上繰り返す。
(`,`の後にスペースを入れない)

```ruby
/pattern{min,}/
```

<details>

```ruby
/lo{2,}l/ === 'll'  # => false
/lo{2,}l/ === 'lol'  # => false
/lo{2,}l/ === 'lool'  # => true
/lo{2,}l/ === 'loool'  # => true
/lo{2,}l/ === 'looool'  # => true
/lo{2,}l/ === 'loogool'  # => false
```

</details>

<br>

<span id='max'></span>
### {,max}

直前の文字を、`max`で指定した回数以下繰り返す。
(`,`の前後にスペースを入れない)

```ruby
/pattern{,max}/
```

<details>

```ruby
/lo{,2}l/ === 'll'  # => true
/lo{,2}l/ === 'lol'  # => true
/lo{,2}l/ === 'lool'  # => true
/lo{,2}l/ === 'loool'  # => false
/lo{,2}l/ === 'looool'  # => false
/lo{,2}l/ === 'logol'  # => false
```

</details>

<br>

<span id='min_max'></span>
### {min,max}

直前の文字を、`min`回以上`max`回以下繰り返す。<br>
(`,`の後にスペースを入れない)

```ruby
/pattern{min,max}/
```

<details>

```ruby
/lo{2,4}l/ === 'll'  # => false
/lo{2,4}l/ === 'lol'  # => false
/lo{2,4}l/ === 'lool'  # => true
/lo{2,4}l/ === 'loool'  # => true
/lo{2,4}l/ === 'looool'  # => true
/lo{2,4}l/ === 'loooool'  # => false
/lo{2,4}l/ === 'loooogooool'  # => false
```

</details>

<br>

<span id='reluctant_quantifier'></span>
### *?

量指定のメタ文字の後に`?`をつけると、**最小量指定子**になる。<br>
(デフォルトは最大良指定子)

`*?`, `+?`, `??`, `{n}?`, `{min,}?`, `{,max}?`, `{min,max}?`

<details>

```ruby
/ho*/.match('hoooo')  # => #<MatchData "hoooo">
/ho*?/.match('hoooo')  # => #<MatchData "h">

/ho+/.match('hoooo')  # => #<MatchData "hoooo">
/ho+?/.match('hoooo')  # => #<MatchData "ho">

/ho?/.match('hoooo')  # => #<MatchData "ho">
/ho??/.match('hoooo')  # => #<MatchData "h">

/^(.*)(\d+)z/.match('abcd1234z')
# => #<MatchData "abcd1234z" 1:"abcd123" 2:"4">
/^(.*?)(\d+)z/.match('abcd1234z')
# => #<MatchData "abcd1234z" 1:"abcd" 2:"1234">
```

</details>

<br>

<span id='possessive_quantifier'></span>
### *+

量指定のメタ文字の後に`+`をつけると、**絶対最大量指定子**になる。

`*+`, `++`, `?+`

[アトミックグループ`(?>　)`](#atomic_grouping)と同じ。

<details>

```ruby
/(.*)1/.match('hoge1')  # => #<MatchData "hoge1" 1: "hoge">
/(.*+)1/.match('hoge1')  # => nil
```

</details>

<br>

<span id='capture_and_group'></span>
## キャプチャ & グループ

| 記号 | 意味 |
|:----:|:----:|
| [(　)](#group) | グループ化 |
| [(　)](#capture) | キャプチャ |
| [(?\<name>　)](#name_capture) | 名前キャプチャ |
| [(?:　)](#non_capture) | キャプチャなしグループ化 |
| [(?>　)](#atomic_grouping) | アトミックグループ |

<br>

<span id='group'></span>
### (　)

グループ化。繰り返しなどで使用。

```ruby
/pa(tte)rn/
```

<details>

```ruby
/l(ho)*l/ === 'll'  # => true
/l(ho)*l/ === 'lhol'  # => true
/l(ho)*l/ === 'lhohol'  # => true
/l(ho)*l/ === 'lhohohol'  # => true
/l(ho)*l/ === 'lhl'  # => false
/l(ho)*l/ === 'lhohl'  # => false
```

</details>

<br>

<span id='capture'></span>
### (　)

マッチした`()`内の部分取得が可能。<br>
呼び出しは`var[n]`。



```ruby
/a(..)b/
```
<br>

キャプチャで`()`で取得した値は、正規表現内で参照可能。<br>
参照メタ文字は、以下のどれでも可。

- `\1, \2, ・・・`
- `\k<1>, \k<2>, ・・・`
- `\k'1', \k'2', ・・・`

```ruby
/a(..)b\1c/
```

<details>

```ruby
var = /2(....)3(\w)4(\w*)5/.match('12hoge3A4fuga56')
# => #<MatchData "2hoge3A4fuga5" 1:"hoge" 2:"A" 3:"fuga">

var[0]  # => "2hoge3A4fuga5"
var[1]  # => "hoge"
var[2]  # => "A"
var[3]  # => "fuga"
```

```ruby
/a(..)b\1c/.match('aABbABc')
# => #<MatchData "aABbABc" 1:"AB">

/a(..)b\1c/.match('aABbCDc')
# => nil
```

</details>

<br>

<span id='name_capture'></span>
### (?\<name>　)

名前つきキャプチャ。

```ruby
/abc(?<name>pattern)def/
```

参照は、`\k<name>`・`\k'name'`。<br>
呼び出しは、`variable[:name]`。

<details>

```ruby
var = /2(?<hoge>....)3/.match('12fuga34')
# => #<MatchData "2fuga3" hoge:"fuga">

var[0]  # => "2fuga3
var[:name]  # => "fuga"
```

</details>

<br>

<span id='non_capture'></span>
### (?:　)

キャプチャなしのグループ化。

```ruby
/ab(?:pattern)cd/
```

<details>

```ruby
/l(?:hoge)l/.match('lhogel')
# => #<MatchData "lhogel" 1:"hoge">

/l(hoge)l/.match('lhogel')
# => #<MatchData "lhogel"
```

</details>

<br>

<span id='atomic_grouping'></span>
### (?>　)

アトミック(不可分)なグループを作る。<br>
キャプチャはつかない。

```ruby
/(?>pattern)/
```

**不可分**： 密接に結びついていて、分けたり切り離したりできないこと。

<details>

```ruby
'abcde'.match(/(\w*)e/)  # => #<MatchData "abcde" 1: "abcd">

'abcde'.match(/(?>\w*)e/)  # => nil
```

- アトミックなし
    1. `\w*`で、アルファベット`abcde`全てにマッチ。
    2. `1.`で全てのアルファベットをマッチしてしまったため、`e`のマッチは失敗。
    3. [バックトラック] マッチした`abcde`の`e`を手放し、リトライ。
    4. 最後の`e`がマッチし、`<MatchData "abcde" 1: "abcd">`となる。
- アトミックあり
    1. `\w*`で、アルファベット`abcde`全てにマッチ。
    2. `1.`で全てのアルファベットをマッチしてしまったため、`e`のマッチは失敗。
    3. アトミックグループのため、バックトラックが起こらず、`nil`となる。

</details>

<br>

<span id='subexpression_call'></span>
## 部分式呼び出し

`\k`との違いは、文字列を呼び出すか、正規表現を呼び出すか。

`\k<name>` => マッチした**文字列**を呼び出す。<br>
`\g<name>` => **正規表現**を呼び出す。

<br>

<span id='g_name_call'></span>
### \g\<name>

名前つきキャプチャ`(?<name>　)`で指定した正規表現を呼び出す。<br>
呼び出しは、`\g<name>`または`\g'name'`。

```ruby
/(?<name>pattern)\g<name>/
```

<details>

```ruby
/(?<hoge>.{4})\g<hoge>/.match('fugaPiyo')  # => #<MatchData "fugaPiyo" hoge: "Piyo">

/(?<hoge>.{4})\k<hoge>/.match('fugaPiyo')  # => nil
```

</details>

<br>

<span id='g_num_call'></span>
### \g<n>

`(　)`で指定したキャプチャを番号で呼び出す。

```ruby
/(pattern)\g<1>/
```

<details>

```ruby
/(.{4})Fuga\g<1>/.match('HogeFugaPiyo')  # => #<MatchData "HogeFugaPiyo" 1: "Piyo">

/(.{4})Fuga\k<1>/.match('HogeFugaPiyo')  # => nil
```

</details>

<br>

<span id='g_relative_num_call'></span>
### \g<±n>

現在位置から相対的に指定。

`\g<-n>` => 自分より**前方**の相対番号。自身がキャプチャの場合、自身も含み、結果を上書き。(`\g'-n'`でも可)<br>
`\g<+n>` => 自分より**後方**の相対番号。自身がキャプチャの場合、自身は含まない。(`\g'+n'`でも可)

```ruby
/\g<+1>(pattern)\g<-1>/
```

<details>

```ruby
/(\d*)(....)(\g<-3>)/.match('123hoge45')  # => #<MatchData "123hoge45" 1:"45" 2:"hoge" 3:"45">

/(\g<+2>)(....)(\d*)/.match('123hoge45')  # => #<MatchData "123hoge45" 1:"123" 2:"hoge" 3:"45">
```

</details>

<br>

<span id='selection_and_condition'></span>
## 選択・条件分岐

<span id='selection_meta'></span>
### |

`|`で区切られたいずれか。

```ruby
/patternA|patternB|patternC/
```

<details>

```ruby
'hoge'.match(/hoge|fuga|piyo/)  # => #<MatchData "hoge">
'fuga'.match(/hoge|fuga|piyo/)  # => #<MatchData "hoge">
'piyo'.match(/hoge|fuga|piyo/)  # => #<MatchData "hoge">
'foo'.match(/hoge|fuga|piyo/)  # => nil
```

</details>

<br>

<span id='condition'></span>
### (?(条件)　)

条件分岐。条件が真であるとき、パターンが使用される。<br>
パターンに`|`を入れると、分岐が可能。`(?(条件)真|偽)`

条件はキャプチャを使用。`(条件)`に、キャプチャ番号や名前を入れ、マッチしていたら真。

```ruby
/(?(condition)pattern)/

/(?(condition)true_pattern|false_pattern)/
```

<details>

```ruby
/(?:(alphabet)|(number))\:\s(?(1)([a-z]+)|(\d+))/.match('alphabet: abcd')
# => #<MatchData "alphabet: abcd" 1:"alphabet" 2:nil 3:"abcd" 4:nil>

/(?:(alphabet)|(number))\:\s(?(1)([a-z]+)|(\d+))/.match('number: 1234')
# => #<MatchData "number: 1234" 1:nil 2:"number" 3:nil 4:"1234">
```

</details>

<br>

<span id='special_variable'></span>
## 特殊変数

| 記号 | 意味 |
|:----:|:----:|
| [$~](#dollar_tilde) | MatchDataオブジェクト |
| [$&](#dollar_and) | マッチテキスト |
| [$\`](#dollar_back_quote) | マッチテキストの前 |
| [$\'](#dollar_single_quote) | マッチテキストの後ろ |
| [$1](#dollar_number) | キャプチャ |
| [$+](#dollar_puls) | 最後のキャプチャ |

<br>

<span id='dollar_tilde'></span>
### $~

最後に成功したマッチのMatchDataオブジェクト。<br>
(`Regexp.last_match`と同じ)

<details>

```ruby
'hoge'.match(/hoge/)

$~  # => #<MatchData "hoge">

Regexp.last_match  # => #<MatchData "hoge">

'fuga'.match(/fuga/)

$~  # => #<MatchData "fuga">
```

</details>

<br>

<span id='dollar_and'></span>
### $&

マッチした文字列。

<details>

```ruby
'hoge1234'.match(/hoge/)

$&  # => "hoge"
```

</details>

<br>

<span id='dollar_back_quote'></span>
### $`

マッチした部分より前の文字列。

<details>

```ruby
'hogefugapiyo'.match(/fuga/)

$`  # => "hoge"
```

</details>

<br>

<span id='dollar_single_quote'></span>
### $'

マッチした部分より後の文字列。

<details>

```ruby
'hogefugapiyo'.match(/fuga/)

$'  # => "piyo"
```

</details>

<br>

<span id='dollar_number'></span>
### $1

マッチしたキャプチャの文字列。<br>
`$1`, `$2`, `$3`・・・と対応する数字を入れる。

<details>

```ruby
'hogefuga1234'.match(/(hoge)(fuga)(\d*)/)

$1  # => "hoge"
$2  # => "fuga"
$3  # => "1234"
```

</details>

<br>

<span id='dollar_puls'></span>
### $+

マッチした最後のキャプチャの文字列。

<details>

```ruby
'hogefuga1234'.match(/(hoge)(fuga)(\d*)/)

$+  $ => "1234"
```

</details>
