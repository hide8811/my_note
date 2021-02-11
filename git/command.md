# git command

<span id=''></span>

- [remote](#remote)
    - [リモートリポジトリの設定(add)](#remoteadd)
    - [リモートリポジトリの確認(-v)](#remote-v)

---

- [ブランチ確認(branch)](#branch)
    - [名前変更(-m)](#branch-m)
- [ブランチ移動(checkout)](#checkout)
    - [新しいブランチ(-b)](#checkout-b)

---

- [インデックスに追加(add)](#add)
- [リポジトリに保存(commit)](#commit)
    - [hookのスキップ(-n)](#commit-n)
- [リモートリポジトリに変更を上げる(push)](#push)
- [ローカルリポジトリに変更を下ろす(pull)](#pull)

---
---

<span id='remote'></span>
## remote

<span id='remoteadd'></span>
### add
ローカルリポジトリにリモートリポジトリを設定・追加する。

```sh
git remote add <リモートリポジトリ名> <リモートリポジトリURL>
```

```sh
git remote add origin https://github.com/<ユーザー名>/<リポジトリ名>.git
```

<span id='remote-v'></span>
### -v
リモートリポジトリのURLを確認する。

```sh
git remote -v
```

---

<span id='branch'></span>
## branch
ブランチの確認。

```sh
git branch
```

<span id='branch-m'></span>
### -m
ローカルブランチ名の変更。

```sh
git branch -m <変更するブランチ> <新しいブランチ名>

# 今のブランチの名前を変更
git branch -m <新しいブランチ名>
```

<span id='checkout'></span>
## checkout
ブランチの切り替え。

```sh
git checkout <ブランチ>
```

<span id='checkout-b'></span>
### -b
新しいブランチを作成して切り替える。

```sh
git checkout -b <新しいブランチ名>
```

---

<span id='add'></span>
## add
ファイルの変更をインデックスに追加する。

```sh
# 全てのファイル
git add .

# 一部のファイル
git add <ファイル名> <ファイル名>
```

<span id='commit'></span>
## commit
ファイルの変更をリポジトリに保存する。

```sh
git commit -m '<コミットメッセージ>'

# メッセージを2行
git commit -m '〜を追加' -m '〜するため'
```

<span id='commit-n'></span>
### -n
gitのhookをスキップする。

```sh
git commit -n -m '<コミットメッセージ>'
```

<span id='push'></span>
## push
ローカルリポジトリに保存した変更をリモートリポジトリに送信する。

```sh
git push origin <ブランチ名>
```

<span id='pull'></span>
## pull
リモートリポジトリにある変更内容をローカルリポジトリに受信する。

```sh
git pull
```
