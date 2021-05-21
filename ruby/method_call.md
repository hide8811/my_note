# メソッド呼び出し

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
