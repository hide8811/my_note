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
chmod [ugoa]+([+-=]([rwx]+|[ugo])) fileA fileB ...
```

| 記号 | 意味 |
|:----:|:-----|
| + | 権限を付与 |
| - | 権限を除去 |
| = | 権限を臨写 |

<details>

```bash
# +
chmod u+x test.txt  # rw-r--r-- => rwxr--r--
```

```bash
# -
chmod g-r test.txt  # rw-r--r-- => rw----r--
```

```bash
# =
chmod u=g test.txt  # rw-r--r-- => r--r--r--
```
</details>
