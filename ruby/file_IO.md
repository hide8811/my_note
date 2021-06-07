# ファイル操作

- [開く【open】](#open)
- [新規作成【new】](#new)

<br>

<span id='open'></span>
## open

ファイルを開く。

```ruby
File.open('ファイル名', 'モード')

File.open('ファイル名', 'モード') { |f| 処理 }
```

<details><summary>ブロックがある場合、終了後自動で`close`される。</summary>

```ruby
# ブロックなし
file = File.open('test.txt', 'r')

p file  # => #<File:test.txt>

file.close

p file # => #<File:test.txt (closed)>
```

```ruby
# ブロックあり
file = File.open('test.txt', 'r') { |f| p f }  # => #<File:test.txt>

p file  # => #<File:test.txt (closed)>
```

</details>

<br>

| モード | 意味 |
|:------:|:-----|
| r | 読み込み |
| w | 書き込み (ファイルが存在する場合は内容を空に) |
| a | 追加書き込み |
| r+ + | 読み書き (ファイル先頭位置から) |

<details>

```txt
# test.txt
Hello
```

<br>

**`r` (読み込み)**

```ruby
file = File.open('test.txt', 'r')

content = file.read

file.close

puts content  # => Hello
```

```ruby
# 書き込みは不可
file = File.open('test.txt', 'r')

file.write('World')  # => IOError (not opened for writing)
```

<br>

**`w` (書き込み)**

ファイル内は空になる。

```ruby
file = File.open('test.txt', 'w')

file.write('World')

file.close
```

```txt
# test.txt
World
```

```ruby
# 読み込みは不可
file = File.open('test.txt', 'w')

file.read  # => IOError (not opened for reading)
```

<br>

**`a`  (追記)**

ファイル末尾に追記する。

```ruby
file = File.open('test.txt', 'a')

file.write('World')

file.close
```

```txt
# test.txt
Hello
World
```

```ruby
# 読み込みは不可
file = File.open('test.txt', 'w')

file.read  # => IOError (not opened for reading)
```

<br>

**`r+` (先頭から読み書き)**

ファイルの先頭位置から読み書き(上書き)。

```ruby
# 読み込み
file.File.open('test.txt', 'r+')

file.read  # => Hello

file.close
```

<br>

```txt
# test.txt
Hello
World
```

```ruby
# 書き込み
file = File.open('test.txt', 'r+')

file.write('xxxxx')  # ファイルの先頭に書き込み

file.close
```

```txt
# test.txt
xxxxx
World
```

</details>

[リファレンスマニュアル](https://docs.ruby-lang.org/ja/latest/method/Kernel/m/open.html)

<br>

<span id='new'></span>
## new (open)

ファイルを新規作成。

```ruby
File.new('ファイル名', 'モード', パーミッション)
```

※ `File.open`でも可。

<details>

```ruby
File.new('test.txt', 'r')  # => #<File:test.txt>
```

</details>

[リファレンスマニュアル](https://docs.ruby-lang.org/ja/latest/method/File/s/new.html)

