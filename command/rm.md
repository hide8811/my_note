# rm

ファイルを削除する。<br>
<span style='color: Crimson;'>
  ※ ゴミ箱には入らず、完全削除される。
</span>

```bash
# text
rm <ファイル名>
```

## オプション

| コマンド | 意味 |
|:--------:|:-----|
| [-f](#f) | 削除確認をしない |
| [-i](#i) | 削除確認をする |
| [-r](#r) | ディレクトリごと削除 |

<details>

別ディレクトリの指定も可。

```bash
rm <ディレクトリ>/<ファイル>
```

ワイルドカードで複数指定も可。

```bash
# 全削除
rm *

rm <ディレクトリ名>/*

# 部分一致
rm *.txt
```

複数指定。

```bash
rm <ファイル名> <ファイル名> <ファイル名>
```

</details>

<!-- -f -------------------------------------------------------------------------- -->
<span id='f'></span>
## -f
削除の前に確認をしない。

```bash
rm -f <ファイル名>
```

<details>

```bash
# before
rm test.txt

=> rm: remove regular file 'test.txt'?
  # 削除するかを確認される。y(yes) or n(no)

# after
rm -f test.txt

=> # 何も表示されず削除完了。
```

</details>

<!-- -i -------------------------------------------------------------------------- -->
<span id='i'></span>
### -i
削除の前に確認を入れる。

```bash
rm -i <ファイル名>
```

<!-- -i -------------------------------------------------------------------------- -->
<span id='r'></span>
### -r
ディレクトリごと削除する。

```bash
rm -r <ディレクトリ名>
```

<details>

```bash
# before
rm test

=> rm: cannot remove 'test': Is a directory

# after
rm -r test

=> rm: descend into directory 'test2'? y
=> rm: remove regular file 'test/test.txt'? y
=> rm: remove directory 'test2'? y
```

</details>

