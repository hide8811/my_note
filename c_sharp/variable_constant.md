# 変数・定数宣言

- [組み込み型](#built-in-type)
- [変数宣言](#variable)
    - [var《暗黙的な型指定》](#var)
- [定数宣言](#const)

<br>

<span id="built-in-type"></span>
## 組み込み型

変数を宣言するときの値の型。<br>
[リファレンス](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/builtin-types/built-in-types)

| 型 | 意味 |
|:--:|:----:|
| [string](#string) | 文字列 |
| [char](#char) | 文字 |
| [int](#int) | 整数 |
| [float](#float) | 浮動小数点数(単精度) |
| [double](#double) | 浮動小数点数(倍精度) |
| [bool](#bool) | ブール値 |

<br>

<span id="string"></span>
### string

文字列の型。<br>
`"`(ダブルクォート)で囲む。

```c#
string s = "文字列";
```

<details>

```c#
string s = "hello"; // OK
string s = "h";     // OK    一文字でも可
string s = 'hello'; // error シングルクォートは不可
string s = "1234";  // OK
string s = 1234;    // error 数値は不可
string s = true;    // error 真偽値は不可
```

</details>

<br>

<span id="char"></span>
### char

文字の型。
一文字(2バイト)のみ。
`'`(シングルクォート)で囲む。

```c#
char c = 'A';
```

<details>

```c#
char c = 'a';  // OK
char c = '字'; // OK    日本語可
char c = '1';  // OK
char c = 'ab'; // error 文字列は不可
char c = "a";  // error ダブルクォートは不可
char c = 1;    // error 数値は不可
```

</details>

<br>

<span id="int"></span>
### int

整数値の型。
`-`も可。

```c#
int i = 1234;
```

<details>

```c#
int i = 1234;   // OK
int i = -1234;  // OK
int i = 1.234;  // error 小数は不可
int i = "1234"; // error 文字列は不可
int i = '1';    // error 文字は不可
int i = true    // error 真偽値は不可
```

</details>

<span id="float"></span>
### float

小数の型(単精度)。<br>
数値の最後に`f`(`F`)が必須。

| 範囲 | 有効桁数 | サイズ |
|:----:|:--------:|:------:|
| `±1.5 x 10^−45` 〜 `±3.4 x 10^38` | `6`〜`9`桁 | `4`バイト |

```c#
float f = 1.234f;
```

<details>

```c#
float f = 0.1234f;  // OK
float f = 0.1234F;  // OK    大文字でも可
float f = 1.2e34f;  // OK    指数表記も可
float f = -1.234f;  // OK
float f = "1.234"f; // error 文字列は不可
float f = truef;    // error 真偽値は不可
```

</details>

<br>

<span id="double"></span>
### double

小数の型(倍精度)。<br>
数値の最後の`d`(`D`)は、なくても可。

| 範囲 | 有効桁数 | サイズ |
|:----:|:--------:|:------:|
| `±5.0 × 10^−324` 〜 `±1.7 × 10^308` | `15`〜`17`桁 | `8`バイト |

```c#
double d = 1.234;
double d = 1.234d;
```

<details>

```c#
double d = 1.234d;  // OK
double d = 1.234D;  // OK    大文字でも可
double d = 1.234;   // OK    dはなくても可
double d = 1.2e34;  // OK
double d = "1.234"; // error 文字列は不可
double d = true;    // error 真偽値は不可
```

</details>

<br>

<span id="bool"></span>
### bool

真偽値の型。<br>
`true`or`false`が入る。

```c#
bool b = true;
```

<details>

```c#
bool b = true;       // OK
bool b = false;      // OK
bool b = "true";     // error 文字列は不可
bool b = 6 % 2 == 0; // OK    式の結果は可
```

</details>

<br>

<span id="variable"></span>
## 変数宣言

変数の宣言は、`組み込み型` + `変数名`。<br>
変数への代入は、宣言と同時にしても、後にしても可。<br>
再宣言: **不可**<br>
再代入: **可**

```c#
// 代入を後
// <組み込み型> <変数名>;
int number;
// <変数名> = <値>;
number = 1;

// 代入を同時
// <組み込み型> <変数名> = <値>;
int number = 1;
```

<details>

```c#
int number = 1;

number = 2;     // OK
int number = 2; // 再宣言不可 型は不要
```

</details>

<br>

<span id="var"></span>
### var

型の宣言をしなくても、コンパイル時に自動で判断される。<br>
[リファレンス](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/keywords/var)

```c#
var <変数名> = <値>;
```

注意点)
- 宣言のみは**不可**。必ず代入と同時に。
- 再宣言 **不可**
- 再代入は可能だが、**同じ型**のみ。
- 定数の宣言は**不可**

<details>

```c#
var number; // 宣言のみは不可
```

```c#
var number = 1234;

var number = 5678; // 再宣言は不可 型は不要
```

```c#
var number = 1234; // int型

number = "hello"; // 異なる型の代入は不可
```

</details>

<br>

<span id="const"></span>
## const

定数宣言。<br>
先頭に`const`を付ける。<br>

宣言と同時に代入。<br>
再宣言: **不可**
再代入: **不可**

```c#
const <組み込み型> <変数名> = <値>;
```

<details>

```c#
const int number; // error 宣言のみは不可
```

```c#
const int number = 1;

const int number = 2; // error 再宣言は不可
```

```c#
const int number = 1;

number = 2; // error 再代入は不可
```

</details>
