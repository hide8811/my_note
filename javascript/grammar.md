# 基本文法

- [変数宣言(var)](#var)
- [変数宣言(let)](#let)
- [定数宣言(const)](#const)
- [関数(function)](#function)
    - [関数宣言(function f())](#function_declaration)
    - [関数式(= function()](#function_based)
    - [アロー関数(() =>)](#arrow)

<span id='var'></span>
## var
変数を定義。<br>
スコープ外でも使用できてしまうため、意図せぬ挙動になることがある。<br>
`let`の使用を推奨。

```javascript
var <変数名> = <値>
```

<details>

再代入 <span style='color: navy;'>可</span>

```javascript
var num = 1;

console.log(num); // => 1

num = 2;

console.log(num); // => 2

```

<br>

再宣言 <span style='color: navy;'>可</span>

```javascript
var num = 1;

console.log(num); // => 1

var num = 2;

console.log(num); // => 2
```

<br>

スコープ外で使用 <span style='color: navy;'>可</span>

```javascript
if (true) {
  var num = 1;

  console.log(num); // => 1
}

console.log(num); // => 1
```

<br>

ネストしたスコープ内での再宣言

```javascript
let num = 1;

console.log(num); // => 1

if (true) {
  console.log(num); // => 1

  let num = 2;

  console.log(num); // => 2
}

console.log(num); // => 1
```

</details>

<span id='let'></span>
## let
変数を定義できる。

```javascript
let <変数名> = <値>
```

<details>

再代入 <span style='color: navy;'>可</span>

```javascript
let num = 1;

console.log(num); // => 1

num = 2;

console.log(num); // => 2

```

<br>

再宣言 <span style='color: crimson;'>不可</span>

```javascript
let num = 1;

let num = 2;

// Uncaught SyntaxError: Identifier 'num' has already been declared
```

<br>

再宣言(スコープ外) <span style='color: navy;'>可</span>

```javascript
if (true) {
  let num = 1;

  console.log(num); // => 1
}

if (true) {
  let num = 2;

  console.log(num); // => 2
}
```

<br>

ネストしたスコープ内での使用 <span style='color: navy;'>可</span>

```javascript
let num = 1;

if (true) {
  console.log(num); // => 1
}

console.log(num); // => 1
```

<br>

スコープ外での使用 <span style='color: crimson;'>不可</span>

```javascript
if (true) {
  let num = 1;

  console.log(num); // => 1
}

console.log(num); // => Uncaught ReferenceError: num is not defined
```

<br>

ネストしたスコープ内での再宣言

```javascript
let num = 1;

console.log(num); // => 1

if (true) {
  console.log(num); // => Uncaught ReferenceError: Cannot access 'num' before initialization

  let num = 2;

  console.log(num); // => 2
}

console.log(num); // => 1
```

</details>

<span id='const'></span>
## const
定数を定義。

```javascript
const <定数名> = <値>
```

<details>

再代入 <span style='color: crimson;'>不可</span>

```javascript
const num = 1;

num = 2;

// Uncaught TypeError: Assignment to constant variable.
```

<br>

再宣言 <span style='color: crimson;'>不可</span>

```javascript
const num = 1;

const num = 2;

// Uncaught SyntaxError: Identifier 'num' has already been declared
```

<br>

再宣言(スコープ外) <span style='color: navy;'>可</span>

```javascript
if (true) {
  const num = 1;

  console.log(num); // => 1
}

if (true) {
  const num = 2;

  console.log(num); // => 2
}
```

<br>

ネストしたスコープ内での使用 <span style='color: navy;'>可</span>

```javascript
const num = 1;

if (true) {
  console.log(num); // => 1
}

console.log(num); // => 1
```

<br>

スコープ外での使用 <span style='color: crimson;'>不可</span>

```javascript
if (true) {
  const num = 1;

  console.log(num); // => 1
}

console.log(num); // => Uncaught ReferenceError: num is not defined
```

<br>

ネストしたスコープ内での再宣言 

```javascript
const num = 1;

console.log(num); // => 1

if (true) {
  console.log(num); // => Uncaught ReferenceError: Cannot access 'num' before initialization

  const num = 2;

  console.log(num); // => 2
}

console.log(num); // => 1
```

</details>

<span id='function'></span>
## function
関数

<span id='function_declaration'></span>
### function f()
関数宣言。<br>
関数に名前をつけて定義する。

```javascript
function <関数名>(<引数>) {
  <-- 処理 -->
}
```

`;`(セミコロン)不要。

<span id='function_based'></span>
### = function()
関数式。<br>
関数を、変数や定数に入れる。

```javascript
// var・letでも可
const <変数・定数名> = function() {
  <-- 処理 -->
};
```

`;`(セミコロン)必要。

<span id='arrow'></span>
## () =>
アロー関数。

```javascript
// 引数が二つ以上
const <変数・定数名> = (<引数1>, <引数2>) => {
  <-- 処理 -->
};

// 引数が一つ
const <変数・定数名> = <引数> => {
  <-- 処理 -->
};

// 引数がない
const <変数・定数名> = () => {
  <-- 処理 -->
};

// 処理が1行
const <変数・定数名> = () => <処理>;
```
