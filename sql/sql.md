# SQL文

- [データベースの一覧(SHOW)](#show_d)
- [データベースの選択(USE)](#use)
    - [使用中データベースの確認(SELECT)](#select_d)
- [テーブルの一覧(SHOW)](#show_t)

- [データの一覧(SELECT FROM)](#select_from)


<span id='show_d'></span>
## SHOW
データベースの一覧を確認する。

```SQL
SHOW DATABASES;
```

<details>
実行結果(mysql + rails)

```bash
+--------------------+
| Database           |
+--------------------+
| information_schema |
| app_development    |
| app_test           |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
```
</details>

<span id='use'></span>
### USE
操作するデータベースを選択する。

```SQL
USE <データベース名>;
```

<span id=select_d></span>
### SELECT DATABASE()
使用中のデータベースを確認する。

```SQL
SELECT database();
```

<details>

```SQL
-- データベース未選択

mysql> SELECT database();
+------------+
| database() |
+------------+
| NULL       |
+------------+
1 row in set (0.00 sec)

-- データベースを選択

mysql> USE test;
Database changed

mysql> SELECT database();
+------------+
| database() |
+------------+
| test       |
+------------+
1 row in set (0.00 sec)
```

</details>

<span id='select_from'></span>
## SELECT FROM
データを確認する。

```SQL
SELECT <カラム名> FROM <テーブル名>;
```

カラム名を`*`にすることで全データを取得できる。

```SQL
SELECT * FROM users;
```

<details>

実行結果。

【データが存在するとき】

```SQL
+----+---------+------+------------+----------------------------+----------------------------+
| id | name    | age  | birthday   | created_at                 | updated_at                 |
+----+---------+------+------------+----------------------------+----------------------------+
|  1 | xx xx   | xx   | xxxx-xx-xx | xxxx-xx-xx xx:xx:xx.xxxxxx | xxxx-xx-xx xx:xx:xx.xxxxxx |
|  2 | xx xx   | xx   | xxxx-xx-xx | xxxx-xx-xx xx:xx:xx.xxxxxx | xxxx-xx-xx xx:xx:xx.xxxxxx |
|  3 | xx xxx  | NULL | xxxx-xx-xx | xxxx-xx-xx xx:xx:xx.xxxxxx | xxxx-xx-xx xx:xx:xx.xxxxxx |
|  4 | xx xx   | xx   | xxxx-xx-xx | xxxx-xx-xx xx:xx:xx.xxxxxx | xxxx-xx-xx xx:xx:xx.xxxxxx |
|  5 | xxx xx  | NULL | xxxx-xx-xx | xxxx-xx-xx xx:xx:xx.xxxxxx | xxxx-xx-xx xx:xx:xx.xxxxxx |
+----+---------+------+------------+----------------------------+----------------------------+
5 rows in set (0.001 sec)
```

<br>
【データが存在しないとき】

```SQL
Empty set (0.003 sec)
```

</details>