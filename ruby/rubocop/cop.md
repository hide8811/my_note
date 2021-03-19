# RuboCop

## Style

### FrozenStringLiteralComment:
***Missing frozen string literal comment.***<br>
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
`Use only ascii symbols in comments.`<br>
***`Use only ascii symbols in comments.`***<br>
(コメントにはASCII記号のみを使用してください。)

**【 解決法 】**

`.rubocop.yml`ファイルで除外。

```yml
Style/AsciiComments:
  Enabled: false
```
