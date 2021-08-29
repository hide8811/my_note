# インクリメント / デクリメント

## インクリメント演算子

値を`1`**増やす**。

```java
i++
++i
```

`i++`: [後置インクリメント演算子](#prefix)<br>
`++i`: [前置インクリメント演算子](#postfix)

<details>

```java
int i = 0;

i++;

System.out.println(i); // => 1
```

</details>

<br>

## デクリメント演算子

値を`1`**減らす**。

```java
i--
--i
```

`i--`: [後置デクリメント演算子](#prefix)<br>
`--i`: [前置デクリメント演算子](#postfix)

<details>

```java
int i = 1;

i--;

System.out.println(i); // => 0
```

</details>

<br>

## 前置 / 後置

<span id="prefix"></span>
### 前置

演算子を変数の前に記載する。<br>
演算子の処理が優先(先に処理)される。

```java
++i
--i
```

<details>

```java
int i = 0;

int n = ++i;

System.out.println(n); // => 1
```

1. `i + 1`が先に処理
2. `n = i`で、iがnに代入される

<br>

```java
int i = 0;

System.out.println(++i); // => 1
```

1. `i + 1`が先に処理
2. `i`が出力される

<br>

```java
int i = 0;

++i == 1; // => true
```

1. `i + 1`が先に処理
2. `i == 1`で、比較される

</details>

<br>

<span id="postfix"></span>
### 後置

演算子を変数の後に記載する。<br>
演算子の処理が劣後(後に処理)される。

```java
i++
i--
```

<details>

```java
int i = 0;

int n = i++;

System.out.println(n); // => 0
```

1. `n = i`が先に処理されて、`i = 0`がnに代入
2. `i + 1`が後から処理される
3. `n`の出力は`0`

<br>

```java
int i = 0;

System.out.println(i++); // => 0
```

1. 先に`i = 0`が出力される
2. 後から`i + 1`が処理される

<br>

```java
int i = 0;

i++ == 1; // false
```

1. 先に`i == 1`が比較される(iは0のまま)
2. 後から`i + 1`が処理される

</details>
