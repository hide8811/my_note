# 記号

- [; 《順に実行》](#semicolon)
- [&& 《成功したら次を実行》](#andand)
- [|| 《失敗したら次を実行》](#berber)
- [& 《バックグラウンドで実行》](#and)
- [| 《実行結果を次に渡す》](#pipe)

<br>

<span id='semicolon'></span>
## ;

コマンドを繋げる。順に実行される。

```bash
<コマンド>; <コマンド> ...
```

<details>

```bash
# 複数可
$ echo 'Hello'; echo 'World'; echo '!!!!!'
Hello
World
!!!!!
```

```bash
# 前のコマンドが失敗しても次のコマンドを実行
$ cat hello; echo 'World'
cat: hello: No such file or directory
World
```

</details>

<br>

<span id='andand'></span>
## &&

左側のコマンドが正常に実行されたら、右側のコマンドが実行される。

```bash
<コマンド> && <コマンド> ...
```

<details>

```bash
$ echo 'Hello' && echo 'World'
Hello
World
```

<br>

左側がエラーなどで正常に実行されなかった場合、右側は実行されない。
```bash
$ cat hello && echo 'World'
cat: hello: No such file or directory
```

</details>

<br>

<span id='berber'></span>
## ||

左側のコマンドが正常に実行されなかったら、右側のコマンドが実行される。

```bash
<コマンド> || <コマンド> ...
```

<details>

```bash
$ cat hello || echo 'World'
cat: hello: No such file or directory
World
```

<br>

左側のコードが正常に実行された場合、右側は実行されない。

```bash
$ echo 'Hello' || echo 'World'
Hello
```

</details>

<br>

<span id='and'></span>
## &

前のコマンドをバックグラウンドで実行する。

```bash
<コマンド> & ...
```

<details>

```bash
$ sleep 5 &
[1] 83280

$ jobs
[1]  + running    sleep 20

# 20秒後
$
[1]  + done       sleep 20
```

</details>

<br>

<span id='pipe'></span>
## |

パイプライン。<br>
左側のコマンドの実行結果を、右側のコマンドに渡す。

```bash
<コマンド> | <コマンド> ...
```

<details>

```bash
$ ls
sample_A.txt  sample_B.csv  test_A.txt  test_B.csv

$ ls | grap sample
sample_A.txt
sample_B.csv
```

<br>

複数も可。

```bash
$ ls sample
sample_A.txt  sample_B.csv  test_A.txt  test_B.csv

$ ls sample | tee test.txt | wc -l
4
```

</details>
