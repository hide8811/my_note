# コンストラクタ

インスタンス生成時に呼び出されるメソッド。

```java
class <クラス名> {
  public <クラス名>() {
    // 処理
  }
}
```

- コンストラクタはクラス名と同一
- 変数の初期化など、インスタンス作成時に実行する処理を記述

<details>

```java
class Person {
  public String name; // 変数を宣言

  // コントラクタ
  public Person(String name) {
    this.name = name;  // インスタンスの変数nameに、引数nameを代入
    System.out.println(this.name + "のインスタンスが作成されました");
  }
}
```

```java
class Main {
  public static void main(String[] args) {
    Person person1 = new Person("person1");

    Person person2 = new Person("person2");

    Person person3 = new Person("person3");
  }
}
```

```bash
# 実行
person1のインスタンスが作成されました
person2のインスタンスが作成されました
person3のインスタンスが作成されました
```

</details>

<br>

## this()

コントラクタ内からコントラクタを呼び出す。

```java
public <クラス名>(<引数1>, <引数2>) {
  // 処理
}

public <クラス名>(<引数1>, <引数2>, <引数3>) {
  this(<引数1>, <引数2>);
  // 処理
}
```

<details>

```java
class Person {
  private String name;
  private int age;
  private double weight;

  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }

  public Person(String name, int age, double weight) {
    this(name, age); // 上のコントラクタを呼び出している

    this.weight = weight; // 新しいデータ
  }

  public void printData() {
    System.out.println("name: " + this.name);
    System.out.println("age: " + this.age);

    if (weight != 0.0) System.out.println("weight: " + this.weight);
  }
}
```

```java
class Main {
  public static void main(String[] args) {
    Person person1 = new Person("person1", 25);
    person1.printData();

    System.out.println("---");

    Person person2 = new Person("person2", 30, 75.4);
    person2.printData();
  }
}
```

```bash
# 実行
name: person1
age: 25
---
name: person2
age: 30
weight: 75.4
```

</details>

<br>

## this

自身のインスタンスそのものを表す。

```java
this.<変数名>
```

<details>

```java
class Person {
  private String name;

  public Person(String name) {
    this.name = name;
  }

  public void printData() {
    String name = "test"; // printDataメソッドのローカル変数
    System.out.println("name: " + name); // ローカル変数nameを出力
    System.out.println("this.name: " + this.name); // インスタンスの変数nameを出力
  }
}
```

```java
class Main {
  public static void main(String[] args) {
    Person person1 = new Person("person1");
    person1.printData();
  }
}
```

```bash
# 実行
name: test
this.name: person1
```

</details>
