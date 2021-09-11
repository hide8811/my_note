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
