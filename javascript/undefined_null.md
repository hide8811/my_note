# undefined と null

値がないこと。

`undefined` => 自動的<br />
`null` => 意図的

## undefined

変数が未定義の際など、値が存在しない時、自動的に割り当てられる。

```javascript
let hoge;

console.log(hoge); // => undefined
```

## null

値がないことを意図的に示す値。<br />
基本的に自然発生はしない。

```javascript
let hoge = null;

console.log(hoge); // => null
```

## 比較

```javascript
typeof undefined // => undefined
typeof null // => object

undefined == null // => true
undefined === null // => false

Boolean(undefined) // => false
Boolean(null) // => false

undefined + 1 // => NaN
null + 1 // => 1
```
