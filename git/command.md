# git command

- [init 《リポジトリの作成》](#init)

<br>

- [remote 《リモートリポジトリの設定》](#remote)
    - [add 《追加》](#remoteadd)
    - [-v 《確認》](#remote-v)

<br>

- [branch 《ブランチ一覧》](#branch)
    - [-m 《名前変更》](#branch-m)
- [checkout 《ブランチ移動》](#checkout)
    - [-b 《新規作成》](#checkout-b)

<br>

- [add 《インデックスに追加》](#add)
    - [-p 《変更の一部を追加》](#add-p)
- [commit 《リポジトリに保存》](#commit)
    - [-n 《hookのスキップ》](#commit-n)
- [push 《リモートリポジトリに変更を上げる》](#push)
- [pull 《ローカルリポジトリに変更を下ろす》](#pull)

<br>

- [status 《状態確認》](#status)

<br>

- [reset 《addの取り消し》](#reset)
    - [--soft 《コミットの取り消し》](#reset-soft)
    - [--hard 《コミットの削除》](#reset-hard)

<br>

- [stash 《変更を隠す》](#stash)
    - [apply 《復元》](#apply)

<br>

<span id='init'></span>
## inti
リポジトリを作成し、gitを使用できるようにする。

```bash
git init
```

<details>

```bash
$ git init
Initialized empty Git repository in <initコマンドを実行したファイルパス>/.git/
```

</details>

<span id='remote'></span>
## remote

<span id='remoteadd'></span>
### add
ローカルリポジトリにリモートリポジトリを設定・追加する。

```bash
git remote add <リモートリポジトリ名> <リモートリポジトリURL>
```

```bash
git remote add origin https://github.com/<ユーザー名>/<リポジトリ名>.git
```

<span id='remote-v'></span>
### -v
リモートリポジトリのURLを確認する。

```bash
git remote -v
```

---

<span id='branch'></span>
## branch
ブランチの確認。

```bash
git branch
```

<span id='branch-m'></span>
### -m
ローカルブランチ名の変更。

```bash
git branch -m <変更するブランチ> <新しいブランチ名>

# 今のブランチの名前を変更
git branch -m <新しいブランチ名>
```

<span id='checkout'></span>
## checkout
ブランチの切り替え。

```bash
git checkout <ブランチ>
```

<span id='checkout-b'></span>
### -b
新しいブランチを作成して切り替える。

```bash
git checkout -b <新しいブランチ名>
```

---

<span id='add'></span>
## add
ファイルの変更をインデックスに追加する。

```bash
# 全てのファイル
git add .

# 一部のファイル
git add <ファイル名> <ファイル名>
```

<span id='add-p'></span>
### -p
確認しながらインデックスに追加する。

```bash
git add -p <ファイル名>
```

```bash
$ git add -p test.txt
diff --git a/test.txt b/test.txt
index 9daeafb..a6b1ac7 ******
--- a/test.txt
+++ b/test.txt
@@ -1 +1,7 @@
 test
+
+test1
+
+test2
+
+test3
(1/1) Stage this hunk [y,n,q,a,d,e,?]?
```

|  | 意味 |
|:-:|:---|
| **y** | インデックスに追加 |
| **n** | 追加しない |
| **q** | 終了(以降を全て追加しない) |
| **a** | 以降を全て追加 |
| **k** | 戻る |
| **s** | さらに細かく |
| **e** | 手動で編集(vim) |

<span id='commit'></span>
## commit
ファイルの変更をリポジトリに保存する。

```bash
git commit -m '<コミットメッセージ>'

# メッセージを2行
git commit -m '〜を追加' -m '〜するため'
```

<span id='commit-n'></span>
### -n
gitのhookをスキップする。

```bash
git commit -n -m '<コミットメッセージ>'
```

<span id='push'></span>
## push
ローカルリポジトリに保存した変更をリモートリポジトリに送信する。

```bash
git push origin <ブランチ名>
```

<span id='pull'></span>
## pull
リモートリポジトリにある変更内容をローカルリポジトリに受信する。

```bash
git pull
```

<br>

---

<span id='status'></span>
## status
前回のコミットから、addしたファイル・変更したファイル・新規作成したファイルを表示する。

```bash
git status
```

<details>

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test_2.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test_3.txt
```

</details>

<br>

---

<span id='reset'></span>
## reset
git add を取り消す。

```bash
git reset

# ファイル名を指定できる。
git reset <ファイル名>
```

<details>

```bash
# 同じ意味
git reset --mixed HEAD
```

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test.txt

$ git reset
Unstaged changes after reset:
M       test.txt

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

</details>

<br>

HEAD~を指定することで、コミットも取り消すことができる。

```bash
git reset HEAD~
```

<details>

```bash
$ git status -s
M  test.txt

$ git commit -m 'reset test'
[master e141608] reset test
 1 file changed, 1 insertion(+)

$ git log --oneline
e141608 (HEAD -> master) reset test
bc9df75 test commit

$ git reset HEAD~
Unstaged changes after reset:
M       test.txt

$ git log --oneline
bc9df75 (HEAD -> master) test commit

$ git status -s
 M test.txt
```

</details>

<br>

<span id='reset-soft'></span>
### reset --soft
コミットのみを取り消す。<br>
コミットした情報はインデックスに戻る。

```bash
git reset --soft HEAD~
```

<details>

```bash
$ git status -s
M  test.txt

$ git commit -m 'reset test'
[master da160e3] reset test
 1 file changed, 1 insertion(+)

$ git log --oneline
da160e3 (HEAD -> master) reset test
bc9df75 test commit

$ git reset --soft HEAD~

$ git log --oneline
bc9df75 (HEAD -> master) test commit

$ git status -s
M  test.txt
```

</details>

<br>

<span id='reset-hard'></span>
### reset --hard
コミットの削除。<br>
ファイルの変更も消去される。

```bash
git reset --hard HEAD~
```

<details>

```bash
$ git status -s
M  test.txt

$ git commit -m 'reset test'
[master 32d1d50] reset test
 1 file changed, 1 insertion(+)

$ git log --oneline
32d1d50 (HEAD -> master) reset test
bc9df75 test commit

$ git reset --hard HEAD~
HEAD is now at bc9df75 test commit

$ git log --oneline
bc9df75 (HEAD -> master) test commit

$ git status -s

```

</details>

<br>

<span id='stash'></span>
## stash

変更を隠し、一時退避。

```bash
git stash
```

※ `push`が省略されている。

<details>

```bash
$ git status -s
 M test.txt

$ git stash
Saved working directory and index state WIP on test_branch: 0545a60 Add:

$ git status -s
                # 表示されない
```

</details>

<br>

<span id="apply"></span>
### apply

`stash`で隠した変更を復元する。

```bash
git stash apply
```

<details>

```bash
$ git status -s


$ git stash apply
On branch test_branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git status -s
 M test.txt
```

</details>
