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

File.open('ファイル名', 'モード', &:メソッド)
```

<details>

```ruby
# 代入
file = File.open('test.txt', 'r')

content = file.read

file.close

p content  # => "Hello\n"
```

```ruby
# ブロック
File.open('test.txt', 'r') { |r| p r.read }  # => "Hello\n"
```

```ruby
# ブロック省略
content = File.open('test.txt', 'r', &:read)

p content  # => "Hello\n"
```

<br>

ブロックがある場合、終了後自動で`close`される。

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
| r+ | 読み書き (ファイル先頭位置から) |
| w+ | 読み書き (ファイルが存在する場合は内容を空に) |

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
File.open('test.txt', 'r') do |f|
  f.write('World')  # => IOError (not opened for writing)
end
```

<br>

**`w` (書き込み)**

ファイル内は空になる。

```ruby
File.open('test.txt', 'w') { |f| f.write('World') }
```

```txt
# test.txt
World
```

```ruby
# 読み込みは不可
File.open('test.txt', 'w') do |f|
  f.read  # => IOError (not opened for reading)
end
```

<br>

**`a`  (追記)**

ファイル末尾に追記する。

```ruby
File.open('test.txt', 'a') { |f| file.write('World') }
```

```txt
# test.txt
Hello
World
```

```ruby
# 読み込みは不可
File.open('test.txt', 'w') do |f|
  file.read  # => IOError (not opened for reading)
end
```

<br>

**`r+` (先頭から読み書き)**

ファイルの先頭位置から読み書き(上書き)。

```ruby
# 読み込み
file = File.open('test.txt', 'r+')

content = file.read

file.close

puts content  # => Hello
```

<br>

```txt
# test.txt
Hello
World
```

```ruby
# 書き込み
File.open('test.txt', 'r+') { |f| f.write('xxxxx') }
```

```txt
# test.txt
xxxxx
World
```

<br>

**'w+' (空にして読み書き)**

```ruby
# 読み込み
file = File.open('test.txt', 'w+', &:read)

p contnt  # => ""
```

```ruby
# 書き込み
File.open('test.txt', 'w+') { |f| f.write('World') }
```

```txt
# test.txt
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

