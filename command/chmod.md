# chmod

**ファイルパーミッション(アクセス許可情報)を変更する。**<br>
<span style="color: gray;">【**ch**ange **mod**e】</span>

```bash
chmod アクセス権限 ファイルA ファイルB ...
```

- [文字列で変更](#string)
- [数値で変更](#integer)
- [オプション](#option)

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

