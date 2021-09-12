# 数値リテラル

## 整数値

- int型
- long型

### int型

デフォルト。特に指定していない場合、int型になる。<br>
範囲は、`-2147483648` 〜 `2147483647`

```java
int num = 123;
int minNum = -2147483648;
int maxNum = 2147483647;

System.out.println(1234); // int型
```

```java
int minNum = -2147483649; // error

int maxNum = 2147483648; // error

System.out.println(2147483648); // error
```

### long型

int型よりも広い範囲の整数値を使用することができる。<br>
範囲は、`-9223372036854775808` 〜 `9223372036854775807`

指定方法は、数値の末尾に`L`(もしくは`l`)をつける。

```java
long num = 10000000000L;

System.out.println(10000000000L);
```

```java
long = 1234L; // long型

long minNum = -9223372036854775809L; // error

long maxNum = 9223372036854775808L; // error
```
