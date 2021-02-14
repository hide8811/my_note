# Rspec

- [describe / context / it](#d_c_i)
    - [describe](#describe)
    - [context](#context)
    - [it](#it)
- [before](#before)
- [shared_examples](#shared_examples)
- [shared_context](#shared_context)
- [aggregate_failures](#aggregate_failures)

<span id='d_c_i'></a>
## describe / context / it

```ruby
describe '〇〇' do
  context '〜の場合' do
    it '〜すること' do
    end
  end
end
```

<span id='describe'></a>
### 【describe】

[ 〜を記述する・〜を説明する ]<br>
<u>**テスト対象の大枠**</u>

<span id='context'></a>
### 【context】

[ 文脈・状況・前後関係 ]<br>
<u>**条件分岐**</u>

`〜の場合` **>** `〜のとき`

```ruby
context '〜の場合' do
  context '〜のとき' do
  end
end
```

<span id='it'></a>
### 【it】

<u>**テスト内容**</u>

<br>

<a id='expect'></a>
## expect

[ 期待する・予期する ]<br>
<u>**テストの結果**</u>

```ruby
it '〜すること' do
  expect(....).to eq ....
end
```

<br>

<span id='before'></a>
## before

[ 〜の前に ]<br>
<u>**共通処理・準備**</u>

```ruby
before do
  処理 1
  処理 2
end

# 1行でも可
before { 処理 }
```

<br>

<span id='shared_examples'></a>
## shared_examples

<u>**テストの共有**</u>

```ruby
shared_examples 'テスト名' do
  it '〜すること' do
  end

  it { expect }

  context '〜のとき' do
    it '〜すること' do
    end
  end
end

RSpec.describe .... do
  context '〜の場合' do
    it_behaves_like 'テスト名'
  end
end
```

ブロック変数も使用できる。

```ruby
shared_examples 'test name' do |variable, parameter|
  it { expect(variable).to eq parameter }
end

# 呼び出し
it_behaves_like 'test name', variable, parameter
```

<span id='shared_context'></span>
## shared_context

<u>**テスト前の準備の共有**</u>

```ruby
shared_context '準備名' do
  処理1
  処理2

  before do
    処理3
    処理4
  end
end

# 呼び出し
include_context '準備名'
```

ブロック因数も使用できる。

<span id='aggregate_failures'></span>
## aggregate_failures
expectをまとめる。

```ruby
it 'test' do
  aggregate_failures do
    expect(page).to have_content 'text_1'
    expect(page).to have_content 'text_2'
  end
end
```

<details>

it内に複数のexpectを記述すると、テストが失敗したところで止まってしまう。

```ruby
it 'test' do
  expect('success').to eq 'success'
  expect('success').to eq 'failure_A'
  expect('success').to eq 'success'
  expect('success').to eq 'failure_B'
  expect('success').to eq 'success'
end
```

```ruby
# テスト結果
Failures:

  1) test
     Failure/Error: expect('success').to eq 'failure_A'

       expected: 'failure_A'
            got: 'success'

       (compared using ==)

Finished in *.***** seconds (files took **.** seconds to load)
1 example, 1 failure

```

<br>
`aggregate_failures`を使用すると、テストが失敗してもit内のexpectを続け、失敗したexpectのみを表示する。

```ruby
it 'test' do
  aggregate_failures do
    expect('success').to eq 'success'
    expect('success').to eq 'failure_A'
    expect('success').to eq 'success'
    expect('success').to eq 'failure_B'
    expect('success').to eq 'success'
  end
end
```

```ruby
# テスト結果
Failures:

  1) test test
     Got 2 failures from failure aggregation block.

     1.1) Failure/Error: expect('success').to eq 'failure_A'

            expected: "failure_A"
                 got: "success"

            (compared using ==)




     1.2) Failure/Error: expect('success').to eq 'failure_B'

            expected: "failure_B"
                 got: "success"

            (compared using ==)




Finished in *.***** seconds (files took **.** seconds to load)
1 example, 1 failure

```

</details>
