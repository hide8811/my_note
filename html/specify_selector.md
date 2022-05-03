# セレクタの指定

|   | 対象 |
|:---:|:---|
| [*](#wild-card) | 全て |
| [,](#comma) | 複数 |
| [+](#plus) | 隣接 |
| [~](#tilde) | 兄弟 |
| [>](#greater-than-sign) | 子要素 |
| [スペース](#space) | 子孫 |

## <a id="wild-card">*</a>

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

## <a id="comma">,</a>

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

## <a id="plus">+</a>

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

## <a id="tilde">~</a>

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

## <a id="greater-than-sign">\></a>

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

## <a id="space">スペース</a>

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
