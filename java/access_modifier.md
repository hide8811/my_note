# アクセス修飾子

メソッドや変数の先頭に記載。<br>
どこからアクセス可能かを決定する。

- [public 《どこからでもアクセス可》](#public)
- [protected 《サブクラスからのアクセスが可能》](#protected)
- [なし 《同じパッケージのクラスから](#none)
- [private 《現在のクラス内でのみアクセス可》](#private)

<span id="public"></span>
## public

**どこからでも**使用可能な修飾子。

```java
public <static> <組み込み型> <変数名> = <値>;

public <static> <返り値の型> <メソッド名>() { ... };
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

<span id="protected"></span>
## protected

**同じパッケージのクラス**か、違うパッケージの**サブクラス**でのみ使用可能な装飾子。

```java
protected <static> <組み込み型> <変数名> = <値>;

protected <static> <返り値の型> <メソッド名>() { ... };
```

<details>

同パッケージ

```java
class Test {
  protected static String hello = "Hello World";

  protected static void printHello() {
    System.out.println(hello);
  }
}
```

```java
class Main {
  public static void main(String[] args) {
    System.out.println(Test.hello); // OK 同じパッケージ内のため、呼び出し可能
    Test.printHello(); // OK 同じパッケージ内のため、呼び出し可能
  }
}
```

<br>

異パッケージ・サブクラス

```bash
.
├── Main.java
├── sample
│    └── Test.java
└── sample2
     └── SubTest.java
```

```java
package sample;

public class Test {
  protected static String hello = "Hello World";

  protected static void printHello() {
    System.out.println(hello);
  }
}
```

```java
package sample2;

import sample.Test;

public class SubTest extends Test {
  public static void subPrintHello() {
    System.out.println(Test.hello); // OK サブクラスなため可
  }
}
```

```java
import sample.Test;
import sample2.SubTest;

class Main {
  public static void main(String[] args) {
    System.out.println(Test.hello); // error パッケージが異なるため不可
    Test.printHello(); // OK パッケージが異なるため不可

    SubTest.subPrintHello(); // => Hello World
  }
}
```

</details>

<br>

<span id="none"></span>
## なし

**同じパッケージのクラス**からのみ使用可能な装飾子。

```java
<static> <組み込み型> <変数名> = <値>;

<static> <返り値の型> <メソッド名>() { ... };
```

<br>

<span id="private"></span>
## private

**現在のクラス内**でのみ使用可能な修飾子。

```java
private <static> <組み込み型> <変数名> = <値>;

private <static> <返り値の型> <メソッド名>() { ... };
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
