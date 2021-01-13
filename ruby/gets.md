# gets
**入力された値を文字列として取得する。**
```sh
irb(main):001:0> greet = gets
こんにちは                    # 入力待ちになる。入力しEnterで次へ。
irb(main):002:0> greet
=> "こんにちは\n"
```

ファイルの実行でも可
```ruby
# ruby.rb

p '入力してください'
greet = gets

p greet
```
```sh
# 実行結果
$ ruby ruby.rb
"入力してください"
こんにちは          # 入力・Enter
"こんにちは\n"
```

## 注意点
### 文字列になる
```sh
irb(main):001:0> int = gets
1234                        # 入力・Enter
irb(main):002:0> int
=> "1234\n"
```
入力された値は**文字列**として取得される。そのため、数値も文字列に変換されてしまう。  
数値として取得したい場合は、[**to_i**](https://docs.ruby-lang.org/ja/latest/method/String/i/to_i.html)メソッドを使用。
```sh
irb(main):001:0> int = gets.to_i
1234                             # 入力・Enter
irb(main):002:0> int
=> 1234
```

### 改行が入る
取得された値には**改行(<span style="color: red;">\n</span>)が入る。  
なくすためには、[**chomp**](https://docs.ruby-lang.org/ja/latest/method/String/i/chomp.html)メソッドを使用する。
```sh
irb(main):001:0> greet = gets.chomp
こんにちは                           # 入力・Enter
irb(main):001:0> greet
"こんにちは"
```
