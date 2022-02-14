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

[EventTarget.addEventListener()](https://developer.mozilla.org/ja/docs/Web/API/EventTarget/addEventListener)
