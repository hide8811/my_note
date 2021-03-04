# BEM
class名をつける際の命名規則。

**B** : <span style='border: thin solid; padding: 0 .5rem;'>**B**lock</span>

**E** : <span style='border: thin solid; padding: 0 .5rem;'>**E**lement</span>

**M** : <span style='border: thin solid; padding: 0 .5rem;'>**M**odifier</span>

**block__element--modifier**

### Block
【 かたまり・まとまり 】

Webページを構成するパーツの一つ一つ。ヘッダー・フッター・商品説明など。

- Blockの中にBlockを使用してもよい。(ヘッダーBlockの中のロゴBlockなど)
- Block名はそのBlockの役割。(menue・formなど)
- Block単体で存在しても良い。(Elementがなくても良い)
- 単語はハイフン`-`で繋ぐ。

### Element
【 要素・成分 】

Blockを構成する要素。(ボタン・入力欄など)

- Blockとアンダーバー2つ`__`で繋ぐ。
- Element単体で存在できない。
- Elementを2つ繋げることはできない。(block__element__element はダメ)

### Modifier

【 修飾語句 】

Elementの状態や特徴を表す。

- Elementとハイフン2つ`--`で繋ぐ。
- Modifier単体で存在できない。
- Modifierを2つ繋げることはできない。(block__element--modifier--modifierはダメ)
- Boolean(真偽)やkey_value(例: color_red)で表す。
- Modifierが存在しなくても良い。
