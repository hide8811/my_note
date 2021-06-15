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

### モード

文字列で指定する。

| 文字列 | 意味 |
|:------:|:-----|
| r | 読み込み |
| w | 書き込み (ファイルが存在する場合は内容を空に) |
| a | 追加書き込み |
| r+ | 読み書き (ファイル先頭位置から) |
| w+ | 読み書き (ファイルが存在する場合は内容を空に) |
| a+ | 読み書き (読み込み: 先頭、書き込み: 末尾) |

<details>

**`r` (読み込み)**

```bash
$ cat test.txt
Hello
```

```ruby
file = File.open('test.txt', 'r')

content = file.read

file.close

puts content  # => Hello
```

<br>

```ruby
# 書き込みは不可
File.open('test.txt', 'r') do |f|
  f.write('World')  # => IOError (not opened for writing)
end
```

---

**`w` (書き込み)**

ファイル内は空になる。

```bash
$ cat test.txt
Hello
```

```ruby
File.open('test.txt', 'w') { |f| f.write('World') }
```

```bash
$ cat test.txt
World
```

<br>

```ruby
# 読み込みは不可
File.open('test.txt', 'w') do |f|
  f.read  # => IOError (not opened for reading)
end
```

---

**`a`  (追記)**

ファイル末尾に追記する。

```bash
$ cat test.txt
Hello
```

```ruby
File.open('test.txt', 'a') { |f| file.write('World') }
```

```bash
$ cat test.txt
Hello
World
```

<br>

```ruby
# 読み込みは不可
File.open('test.txt', 'w') do |f|
  file.read  # => IOError (not opened for reading)
end
```

---

**`r+` (先頭から読み書き)**

ファイルの先頭位置から読み書き(上書き)。

```bash
$ cat test.txt
Hello
World
```

```ruby
# 読み込み
file = File.open('test.txt', 'r+')

content = file.readline

file.close

puts content  # => Hello
```

<br>

```bash
$ cat test.txt
Hello
World
```

```ruby
# 書き込み
File.open('test.txt', 'r+') { |f| f.write('xxxxx') }
```

```bash
$ cat test.txt
xxxxx
World
```

---

**`w+` (空にして読み書き)**

```bash
$ cat test.txt
Hello
World
```

```ruby
# 読み込み
file = File.open('test.txt', 'w+', &:read)

p contnt  # => ""
```

```bash
$ cat test.txt

```

<br>

```bash
$ cat test.txt
Hello
```

```ruby
# 書き込み
File.open('test.txt', 'w+') { |f| f.write('World') }
```

```bash
$ cat test.txt
World
```

---

**`a+` (先頭読み込み + 追記)**

```bash
$ cat memo.txt
Hello
World
```

```ruby
file.open('memo.txt', 'a+')

content = file.readline

file.close

puts content  # => Hello
```

<br>

```bash
$ cat test.txt
Hello
World
```

```ruby
File.open('test.txt', 'w+') { |f| f.write('xxxxx') }
```

```bash
$ cat test.txt
xxxxx
World
```

</details>

<br>

### Universal Newline

改行の処理。<br>
モードの後に付け足す。例）`rt`

| 文字列 | 読み込み時 | 書き込み時 |
|:------:|:----------:|:----------:|
| t | LFに変換 | OS依存 |
| b | そのまま | そのまま |

<details>

#### 改行コード

| 名称 | コード | 意味 | OS |
|:----:|:------:|:-----|:--:|
| CR<br>(Carrige Return) | \r | 復帰 (カーソルを左端に移動) | MacOS 9 以前 |
| LF<br>(Line Feed) | \n | 改行 (カーソルを次の行に移動) | MacOS・Linux (UNIX系) |
| CRLF<br>(CR + LF) | \r\n | 復帰 + 改行 (カーソルを左端に移動し、次に行に移動) | Windows |

#### r

**Unix系** => `rb`<br>
**mswin・mingw** => `rt`

<br>

#### rt

改行は全てLFとして読み込む。

```bash
$ cat -e test.txt
Hello^MWorld^M
```

```ruby
File.open('test.txt', 'rt') { |f| p f.read }  # => "Hello\nWorld\n"
```

<br>

#### rb

改行をそのまま読みこむ。

```bash
$ cat -e test.txt
Hello^MWorld^M
```

```ruby
File.open('test.txt', 'rt') { |f| p f.read }  # => "Hello\rWorld\r"
```

<br>

#### w / wt

`LF`書き込み時、<br>
**Unix系** => `LF`
**mswin・mingw** => `CRLF`

<br>

#### wb

改行はそのまま書き込まれる。

```ruby
File.open('test.txt', 'wb') { |f| f.write("Hello\rWorld\r") }
```

```bash
$ cat -e test.txt
Hello^MWorld^M
```

</details>

[リファレンスマニュアル](https://docs.ruby-lang.org/ja/latest/method/Kernel/m/open.html)

<br>

<span id='new'></span>
## new (open)

ファイルを新規作成。<br>
`File.open`とほぼ同じ。<br>
<span style='color: crimson;'>ブロックは使用不可。</span>

```ruby
File.new('ファイル名', 'モード', パーミッション)
```


**モード**は[open](#open)と同じ。

**パーミッション**は整数値。

| 数値 | 意味 |
|:----:|:----:|
| 0o | 8進数 |
| 4 | 読み込み (read) |
| 2 | 書き込み (write) |
| 1 | 実行 (execute) |
| 0 | なし |

<details>

```ruby
file = File.new('test.txt', 'w', 0o644)

file.write('Hello')

file.close
```

```bash
$ ls -l test.txt
-rw-r--r-- user group xx xx xx xx:xx  test.txt

$ cat test.txt
Hello
```

</details>

[リファレンスマニュアル](https://docs.ruby-lang.org/ja/latest/method/File/s/new.html)

