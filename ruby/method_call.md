# メソッド呼び出し

[リファレンスマニュアル](https://docs.ruby-lang.org/ja/latest/doc/spec=2fcall.html)

- [super](#super)
- [yield](#yield)

<span id='super'></span>
## super

オーバーライド(再定義)前のメソッドを呼び出す。

```ruby
class Hoge
  def hogehoge
    処理
  end

  def fugafuga(引数)
  　処理
  end
end

class Fuga < Hoge
  def hogehoge
    super            # 引数なし
    処理
  end

  def fugafuga(引数)
    super(引数)      # 引数あり
    処理
  end
end
```

<details>

```ruby
class Hoge
  def piyo(word)
    puts word
  end
end

class Fuga < Hoge
  def piyo(word)
    super(word)
    puts 'World'
  end
end

Fuga.new.piyo('Hello')
# => Hello
#    World
```

</details>

<br>

<span id='yield'></span>
## yield

自分で定義したブロック付きメソッドで使用<br>
渡された値はブロックの変数に代入される。<br>
<span style="color: gray;">yield: 産出・もたらす・生み出す</span>

```ruby
def hoge
  yield 値, 値, ...
end
```

<details>

```ruby
def example
  yield 'hoge', 'fuga'
end

example { |x, y| p "#{x} #{y}" }  # => "hoge fuga"
```

```ruby
class Array
  def two_each
    i = 0
    while i < length
      yield self[i], self[i + 1]
      i += 2
    end
  end
end

ary = %w[a b c d e f g h]

ary.two_each { |x, y| puts "#{x} - #{y}" }

# => a - b
#    c - d
#    e - f
#    g - h
```

</details>
