# イベント

ブラウザのウィンドウ上で生じた動作・出来事。<br />
(クリックやスクロールなど)

[イベントリファレンス](https://developer.mozilla.org/ja/docs/Web/Events)<br />
[イベントへの入門](https://developer.mozilla.org/ja/docs/Learn/JavaScript/Building_blocks/Events)

## イベントハンドラとイベントリスナ

イベントハンドラ`Event Handler`: イベント発火時に実行される処理<br />
イベントリスナ`Event Listener`: イベントの発生を監視し、イベントハンドラと結びつける。

Handoler: 取り扱う人・調教師・トレーナー<br />
Listener: 聞く人・聴取者


## イベントハンドラの登録

- イベントハンドラプロパティを使用する。(`onevent`)
- イベントリスナで紐付け。(`addEventListener`)
- ~~HTMLのイベントハンドラ属性を使用する。(`onevent="myFunc()"`)~~<span style="font-size: small">非推奨</span>

### イベントハンドラプロパティ(`onevent`)

イベントハンドラをイベントハンドラプロパティに代入する。<br />

```javascript
target.onevent = eventHandler
```

<details>

```javascript
const btn = document.getElementById('btn');

const putsHello = () => console.log('Hello');

btn.onclick = putsHello;

// Hello
```

</details>

<br />

イベントハンドラプロパティは、`on` + `イベント`<br />
例) `onclick` `onscroll` など

登録できるイベントハンドラは**1つ**。<br />
2つ目以降は上書きされる。

<details>

```javascript
const btn = document.getElementById('btn');

const putsHello = () => console.log('Hello');
const putsWorld = () => console.log('World');

btn.onclick = putsHello;
btn.onclick = putsWorld;

// World
```

</details>

<br />

[GlobalEventHandlers](https://developer.mozilla.org/ja/docs/Web/API/GlobalEventHandlers)

<br />

### イベントリスナを使用した紐付け(`addEventListener`)

イベントリスナを使用し、イベントとイベントハンドラを紐づける。

```javascript
target.addEventListener('event', eventHandler);
```

<details>

```javascript
const btn = document.getElementById('btn');

const putsHello = () => console.log('Hello');

btn.addEventListener('click', putsHello);

// Hello
```

</details>

<br />

複数のイベントハンドラが登録できる。

<details>

```javascript
const btn = document.getElementById('btn');

const putsHello = () => console.log('Hello');
const putsWorld = () => console.log('World');

btn.addEventListener('click', putsHello);
btn.addEventListener('click', putsWorld);

// Hello
// World
```

</details>

<br />

#### 第一引数 【イベント】

#### 第二引数 【関数 or `handleEvent()`をもつオブジェクト】

<details>

```javascript
// 関数を渡す
const btn = document.getElementById('btn');
const changeColor = (e) => { e.currentTarget.style.color = 'red'; };

btn.addEventListener('click', changeColor);
```

```javascript
// 無名関数を渡す
const btn = document.getElementById('btn');

btn.addEventListener('click', function () {
  this.style.color = 'red';
});

// アロー関数
btn.addEventListener('click', (e) => {
  e.currentTarget.style.color = 'red';
});
```

```javascript
// オブジェクト(handleEvent)を渡す
const btn = document.getElementById('btn');
const changeColor = {
  handleEvent() {
    e.currentTarget.style.color = 'red';
  },
};

btn.addEventListener('click', changeColor);
```

</details>

<br />

##### 関数の重複

同じ関数やオブジェクトがすでに登録されていた場合、二つ目以降は追加されない。<br />
ただし、無名関数だった場合は別物と見做されるため、二つ目以降も追加される。

<details>

```javascript
// 関数の場合
const btn = document.getElementById('btn');
const putsHello = () => { console.log('Hello'); };

btn.addEventListener('click', putsHello);
btn.addEventListener('click', putsHello);
// 出力は一回
//
// Hello
```

```javascript
// オブジェクトの場合
const btn = document.getElementById('btn');
const putsHello = {
  handleEvent() { console.log('Hello'); },
};

btn.addEventListener('click', putsHello);
btn.addEventListener('click', putsHello);
// 出力は一回
//
// Hello
```

```javascript
// 無名関数の場合
const btn = document.getElementById('btn');

btn.addEventListener('click', () => { console.log('Hello'); });
btn.addEventListener('click', () => { console.log('Hello'); });
// 出力は二回
//
// Hello
// Hello
```

</details>

<br />

#### イベントリスナの関数に引数を渡す

イベントリスナに渡す関数の引数は、イベントオブジェクトのみ。

<details>

```javascript
const btn = document.getElementById('btn');
const putsArg = (event) => { console.log(event) };

btn.addEventListener('click', putsArg); // => PointerEvent {isTrusted: true, pointerId: 1, width: 1, height: 1, pressure: 0, …}
```

</details>

<br />

##### オブジェクト(`hendleEvent`)を使用

オブジェクトのプロパティで渡す。

```javascript
target.addEventListener('event', {
  key: 'value',
  handleEvent: myFunc,
});
```

<details>

```javascript
const btn = document.getElementById('btn');
const putsWord = function () {
  console.log(this.word);
};

btn.addEventListener('click', {
  word: 'Hello',
  handleEvent: putsWord,
});
// => Hello
```

</details>

<br />

##### `bind()`を使用

イベントハンドラに`bind()`で引数を渡す。

```javascript
target.addEventListener('event', myFunc.bind(null, arg));
```

<details>

```javascript
const btn = document.getElementById('btn');
const putsWord = (word) => { console.log(word); };

btn.addEventListener('click', putsWord.bind(null, 'Hello'));
// => Hello
```

<br />

`event`オブジェクトを使用する際は、`bind`で渡した引数の次に指定する。

```javascript
const btn = document.getElementById('btn');
const putsWord = (hoge, fuga, event) => { console.log(hoge, fuga, event.type); };

btn.addEventListener('click', putsWord.bind(null, 'Hello', 'World'));
// => Hello World click
```

</details>

<br />

##### 無名関数を使用

イベントハンドラに無名関数を使用し、その中で関数を呼び出す。

```javascript
target.addEventListener('event', function() {
  myFunc(arg);
});
```

<details>

```javascript
const btn = document.getElementById('btn');
const putsWord = (word) => { console.log(word); };

btn.addEventListener('click', function() {
  putsWord('Hello');
});
```

</details>

<br />

[EventTarget.addEventListener()](https://developer.mozilla.org/ja/docs/Web/API/EventTarget/addEventListener)
