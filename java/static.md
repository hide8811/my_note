# static

【静的な、固定された、変化がない】

- インスタンスを生成しなくても呼び出せる。
- インスタンス化の影響を受けない。

### staticを付ける

- クラスで呼び出し(Class.method)
- クラスで使用する変数を指定(インスタンス作成回数のカウントなど)

### staticを付けない

- インスタンスで呼び出し (instance.method)
- 変数はインスタンス呼び出し時に初期化

<br>

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

<details>

```java
class Test {
  public int count = 0;              // static なし
  public static int countStatic = 0; // static あり

  public Test() {
    count++;       // インスタンス作成時に、初期化してから+1
    countStatic++; // インスタンス作成時に、+1
  }

  public void printCount() {
    System.out.println("count: " + count);
    System.out.println("countStatic: " + countStatic);
    System.out.println("---");
  }
}
```

```java
class Main {
  public static void main(String[] args) {
    Test test1 = new Test();
    test1.printCount();

    Test test2 = new Test();
    test2.printCount();

    Test test3 = new Test();
    test3.printCount();
  }
}
```

</details>
