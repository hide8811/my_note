# スプレッド構文

反復可能オブジェクト(配列、文字列など)を展開する。

```js
...object
```

## 使用例

### 配列を繋げる

```javascript
[...ary1, ...ary2]
```

<details>

```javascript
const ary1 = [1, 2, 3];
const ary2 = [5, 6, 7];

const newAry = [...ary1, 4, ...ary2];

console.log(newAry); // => [1, 2, 3, 4, 5, 6, 7]
```

</details>

<br />

### 引数として渡す

```javascript
myFunction(...ary)
```

<details>

```javascript
const puts = (a, b, c) => {
  console.log(`${a}, ${b}, ${c}`);
}

const ary = [1, 2, 3];
const ary2 = [1, 2];
const ary3 = [1, 2, 3, 4];

puts(...ary); // => 1, 2, 3
puts(...ary2); // => 1, 2, undefined
puts(...ary3); // => 1, 2, 3
```

</details>
