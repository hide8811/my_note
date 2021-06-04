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

