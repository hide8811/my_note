# 基本文法

- [変数宣言(let)](#let)
    - [変数宣言(var)](#var)

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

// Uncaught SyntaxError:
// Identifier 'num' has already been declared
```

<br>

スコープ外での使用 <span style='color: crimson;'>不可</span>

```javascript
let num = 1;

console.log(num); // => 1

if (num === 1) {
  console.log(num); // => ReferenceError
}

console.log(num); // => 1
```

<br>

スコープ外であれば同じ変数名が使用可。

```javascript
let num = 1;

console.log(num); // => 1

if (num === 1) {
  let num = 2;

  console.log(num); // => 2
}

console.log(num); // => 1
```

</details>

<span id='var'></span>
## var
変数宣言。<br>
スコープ外でも使用できてしまうため、意図せぬ挙動になることがある。

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
var num = 1;

console.log(num); // => 1

if (num === 1) {
  console.log(num); // => 1
}

console.log(num); // => 1
```

</details>

