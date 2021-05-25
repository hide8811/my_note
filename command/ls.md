# ls

ファイルやディレクトリの一覧表示。<br>
`list segments`の略。

```bash
ls -オプション ディレクトリ
```

<details>

```bash
$ ls
image.jpeg  memo.txt  sample  test.md
```

```bash
$ ls sample
example.md  sample.txt
```

</details>

## オプション

| コマンド | 意味 |
|:--------:|:----:|
| [-a](#a) | 隠しファイルも表示 |
| [-A](#A) | 同上 (`.``..`を除外) |
| [-l](#l) | 長いフォーマット表示 |

<br>

<span id='a'></span>
### -a

隠しファイル(先頭に`.`がついたファイル)も表示。

```bash
ls -a
```

<details>

```bash
$ ls -a
.  ..  .hide  .secret_file.pdf  image.jpeg  memo.txt  sample  test.md
```

</details>

<br>

<span id='A'></span>
### -A

隠しファイル(先頭に`.`がついたファイル)も表示するが、<br>
`.`(カレントディレクトリ)と`..`(親ディレクトリ)は除外。

```bash
ls -A
```

<details>

```bash
$ ls -A
.hide  .secret_file.pdf  image.jpeg  memo.txt  sample  test.md
```

</details>

<br>

<span id='l'></span>
### -l

長いフォーマットを表示。

```bash
ls -l
```

```bash
# 出力結果
drwxr-xr-x 4 user staff 128  5 24 00:00 sample
```

| 表記 | 意味 |
|:----:|:-----|
| d | 種類 |
| rwxr-xr-x | パーミッション (user/group/other) |
| 4 | ハードリンク数 |
| user | 所有者 |
| staff | グループ |
| 128 | サイズ |
| 5 24 00:00 | 最終更新日 |
| sample | 名前 |

<br>

#### 追加オプション

| 表記 | 意味 |
|:----:|:-----|
| -h | サイズを見やすく表示(例: 1k) |
| -c | 日付に属性変更日を表示 |
| -u | 日付に最終アクセス日を表示 |

<details>

```bash
$ ls -l
total 24
-rw-r--r-- 1 user staff 17754  5 24 23:20 image.jpeg
-rw-r--r-- 1 user staff    54  5 24 23:36 memo.txt
drwxr-xr-x 4 user staff   128  5 24 23:15 sample
-rw-r--r-- 1 user staff     0  5 24 23:08 test.md
```

<br>

#### 種類

| 表記 | 意味 |
|:----:|:-----|
| - | ファイル |
| d | ディレクトリ |
| \| | シンボリックリンク(ショートカット・エイリアス) |

<br>

#### パーミッション

所有者(user)/グループ(group)/他(other)

| 表記 | 意味 |
|:----:|:-----|
| - | 許可なし |
| r | 読み込み **r**ead |
| w | 書き込み **w**rite |
| x | 実行 e**x**ecute |

</details>
