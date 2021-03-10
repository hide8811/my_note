# && / ||
- [&&](#and_and)
    - [and](#and)
    - [&=](#and_and_equal)
- [||](#or_or)
    - [or](#or)
    - [||=](#or_or_equal)

<span id='and_and'></span>
## &&
[リファレンスマニュアル](https://docs.ruby-lang.org/ja/2.1.0/doc/spec=2foperator.html#and)

A **かつ** B<br>

```ruby
A && B
```

まず左辺を評価する。その結果によって右辺を評価。

- `nil`の場合 => 左辺を返す。

    ```ruby
    irb(main):001:0> nil && true
    => nil
    ```

- `false`の場合 => 左辺を返す。

    ```ruby
    irb(main):001:0> false && true
    => false
    ```

- `true`の場合 => 右辺を返す。

    ```ruby
    irb(main):001:0> true && 'right'
    => 'right'
    ```

- `数字`の場合 => 右辺を返す。

    ```ruby
    irb(main):001:0> 1 && 2
    => 2
    ```

- `文字列`の場合 => 右辺を返す。

    ```ruby
    irb(main):001:0> 'left' && 'right'
    'right'
    ```

<span id='and'></span>
### and

働きは同じだが、優先度が低い。

```ruby
# &&
irb(main):001:0> var = 'left' && 'right'
irb(main):002:0> var
=> 'left'

# and
irb(main):001:0> var = 'left' and 'right'
=> 'right'
irb(main):002:0> var
=> 'left'
```

つまり、

```ruby
# &&
var = ('left' && 'right')

# and
(var = 'left') and 'right'
```
となっている。

<span id='and_and_equal'></span>
### &&=

右辺が偽(`nil`, `false`)以外のとき、右辺に左辺を代入する。

```ruby
A &&= B
```

`&&`は優先度が高いため、他(`+=`や`-=`など)とは動きが違う。

```ruby
A && (A = B)
```

<br>

---
---

<br>

<span id='or_or'></span>
## ||

[リファレンスマニュアル](https://docs.ruby-lang.org/ja/2.1.0/doc/spec=2foperator.html#or)

A **または** B<br>

```ruby
A || B
```

まず左辺を評価する。その結果によって右辺を評価。

- `true`の場合 => 左辺を返す。

    ```ruby
    irb(main):001:0> true || false
    => true
    ```

- `数字`の場合 => 左辺を返す。

    ```ruby
    irb(main):001:0> 1 || 2
    => 1
    ```

- `文字列`の場合 => 左辺を返す。

    ```ruby
    irb(main):001:0> 'left' || 'right'
    => 'left'
    ```

- `nil`の場合 => 右辺を返す。

    ```ruby
    irb(main):001:0> nil || 'right'
    => 'right'
    ```

- `false`の場合 => 右辺を返す。

    ```ruby
    irb(main):001:0> false || 'right'
    => 'right'
    ```

<span id='or'></span>
### or

働きは同じだが、優先度が低い。

```ruby
# ||
irb(main):001:0> var = false || 'right'
irb(main):002:0> var
'left'

# and
irb(main):001:0> var = false or 'right'
=> 'right'
irb(main):001:0> var
=> false
```

つまり、

```ruby
# ||
var = (false || 'right')

# or
(var = false) || 'right'
```

となっている。

<span id='or_or_equal'></span>
### ||=

右辺が偽(`nil`, `false`)のとき、右辺を左辺に代入する。

```ruby
A ||= B
```

`||`は優先度が高いため、他(`+=`や`-=`など)と動きが違う。

```ruby
A || (A = B)
```
