# static

【静的な、固定された、変化がない】

- インスタンスを生成しなくても呼び出せる。
- インスタンス化の影響を受けない。

## メソッドで使用

```java
public static <戻り値の型> <メソッド名>(<引数の型> <変数名>, <引数の型> <変数名>) {
  処理
}
```

<details>

`static`あり

インスタンスを生成しなくても、クラスで呼び出しが可能。

```java
class Greeting {
  public static void hello() {
    System.out.println("Hello");
  }
}
```

```java
Greeting.hello(); // => OK

Greeting hi = new Greeting();
hi.hello(); // (OK) 警告あり
```

<br>

`static`なし

クラスでの呼び出しは不可。インスタンスが必須。

```java
class Greeting {
  public void hello() {
    System.out.println("Hello");
  }
}
```

```java
Greeting.hello(); // => error

Greeting hi = new Greeting();
hi.hello(); // OK
```

</details>

<br>

## 変数で使用

```java
public static <変数の型> <変数名> = <値>;
```
