# 演算子

## 代数演算子
| 演算子 | 意味 | 例 |
| :---: | :---: | :---: |
| + | 加算 | a + b |
| - | 減算 | a - b |
| * | 乗算 | a * b |
| / | 除算 | a / b |
| % | 剰余算 | a % b |
| ** | 累乗 | a ** b |

<details>

### +
```Ruby
1 + 2
#=> 3
```

### -
```Ruby
3 - 2
#=> 1
```

### *
```Ruby
2 * 3
#=> 6
```

### /
```Ruby
6 / 2
#=> 3
```

### %
a / b の余り
```Ruby
4 % 2
#=> 0


5 % 2
#=> 1
```

### **
```Ruby
2 ** 3
#=> 8
```
</details>


### 文字列演算子
| 演算子 | 意味 | 例 |
| :---: | :---: | :---: |
| + | 連結(非破壊的) | str1 + str2 |
| << | 連結(破壊的) | str1 << str2 | <!-- -->
| * | 繰り返し | str1 * n |

<details>

### +
str1は変わらない。
```Ruby
str1 = "Hello "
str2 = "World!"
str1 + str2
#=> "Hello World!"

p str1
#=> "hello "

# 以下も同じ意味

"#{str1}#{str2}"
#=> "Hello World!"
```

### <<
str1自体が変わる
```Ruby
str1 = "Hello "
str2 = "World!"
str1 << str2
#=> "Hello World!"

p str1
#=> "Hello World!"
```

### *
```Ruby
str = "Hello!"
str * 3
#=> "Hello!Hello!Hello!"
```
</details>


## 代入演算子
| 演算子 | 意味 | 例 |
| :---: | :---: | :---: |
| = | 代入 | a = b |
| += | a = a + b | a += b |
| -= | a = a - b | a -= b |
| *= | a = a * b | a *= b |
| /= | a = a / b | a /= b |
| %= | a = a % b | a %= b |
| \**= | a = a \** b | a \**= b |

<details>

### =
```Ruby
num = 1

p num
#=> 1
```

### +=
```Ruby
num = 1
num += 2

p num
#=> 3
```

### -=
```Ruby
num = 4
num -= 3

p num
#=> 1
```

### *=
```Ruby
num = 2
num *= 3

p num
#=> 6
```

### /=
```Ruby
num = 6
num /= 3

p num
#=> 2
```

### %=
```Ruby
num = 7
num %= 3

p num
#=> 1
```

### **=
```Ruby
num = 3
num **= 2

p num
#=> 9
```
</details>


## 比較演算子
| 演算子 | 意味 | 例 |
| :---: | :---: | :---: |
| == | 等しい | a == b |
| != | 等しくない | a != |
| < | より小さい | a < b |
| > | より大きい | a > b |
| <= | 以下 | a <= b |
| >= | 以上 | a >= b |

<details>

### ==
```Ruby
1 == 1
#=> true

1 == 2
#=> false
```

### !=
```Ruby
1 != 2
#=> true

1 != 1
#=> false
```

### <
```Ruby
1 < 2
#=> true

1 < 1
#=> false

1 < 0
#=> false
```

### >
```Ruby
1 > 0
#=> true

1 > 1
#=> false

1 > 2
#=> false
```

### <=
```Ruby
1 <= 2
#=> true

1 <= 1
#=> true

1 <= 0
#=> false
```

### >=
```Ruby
1 >= 0
#=> true

1 >= 1
#=> true

1 >= 2
#=> false
```
</details>

## 論理演算子
| 演算子 | 意味 | 例 |
| :---: | :---: | :---: |
| && | and | a && b |
| \|\| | or | a \|\| b |
| !  | not | !a |

<details>

### &&
```Ruby
true && true
#=> true

true && true
#=> false

false && false
#=> false

false && false
#=> false
```

### ||
```Ruby
true || true
#=> true

true || false
#=> true

false || true
#=> true

false || false
#=> false
```

### !
```Ruby
!true
#=> false

!false
#=> true
```
</details>

## 三項演算子
| 演算子 | 例 |
| :---: | :---: |
| ? : | a ? b : c |
***a*** が真であれば ***b*** それ以外は ***c*** を返す

<details>

```Ruby
true ? "yes" : "no"
#=> "yes"

false ? "yes" : "no"
#=> "no"
```
</details>

