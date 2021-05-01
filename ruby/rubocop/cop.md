# RuboCop

## Style

### FrozenStringLiteralComment:
***`Missing frozen string literal comment.`***<br>
(凍結文字列リテラルコメントがありません。)

**【 解決法 】**

ファイル行頭にマジックコメントを記載。

```ruby
# frozen_string_literal: true
```

もしくは、`.rubocop.yml`ファイルで除外。

```yml
Style/FrozenStringLiteralComent:
  Enabled: false
```

<br>

### AsciiComments:
***`Use only ascii symbols in comments.`***<br>
(コメントにはASCII記号のみを使用してください。)

コメントに日本語が使えない。

**【 解決法 】**

`.rubocop.yml`ファイルで除外。

```yml
Style/AsciiComments:
  Enabled: false
```

<br>

### IdenticalConditionalBranches
***`Move _____ out of the conditional.`***

同一の条件分岐。

**【 解決法 】**

if文で条件分岐した処理の共通部分は抜き出す。

```ruby
if truth
  process_A
  # process_C
else
  process_B
  # process_C
end

process_C  # 共通部分
```
