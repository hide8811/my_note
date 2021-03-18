# 真偽判定
[Railsドキュメント](#https://railsdoc.com/page/empty)

- [nil?](#nil)
- [empty?](#empty)
- [blank?](#blank)
- [present?](#present)

|  | nil? | empty? | blank? | present? |
|:---:|:---:|:---:|:---:|:---:|
| **nil** | <span style='color: cyan'>true</span> | <span style='color: gray'>NoMethodError</span> | <span style='color: cyan'>true</span> | <span style='color: magenta'>false</span> |
| **''** | <span style='color: magenta'>false</span> | <span style='color: cyan'>true</span> | <span style='color: cyan'>true</span> | <span style='color: magenta'>false</span> |
| **' '** | <span style='color: magenta'>false</span> | <span style='color: magenta'>false</span> | <span style='color: cyan'>true</span> | <span style='color: magenta'>false</span> |
| **[]** | <span style='color: magenta'>false</span> | <span style='color: cyan'>true</span> | <span style='color: cyan'>true</span> | <span style='color: magenta'>false</span> |
| **{}** | <span style='color: magenta'>false</span> | <span style='color: cyan'>true</span> | <span style='color: cyan'>true</span> | <span style='color: magenta'>false</span> |
| **0** | <span style='color: magenta'>false</span> | <span style='color: gray'>NoMethodError</span> | <span style='color: magenta'>false</span> | <span style='color: cyan'>true</span> |
| **true** | <span style='color: magenta'>false</span> | <span style='color: gray'>NoMethodError</span> | <span style='color: magenta'>false</span> | <span style='color: cyan'>true</span> |
| **false** | <span style='color: magenta'>false</span> | <span style='color: gray'>NoMethodError</span> | <span style='color: cyan'>true</span> | <span style='color: magenta'>false</span> |

<br>

<span id='nil'></span>
## nil?
<span style='padding: 0 .5rem; background-color: #c01050; color: white;'>Ruby</span>のメソッド。<br>
`nil`のときのみ`true`を返す。<br>
[Object#nil?](https://docs.ruby-lang.org/ja/latest/method/Object/i/nil=3f.html)

<details>

【 nil 】

```ruby
[1] pry(main)> var = nil
=> nil
[2] pry(main)> var.nil?
=> true
```

【 空 ( '' ) 】

```ruby
[1] pry(main)> var = ''
=> ""
[2] pry(main)> var.nil?
=> false
```

【 空白 ( ' ' ) 】

```ruby
[1] pry(main)> var = ' '
=> " "
[2] pry(main)> var.nil?
=> false
```

【 空の配列 ( [] ) 】

```ruby
[1] pry(main)> var = []
=> []
[2] pry(main)> var.nil?
=> false
```

【 空のハッシュ ( {} ) 】

```ruby
[1] pry(main)> var = {}
=> {}
[2] pry(main)> var.nil?
=> false
```

【 0 】

```ruby
[1] pry(main)> var = 0
=> 0
[2] pry(main)> var.nil?
=> false
```

【 true 】

```ruby
[1] pry(main)> var = true
=> true
[2] pry(main)> var.nil?
=> false
```

【 false 】

```ruby
[1] pry(main)> var = false
=> false
[2] pry(main)> var.nil?
=> false
```

</details>

<br>

<span id='empty'></span>
## empty?
<span style='padding: 0 .5rem; background-color: #c01050; color: white;'>Ruby</span>のメソッド。<br>
文字列・配列・ハッシュに対するメソッド。<br>
それぞれが空のとき、`true`を返す。<br>
[String#empty?](https://docs.ruby-lang.org/ja/latest/method/String/i/empty=3f.html)
&nbsp;[Array#empty?](https://docs.ruby-lang.org/ja/latest/method/Array/i/empty=3f.html)
&nbsp;[Hash#empty?](https://docs.ruby-lang.org/ja/latest/method/Hash/i/empty=3f.html)

<details>

【 nil 】

```ruby
[1] pry(main)> var = nil
=> nil
[2] pry(main)> var.empty?
NoMethodError: undefined method `empty?' for nil:NilClass
from (pry):1:in `<main>'
```

【 空 ( '' ) 】

```ruby
[1] pry(main)> var = ''
=> ""
[2] pry(main)> var.empty?
=> true
```

【 空白 ( ' ' ) 】

```ruby
[1] pry(main)> var = ' '
=> " "
[2] pry(main)> var.empty?
=> false
```

【 空の配列 ( [] ) 】

```ruby
[1] pry(main)> var = []
=> []
[2] pry(main)> var.empty?
=> true
```

【 空のハッシュ ( {} ) 】

```ruby
[1] pry(main)> var = {}
=> {}
[2] pry(main)> var.empty?
=> true
```

【 0 】

```ruby
[1] pry(main)> var = 0
=> 0
[2] pry(main)> var.empty?
NoMethodError: undefined method `empty?' for 0:Integer
from (pry):1:in `<main>'
```

【 true 】

```ruby
[1] pry(main)> var = true
=> true
[2] pry(main)> var.empty?
NoMethodError: undefined method `empty?' for true:TrueClass
from (pry):1:in `<main>'
```

【 false 】

```ruby
[1] pry(main)> var = false
=> false
[2] pry(main)> var.empty?
NoMethodError: undefined method `empty?' for false:FalseClass
from (pry):1:in `<main>'
```

</details>

<br>

<span id='blank'></span>
## blank?
<span style='padding: 0 .5rem; border: thin solid #c01050; color: #c01050;'>Rails</span>のメソッド。<br>
Rubyの`nil?`と`empty?`が合わさったようなメソッド。<br>
ただし、文字列がスペースのみであった場合(全角半角関係なし)と`false`の場合も`true`を返す。<br>
[GitHub rails/blank.rb](https://github.com/rails/rails/blob/main/activesupport/lib/active_support/core_ext/object/blank.rb#L6-L20)

<details>

【 nil 】

```ruby
[1] pry(main)> var = nil
=> nil
[2] pry(main)> var.blank?
=> true
```

【 空 ( '' ) 】

```ruby
[1] pry(main)> var = ''
=> ""
[2] pry(main)> var.blank?
=> true
```

【 空白 ( ' ' ) 】

```ruby
[1] pry(main)> var = ' '
=> " "
[2] pry(main)> var.blank?
=> true
```

【 空の配列 ( [] ) 】

```ruby
[1] pry(main)> var = []
=> []
[2] pry(main)> var.blank?
=> true
```

【 空のハッシュ ( {} ) 】

```ruby
[1] pry(main)> var = {}
=> {}
[2] pry(main)> var.blank?
=> true
```

【 0 】

```ruby
[1] pry(main)> var = 0
=> 0
[2] pry(main)> var.blank?
=> false
```

【 true 】

```ruby
[1] pry(main)> var = true
=> true
[2] pry(main)> var.blank?
=> false
```

【 false 】

```ruby
[1] pry(main)> var = false
=> false
[2] pry(main)> var.blank?
=> true
```

</details>

<br>

<span id='present'></span>
## present?
<span style='padding: 0 .5rem; border: thin solid #c01050; color: #c01050;'>Rails</span>のメソッド。<br>
`blank?`の反対。<br>
[GitHub rails/blank.rb](https://github.com/rails/rails/blob/main/activesupport/lib/active_support/core_ext/object/blank.rb#L22-L27)

<details>

【 nil 】

```ruby
[1] pry(main)> var = nil
=> nil
[2] pry(main)> var.present?
=> false
```

【 空 ( '' ) 】

```ruby
[1] pry(main)> var = ''
=> ""
[2] pry(main)> var.present?
=> false
```

【 空白 ( ' ' ) 】

```ruby
[1] pry(main)> var = ' '
=> " "
[2] pry(main)> var.present?
=> false
```

【 空の配列 ( [] ) 】

```ruby
[1] pry(main)> var = []
=> []
[2] pry(main)> var.present?
=> false
```

【 空のハッシュ ( {} ) 】

```ruby
[1] pry(main)> var = {}
=> {}
[2] pry(main)> var.present?
=> false
```

【 0 】

```ruby
[1] pry(main)> var = 0
=> 0
[2] pry(main)> var.present?
=> true
```

【 true 】

```ruby
[1] pry(main)> var = true
=> true
[2] pry(main)> var.present?
=> true
```

【 false 】

```ruby
[1] pry(main)> var = false
=> false
[2] pry(main)> var.present?
=> false
```

</details>
