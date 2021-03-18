# expect

expect(....).to ....

- [to/not_to](#to-not_to)
- [(....)](#expected)
    - [page](#page)
- [.... matchere](#matchers)
    - [等しいこと (eq)](#eq)
    - [ページ内に特定のテキストがあること (have_context)](#have_context)
    - [特定のセレクターに特定の要素があること (have_selector)](#have_selector)

<a id='to-not_to'></a>
## to / not_to

### to
**肯定**

### not_to
**否定**

<br>

<a id='expected'></a>
## (....)
**テストする対象・要素など**

<br>

<a id='page'></a>
### page
**ページ全体**

<a id='matchers'></a>
## .... mathchers

<a id='eq'></a>
### eq
**等しいこと**

```ruby
exoect(A).to eq B
```

<a id='have_context'></a>
### have_context
**テキストがあるかどうか**

```ruby
expect(page).to have_context 'テキスト'
```

[Method: Capybara::RSpecMatchers#have_content](https://www.rubydoc.info/github/jnicklas/capybara/Capybara%2FRSpecMatchers:have_content)

<a id='have_selector'></a>
### have_selector
**要素があるかどうか**

```ruby
# text
expect(page).to have_selector '.class', text: 'テキスト'

# class
expect(page).to have_selector '.class', class: 'class'
```

[Method: Capybara::RSpecMatchers#have_selector](https://rubydoc.info/github/jnicklas/capybara/Capybara%2FRSpecMatchers:have_selector)
