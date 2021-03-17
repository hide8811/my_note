# SQL文

- [MySQLにログイン( mysql ••• )](#mysql)
- [データベースの一覧( SHOW DATABASES; )](#show_d)
- [データベースの選択( USE •••; )](#use)
    - [使用中データベースの確認( SELECT DATABASE(); )](#select_d)
- [テーブルの一覧( SHOW TABLES; )](#show_t)

- [データの一覧( SELECT ••• FROM •••; )](#select_from)


<span id='mysql'><span>
## mysql •••
Mysqlにログインする。

```bash
mysql -u <ユーザー名> -p

# docker使用時
mysql -u <ユーザー名> -p -h <ホスト名(サービス名)> -P <ポート番号>
```

<details>

実行結果

```bash
$ mysql -u root -p
Enter password:    # パスワードを入力
```

**【オプション】**

| オプション | 意味 |
| ---------- | ---- |
| -u | ユーザー名を指定 |
| -p | パスワードを入力 |
| -h | ホスト名を指定 |
| -P | ポート番号を指定 |

</details>

<br>

<span id='show_d'></span>
## SHOW DATABASES;
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

<br>

<span id='use'></span>
## USE •••;
操作するデータベースを選択する。

```SQL
USE <データベース名>;
```

<br>

<span id=select_d></span>
### SELECT DATABASE();
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

<br>

<span id='show_t'></span>
## SHOW TABLES;
テーブル一覧の表示。

データベース選択時
```SQL
SHOW TABLES;
```

<br>

データベース未選択時
```SQL
SHOW TABLES FROM <テーブル名>;
```

<details>

実行結果(Rails [myapp])
```SQL
MySQL [myapp_development]> SHOW TABLES;
+-----------------------------+
| Tables_in_myapp_development |
+-----------------------------+
| ar_internal_metadata        |
| books                       |
| messages                    |
| schema_migrations           |
| users                       |
+-----------------------------+
7 rows in set (0.003 sec)
```

</details>

<br>

<span id='select_from'></span>
## SELECT ••• FROM •••;
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
