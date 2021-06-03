# chmod

**ファイルパーミッション(アクセス許可情報)を変更する。**<br>
<span style="color: gray;">【**ch**ange **mod**e】</span>

```bash
chmod OPTION MODE,MODE,... fileA fileB ...
```

- [文字列で変更](#string)
- [数値で変更](#integer)
- [オプション](#option)
- [特殊なアクセス権](#special)
    - [スティッキービット](#sticky_bit)
    - [SGID](#sgid)
    - [SUID](#suid)
- [パーミッションのデフォルト値の変更【umask】](#umask)

<br>

## ファイルパーミッション

ファイル(ディレクトリ)ごとのアクセス権限。<br>
<span style="color: gray;">【permission】: 許可・許諾・承認</span>

**自分(User)**
・
**グループ(Group)**
・
**他人(Other)**

| 記号 | 意味 |
|:----:|:-----|
| u | 自分 (**u**ser) |
| g | グループ (**g**roup) |
| o | 他人 (**o**ther) |
| a | 全て (**a**ll) |

| 記号 | 数字 | 意味 |
|:----:|:----:|:-----|
| r | 4 | 読み込み (**r**ead) |
| w | 2 | 書き込み (**w**rite) |
| x | 1 | 実行 (e**x**ecute) |
| - | 0 | なし |

<br>

<span id='string'></span>
## 文字列で変更

```bash
chmod  MODE,MODE,... fileA fileB ...

# MODE = [ugoa]+([+-=]([rwx]+|[ugo]))
```
<span style='color: crimson'>※ `MODE`間にスペースは不要</span>

| 記号 | 意味 |
|:----:|:-----|
| + | 権限を付与 |
| - | 権限を除去 |
| = | 権限を臨写 |

<details>

```bash
# +
chmod u+x test.txt  # rw-r--r-- => rwxr--r--

chmod g+u test.txt  # rw-r--r-- => rw-rw-r--
```

```bash
# -
chmod g-r test.txt  # rw-r--r-- => rw----r--

chmod u-g test.txt  # rw-r--r-- => -w-r--r--
```

```bash
# =
chmod g=w test.txt  # rw-r--r-- => rw--w-r--

chmod u=g test.txt  # rw-r--r-- => r--r--r--
```

```bash
# 複数も可
chmod go+w test.txt  # rw-r--r-- => rw-rw-rw-
chmod u-rw test.txt  # rw-r--r-- => ---r--r--
chmod g+w-r test.txt  # rw-r--r-- => rw--w-r--
chmod g+w,o-r test.txt  # rw-r--r-- => rw-rw----
```
</details>

<br>

<span id='integer'></span>
## 数値(8進数)で変更

指定したい権限の数値を足す。<br>
<span style='color: gray;'>例）読み込み(4) + 読み込み(2) => 6</span>

```bash
chmod MODE fileA foleB ...

# MODE = [0-7]{3}
```

<details>

```bash
chmod 751 test.txt  # => rw-r--r-- => rwxr-x--x
```

| 数値 | 意味 | 記号 |
|:----:|:-----|:----:|
| 7 | 読み込み + 書き込み + 実行 | rwx |
| 6 | 読み込み + 書き込み | rw- |
| 5 | 読み込み + 実行 | r-x |
| 4 | 読み込み | r-- |
| 3 | 書き込み + 実行 | -wx |
| 2 | 書き込み | -w- |
| 1 | 実行 | --x |
| 0 | 権限なし | --- |

</details>

<br>

<span id='option'></span>
## オプション

|   | 意味 |
|:-:|:----:|
| -c | 変更のあった処理を出力 |
| -v | 全ての処理を出力 |
| --reference=参照ファイル | 参照ファイルと同じパーミッションに変更 |
| -R | ディレクトリ内のファイルも同時に変更 |

### -c

```bash
chmod -c MODE file
```

<details>

```bash
$ chmod -c g+w test.txt
mode of 'test.txt' changed from 0644 (rw-r--r--) to 0664 (rw-rw-r--)
```

```bash
$ chmod -c u+w test.txt
# 変更なし
```

</details>

<br>

### -v

```bash
chmod -v MODE file
```

<details>

```bash
$ chmod -v g+w test.txt
mode of 'test.txt' changed from 0644 (rw-r--r--) to 0664 (rw-rw-r--)
```

```bash
$ chmod -v u+r test.txt
mode of 'test.txt' retained as 0644 (rw-r--r--)
```

</details>

<br>

### --reference=参照ファイル

```bash
chmod --reference=fileR fileA
```

<details>

```bash
$ ls -l
-rw-rw-rw- x user group xxx xx xx xx:xx sample.txt
-rw-r--r-- x user group xxx xx xx xx:xx test.txt

$ chmod --reference=sample.txt test.txt  # rw-r--r-- => rw-rw-rw-

$ ls -l
-rw-rw-rw- x user group xxx xx xx xx:xx sample.txt
-rw-rw-rw- x user group xxx xx xx xx:xx test.txt
```

</details>

<br>

### -R

```bash
chmod -R MODE directory
```

<details>

```bash
$ ls -lR
drwxr-xr-x x user group xxx xx xx xx:xx sample

./sample:
-rw-r--r-- x usre group xxx xx xx xx:xx sample.txt
-rw-r--r-- x usre group xxx xx xx xx:xx test.txt

$ chmod -R 111 sample

$ ls -lR
d--x--x--x x user group xxx xx xx xx:xx sample

./sample:
---x--x--x x usre group xxx xx xx xx:xx sample.txt
---x--x--x x usre group xxx xx xx xx:xx test.txt
```

</details>

<br>

<span id='special'></span>
## 特殊なアクセス権

| 記号 | 数値 | 名前 | 意味 |
|:----:|:----:|:----:|:-----|
| t (other) | 1000 | スティッキービット(Sticky Bit) | 所有者(とroot)以外は削除不可 |
| s (group) | 2000 | SGID (Set Group ID) | 実行時、所有グループ権限で実行 |
| s (user) | 4000 | SUID (Set User ID) | 実行時、所有者権限で実行 |

<br>

<span id='sticky_bit'></span>
### スティッキービット (Sticky Bit)

所有者とroot以外は削除ができない。<br>
記号はその他(other)に`t`。

drwxrwxrw<span style='color: mediumvioletred;'>t</span>

```bash
# 文字列
chmod o+t file
```

```bash
# 数値
chmod 1xxx file
```

<br>

<span id='sgid'></span>
### SGID (Set Group ID)

この実行権があるファイルを実行すると、所有グループの権限で実行される。<br>
記号はグループ(group)に`s`

-rwxr-<span style='color: mediumvioletred;'>s</span>r-x

```bash
# 文字列
chmod g+s file
```

```bash
# 数値
chmod 2xxx file
```

<br>

<span id='suid'></span>
### SUID (Set User ID)

この実行権があるファイルを実行すると、所有者(User)の権限で実行される。<br>
記号はユーザー(user)に`s`

-rw<span style='color: mediumvioletred;'>s</span>r-xr-x

```bash
# 文字列
chmod u+s file
```

```bash
# 数値
chmod 4xxx file
```

<br>

<span id='umask'></span>
## パーミッションのデフォルト値

ファイルやディレクトリを新規作成した際のデフォルトのパーミッションは、<br>
`umask`コマンドで、確認・変更ができる。

```bash
# 確認
umask
```

```bash
# 変更
umask 値
```

ファイル`666`・ディレクトリ`777`から、`umask`の値を引いたものがデフォルトのパーミッションになる。

<details>

`umask => 022`

**ディレクトリの場合**<br>
`777 - 022 => 755`

```bash
$ umask
022

$ mkdir sample

$ ls -l
drwxr-xr-x user group xxx x xx xx:xx sample
```

<br>

**ファイルの場合**<br>
`666 - 022 => 644`

```bash
$ umask
022

$ touch sample.txt

$ ls -l
-rw-r--r-- user group xxx x xx xx:xx sample.txt
```

</details>


