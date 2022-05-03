# セレクタ

|   | 対象 |
|:---:|:---|
| [*](#wild-card) | 全て |
| [,](#comma) | 複数 |
| [+](#plus) | 隣接 |
| [~](#tilde) | 兄弟 |
| [>](#greater-than-sign) | 子要素 |
| [スペース](#space) | 子孫 |

- [優先度(詳細度)](#specificity)

## 指定

### <a id="wild-card">*</a>

全ての要素

```html
<div>
  親要素
  <div>
    子要素
    <div>孫要素</div>
  </div>
</div>
```

```css
* {
  color: green;
}
```

***結果***

<span style="color: green;">親要素</span><br>
<span style="color: green;">子要素</span><br>
<span style="color: green;">孫要素</span><br>

### <a id="comma">,</a>

複数要素の同時指定

```html
<div class="element-a">要素A</div>
<div class="element-b">要素B</div>
<div class="element-c">要素C</div>
```

```css
.element-a,
.element-c {
  color: green;
}
```

***結果***

<span style="color: green">要素A</span><br>
要素B<br>
<span style="color: green">要素C</span><br>

### <a id="plus">+</a>

直後の兄弟要素

```html
<div class="element">
  要素A
</div>

<div class="current">
  要素

  <div class="element">
    子要素
  </div>
</div>

<div class="element">
  要素B
</div>

<div class="element">
  要素C
</div>
```

***結果***

要素A<br>
要素<br>
子要素<br>
<span style="color: green;">要素B</span><br>
要素C

<br>

※ 直後にない場合は不可

```html
<div class="current">
  要素
</div>

<div>
  要素A
</div>

<div class="element">
  要素B
</div>
```

```css
.current + .element {
  color: green;
}
```

***結果***

要素<br>
要素A<br>
要素B

### <a id="tilde">~</a>

兄弟要素全て

```html
<div class="element">
  要素A
</div>

<div class="current">
  要素

  <div class="element">
    子要素
  </div>
</div>

<div class="element">
  要素B
</div>

<div>
  <div class="element">
    甥要素
  </div>
</div>

<div class="element">
  要素C
</div>
```

```css
.current ~ .element {
  color: green;
}
```

***結果***

要素A<br>
要素<br>
子要素<br>
<span style="color: green;">要素B</span><br>
甥要素<br>
<span style="color: green;">要素C</span>

### <a id="greater-than-sign">\></a>

直下の子要素<br>
孫要素には作用しない

```html
<div class="parent element">
  親要素

  <div class="element">
    子要素A
  </div>

  <div class="element">
    子要素B
  </div>

  <!-- 孫要素は不可 -->
  <div>
    <div class="element">
      孫要素
    </div>
  </div>
</div>

<div class="element">
  兄弟要素

  <div class="element">
    甥要素
  </div>
</div>
```

```css
.parent > .element {
  color: green;
}
```

***結果***

親要素<br>
<span style="color: green;">子要素A</span><br>
<span style="color: green;">子要素B</span><br>
孫要素<br>
兄弟要素<br>
甥要素<br>

### <a id="space">スペース</a>

子孫要素

```html
<div class="parent element">
  親要素

  <div class="element">
    子要素A
  </div>

  <div class="element">
    子要素B
  </div>

  <div>
    <div class="element">
      孫要素
    </div>
  </div>

  <div>
    <div>
      <div class="element">
        ひ孫要素
      </div>
    </div>
  </div>
</div>

<div class="element">
  兄弟要素

  <div class="element">
    甥要素
  </div>
</div>
```

## <a id="specificity">優先度(詳細度)</a>

基本はcssファイルの最後に宣言されたもの。<br>

詳細レベルがあり、高い方が優先される。<br>
`要素` **＜** `class / 属性 / 擬似クラス` **＜** `id` **＜** `style属性`

それぞれが点数を持っていて、その合計で優先度が変わる。

|   | 点数 |
|:---:|:---:|
| style属性 | 1,000 |
| id | 100 |
| class / 属性 / 擬似クラス | 10 |
| 要素 | 1 |

ただし、点数よりも詳細度レベルの方が優先される。<br>
(`class`11個より`id`の方が強い)


<details>

基本はcssファイルの最後に宣言されたもの。

```html
<div class="green red">text</div>
```

```css
.green {
  color: green;
}

.red {
  color: red;
}
```

***結果***

<span style="color: red">text</span>

<br>

#### `要素` <[](>) `class`

```html
<div class="green">text</div>
```

```css
.green {
  color: green;
}

div {
  color: red;
}
```

***結果***

<span style="color: green">text</span>


<br>

#### `class` = `属性` = `擬似クラス`

```html
<div class="green" data-color="red">text</div>
```

```css
.green {
  color: green;
}

[data-color="red"] {
  color: red;
}
```

***結果***

<span style="color: red;">text</span>

<br>

#### `class` <[](>) `id`

```html
<div id="red" class="green">text</div>
```

```css
#red {
  color: red;
}

.green {
  color: green;
}
```

***結果***

<span style="color: red;">text</span>

<br>

#### `id` <[](>) `style属性`

```html
<div id="red" style="color: green;">text</div>
```

```css
#red {
  color: red;
}
```

***結果***

<span style="color: green;">text</span>

<br>

#### 点数計算

```html
<div class="class" data-color="green">text</div>
```

```css
.class1[data-color="green"] {  /* 20点 */
  color: green;
}

.class1 {  /* 10点 */
  color: red;
}
```

***結果***

<span style="color: green">text</span>

<br>

```html
<div class="parent">
  <div class="element">text</div>
</div>
```

```css
.parent > .element {  /* 20点 */
  color: green;
}

.element {  /* 10点 */
  color: red;
}
```

***結果***

<span style="color: green;">text</span>

<br>

```html
<div class="parent">
  <div class="element red text">text</div>
</div>
```

```css
.parent > .element {  /* 20点 */
  color: green;
}

.element.red.text {  /* 30点 */
  color: red;
}
```

***結果***

<span style="color: red;">text</span>

<br>

点数をより詳細レベルの方が優先<br>
`class`を11個繋げても`id`に勝てない

```html
<div id="id" class="c1 c2 c3 c4 c5 c6 c7 c8 c9 c10 c11">text</div>
```

```css
#id {
  color: green;
}

.c1.c2.c3.c4.c5.c6.c7.c8.c9.c10.c11 {
  color: red;
}
```

***結果***

<span style="color: green">text</span>

</details>
