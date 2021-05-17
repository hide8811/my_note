# 制御構造

- [条件分岐](#conditional_branch)
    - [if](#if)
    - [unless](#unless)
    - [case](#case)
- [繰り返し](#repeat)
    - [while](#while)
    - [until](#until)
    - [for](#for)
- [繰り返し制御](#repeat_control)
    - [break](#break)
    - [next](#next)
    - [redo](#redo)
- [例外処理](#exception_handling)
    - [begin](#begin)
        - [rescue](#rescue)
        - [else](#else)
        - [ensure](#ensure)
    - [raise](#raise)
    - [特殊変数 $! / $@](#special_variable)

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
`when`の式に`*`をつけると、配列が展開される。

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
when 式1       # 式1 === 式0
  処理
when 式2, 式3  # 式2 === 式0 or 式3 === 式0
  処理
else           # それ以外
  処理
end
```

```ruby
ary = [1, 2, 3]

case 式
when ary    # [1, 2, 3] => [1, 2, 3] === 式
  処理
when *ary   # 1, 2, 3 => 1 === 式 or 2 === 式 or 3 === 式
  処理
end
```

<br>

<span id='repeat'></span>
## 繰り返し

<span id='while'></span>
### while

**真**(`false`, `nil`以外)の間、処理を繰り返す。

```ruby
while 式
  処理
  処理
end

# 1行
処理 while 式
```

<br>

<span id='until'></span>
### until

**偽**(`false`, `nil`)の間、処理を繰り返す。

```ruby
until 式
  処理
  処理
end

# 1行
処理 until 式
```

<br>

<span id='for'></span>
### for

要素の数だけ繰り返し実行。<br>
要素には**範囲**や**配列**を使用。<br>
`each`との違いは変数のスコープ。

<details>

二重配列

```ruby
ary = [[1, 2], [3, 4], [5, 6]]

for var in ary
  p var
end
# => [1, 2]
#    [3, 4]
#    [5, 6]

for var1, var2 in ary
  p "#{var1} #{var2}"
end

# => "1 2"
#    "3 4"
#    "5 6"
```

<br>

`each`との比較

```ruby
# each
(1..5).each do |num|
  var = num
end

var  # =>NameError (undefined local variable or method `var' for main:Object)
```

```ruby
# for
for num in 1..5
  var = num
end

var  # => 5
```

</details>

<br>

```ruby
for 変数 in 要素
  処理
end
```

<br>

<span id='repeat_control'></span>
## 繰り返し制御

<br>

<span id='break'></span>
### break

繰り返しを中断する。<br>
引数の指定ができる。

```ruby
break

break 引数
```

<details>

```ruby
for var in 1..5
  break if var == 4
  p var
end

# => 1
#    2
#    3
```

```ruby
# 引数なし
val = (1..5).each { |num| break if num == 3 }

val  # => nil


# 引数あり
val = (1..5).each { |num| break num if num == 3 }

val  # => 3
```

</details>

<br>

<span id='next'></span>
### next

以降の処理をしないで、次の要素に進む。<br>
引数の指定ができる。

```ruby
next

next 引数
```

<details>

```ruby
for var in 1..10
  next if var.even?
  p var
end

# => 1
#    3
#    5
#    7
#    9
```

```ruby
# 引数なし
val = (1..10).map do |num|
  next if num.even?
  num * 10
end

val  # => [10, nil, 30, nil, 50, nil, 70, nil, 90, nil]


# 引数あり
val = (1..10).map do |num|
  next num if num.even?
  num * 10
end

val  # => [10, 2, 30, 4, 50, 6, 70, 8, 90, 10]
```

</details>

<br>

<span id='redo'></span>
### redo

以降の処理を中断し、初めからやり直す。(繰り返し要素はそのまま)

```ruby
redo
```

<details>

```ruby
count = 0

for num in 1..5
  count += 1
  redo if count == 3
  p "#{count}: #{num}"
end

# => "1: 1"
#    "2: 2"
#    "4: 3"
#    "5: 4"
#    "6: 5"
```

</details>

<br>

<span id='exception_handling'></span>
## 例外処理

[class Exception](https://docs.ruby-lang.org/ja/latest/class/Exception.html)<br>
[例外一覧(組み込みライブラリ)](https://docs.ruby-lang.org/ja/latest/library/_builtin.html)

<br>

<span id='begin'></span>
### begin

例外(エラーなど)が発生した場合、プログラムがそこで止まらないようにする。

<span id='rescue'></span>
#### rescue

例外が発生した場合の処理。

`rescue 例外クラス名`: 例外オブジェクトのクラス指定。省略すると、`StandardError`のサブクラス全てを捕捉。<br>
`rescue => 変数`: 変数にエラー内容を格納。

```ruby
begin
  例外が起こりうるコード
rescue 例外クラス名, => 変数
  例外が発生した場合の処理
end
```

`例外クラス名`、`=> 変数`は省略可。

<details>

```ruby
begin
  1 / 0
rescue => e
  puts e
end

# => divided by 0
```

<br>

**【例外処理をしていない場合】**

```ruby
# test.rb
1 / 0

puts 'Hello'
```

```sh
# 実行結果
test.rb:1:in `/': divided by 0 (ZeroDivisionError)
        from memo.rb:1:in `<main>'

```

<br>

**【例外処理をしている場合】**

```ruby
# test.rb
begin
  1 / 0
rescue
  puts 'Hi'
end

puts 'Hello'
```

```sh
# 実行結果
Hi
Hello
```

<br>

**`=>`**

```ruby
# test.rb

begin
  1 / 0
rescue => e
  p e                   # => #<ZeroDivisionError: divided by 0>
  p e.class             # => ZeroDivisionError
  p e.class.superclass  # => StandardError
  p e.message           # => "divided by 0"
  p e.backtrace         # => ["test.rb:2:in `/'", "test.rb:2:in `<main>'"]
end
```

| メソッド | 意味 |
|:--------:|:-----|
| [class](https://docs.ruby-lang.org/ja/latest/method/Object/i/class.html) | レシーバーのクラスを返す |
| [superclass](https://docs.ruby-lang.org/ja/latest/method/Class/i/superclass.html) | スーパークラス(親クラス)を返す |
| [message](https://docs.ruby-lang.org/ja/latest/method/Exception/i/message.html) | エラーメッセージを返す |
| [backtrace](https://docs.ruby-lang.org/ja/latest/method/Exception/i/backtrace.html) | バックトレース(例外発生の過程)を返す |

<br>

**例外オブジェクトのクラス指定**<br>
例外の種類に応じて、処理を分岐させることができる。

```ruby
begin
  1 / 0
rescue ZeroDivisionError => e
  puts e
end
```

<br>

指定しない場合、`StandardError`のサブクラス以外は捕捉しない。

```ruby
begin
  raise NameError
rescue
  puts 'hoge'
end

# => "hoge"
```

```ruby
begin
  raise SyntaxError
rescue
  puts 'hoge'
end

# => test.rb:2:in `<main>': compile error (SyntaxError)
```

</details>

<br>

<span id='else'></span>
#### else

例外が発生しなかった場合の処理。

```ruby
begin
  例外が起こりうるコード
rescue
  例外が発生した場合の処理
else
  例外が発生しなかった場合の処理
end
```

<details>

```ruby
begin
  n = 1 / 0
rescue => e
  puts e
else
  puts n
end

# => divided by 0


begin
  n = 1 / 1
rescue => e
  puts e
else
  puts n
end

# => 1
```

</details>

<br>

<span id='ensure'></span>
#### ensure

例外が発生してもしなくても評価される処理。

```ruby
begin
  例外が起こりうるコード
rescue
  例外が発生した場合の処理
ensure
  必ず行う処理
end
```

<details>

```ruby
begin
  1 / 0
rescue => e
  puts e
ensure
  puts '終了'
end

# => divided by 0
#    終了


begin
  1 / 1
rescue => e
  puts e
ensure
  puts '終了'
end

# => 終了
```

</details>

<br>

<span id='raise'></span>
### raise

例外を発生させる。<br>

```ruby
raise
raise 'メッセージ'
raise 例外クラス
raise 例外クラス, 'メッセージ'
raise 例外クラス, 'メッセージ', [バックトレース]
```

<details>

**引数なし**:<br>
直前の例外を再発生。直前がないときは、`RuntimeError`。

```ruby
raise  # => RuntimeError
1/0    # => ZeroDivisionError
raise  # => ZeroDivisionError
```

<br>

**メッセージ**:<br>
引数で指定したメッセージの`RuntimeError`を発生。

```ruby
raise 'message'
# => #<RuntimeError: message>
```

<br>

**例外クラス**:<br>
引数で指定した例外クラスを発生。

```ruby
raise NameError
# => #<NameError: NameError>
```

<br>

**例外クラス, メッセージ**<br>
引数で指定したメッセージの例外クラスを発生。

```ruby
raise NameError, 'message'
# => #<NameError: message>
```

**例外クラス, メッセージ, バックトレース**

クラス・メッセージ・バックトレース(例外発生の過程)を指定した例外を発生。

```ruby
begin
  raise NameError, 'message', %w(hoge fuga piyo)
rescue => e
  p e.class      # => NameError
  p e.message    # => "message"
  p e.backtrace  # => ["hoge", "fuga", "piyo"]
end
```

</details>

<br>

<span id='special_variable'></span>
### 特殊変数

#### $!

最後に発生した例外オブジェクトが格納された変数。

```ruby
$!
```

<details>

```ruby
begin
  1 / 0
rescue => e
  puts $!.class             # => ZeroDivisionError
  puts e.class              # => ZeroDivisionError
  puts $!.class.superclass  # => StandardError
  puts e.class.superclass   # => StandardError
  puts $!.message           # => divided by 0
  puts e.message            # => divided by 0
end
```

</details>

<br>

#### $@

例外発生時のバックトレース(例外発生までの過程)が配列で格納された変数。

```ruby
$@
```

<details>

```ruby
# test.rb

begin
  1/0
rescue => e
  p $@            # => ["test.rb:2:in `/'", "test.rb:2:in `<main>'"]
  p $!.backtrace  # => ["test.rb:2:in `/'", "test.rb:2:in `<main>'"]
  p e.backtrace   # => ["test.rb:2:in `/'", "test.rb:2:in `<main>'"]
end
```

</details>
