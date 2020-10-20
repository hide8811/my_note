# Rubyの実行

<br>

## ファイルの実行
```
$ ruby [オプション] <ファイル名>
```

| オプション | 説明 |
| --- | --- |
| -c | 文法チェック。コンパイルのみ行い、実行はしない。<br>文法エラーがなければ、"Syntax OK" と出力。 |
| -K[kcode] | 文字コードの指定。 例) -Ku で UTF-8 |

<br>
<br>

## スクリプトの実行
```
$ ruby -e <スクリプト>
```

スクリプトは``''``か``""``で囲む。
```
$ ruby -e 'puts "Hello"'

Hello
```

-e を複数も可。
```
$ ruby -e 'hoge = "Hello "' -e 'fuga = "World!"' -e 'puts hoge + fuga'

Hello World!
```

途中の改行もできる。
```
$ ruby -e 'hoge = "Hello "
quote> fuga = "World!"
quote> puts hoge + fuga'

Hello World!
```

``;``で区切ることもできる。
```
$ ruby -e 'hoge = "Hello "; fuga = "World!"; puts hoge + fuga'

Hello World!
```
<br>
<br>

## 対話形式での実行
```
$ irb
```
Interactive Rubyの略。
```
$ irb

irb(main):001:0> puts 'Hello World!'
Hello World!
=> nil
irb(main):002:0>
```

変数やメソッドの呼び出しもできる。
```
$ irb

irb(main):001:1* def greeting(name)
irb(main):002:1*   puts "Hello #{name}!"
irb(main):003:0> end
=> :greeting
irb(main):004:0> greeting('World')
Hello World!
=> nil
irb(main):005:0>
```

``exit``で終了。
```
$ irb

irb(main):001:0> puts 'Hello World!'
Hello World!
=> nil
irb(main):002:0> exit

$
```

