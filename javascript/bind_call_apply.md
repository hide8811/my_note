# bind()

関数に`this`と引数を指定した、新しい関数を生成する。

```javascript
func.bind(thisArg, agr);
```

`func`: 対象となる関数。<br />
`thisArg`: 第一引数。関数に渡される`this`の値。<br />
`arg`: 関数に渡される引数。複数可。本来の関数が持つ引数の前に追加される。

<details>

### `this`を渡す

```javascript
this.text = 'this text';

const obj = {
  text: 'obj text',
  getText() {
    return this.text;
  },
};

console.dir(obj.getText); // => Function: getText
console.log(obj.getTest()); // obj text

const bindGetText = obj.getText.bind(this);
console.dir(bindGetText); // => Function: bound getText
console.log(bindGetText()); // => this text
```

### 引数を渡す

```javascript
const myFunc = (agr, agr2, agr3, agr4) => {
  console.log(agr, agr2, agr3, agr4);
};

const bindFunc = myFunc.bind(null, 'bindAgr', 'bindAgr2');

bindFunc('Agr', 'Agr2'); // => bindAgr bindAgr2 Agr Agr2
```

</details>
