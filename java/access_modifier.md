# アクセス修飾子

メソッドや変数の先頭に記載。<br>
どこからアクセス可能かを決定する。

- [public 《どこからでもアクセス可》](#public)
- [private 《現在のクラス内でのみアクセス可》](#private)

<span id="public"></span>
## public

どこからでも使用可能な修飾子。

```java
public static <組み込み型> <変数名> = <値>;

public static <返り値の型> <メソッド名>() { ... };
```

<details>

```java
class Test {
  public static String hello = "Hello World";

  public static void printHello() {
    System.out.println(hello); // OK
  }
}
```

```java
class Main {
  public static void main(String[] args) {
    System.out.println(Test.hello); // OK 変数呼び出し【Test.hello】
    Test.printHello(); // OK
  }
}
```

</details>

<br>

<span id="private"></span>
## private

クラス内でのみ使用可能な修飾子。

```java
private static <組み込み型> <変数名> = <値>;

private static <返り値の型> <メソッド名>() { ... };
```

<details>

```java
class Test {
  private static String hello = "Hello World";

  private static void printHello() {
    System.out.println(hello); // OK
  }
}
```

```java
class Main {
  public static void main(String[] args) {
    System.out.println(Test.hello); // error
    Test.printHello(); // error
  }
}
```

</details>
