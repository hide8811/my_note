# Docker コマンド

- [イメージ](#image)
    - [images《一覧表示》](#images) 
    - [pull 《取得》](#pull)
    - [rmi 《削除》](#rmi)
    - [build 《作成》](#build)
- [コンテナ](#container)
    - [run 《作成 + 起動》](#run)
    - [ps 《一覧》](#ps)
    - [rm 《削除》](#rm)
- [prune 《全削除》](#prune)
    - [system prune](#system_prune)
    - [image prune](#image_prune)

<br>

<span id='image'></span>
## Dockerイメージ

<span id='images'></span>
### images

Dockerイメージの一覧を表示。

```bash
docker images
```

`REPOSITORY`や`TAG`で絞り込みも可。

```bash
docker images <リポジトリ名>
docker images <リポジトリ名>:<タグ>
```

<details>

```bash
$ docker images
REPOSITORY    TAG      IMAGE ID       CREATED        SIZE
nginx         latest    d1a364dc548d   2 weeks ago    133MB
hello-world   latest    d1165f221234   3 months ago   13.3kB
hello-world   linux     d1165f221234   3 months ago   13.3kB
```

```bash
$ docker images hello-world
REPOSITORY    TAG      IMAGE ID       CREATED        SIZE
hello-world   latest    d1165f221234   3 months ago   13.3kB
hello-world   linux     d1165f221234   3 months ago   13.3kB
```

</details>

<br>

<span id='pull'></span>
### pull

Dockerイメージを、[Docker Hub](https://hub.docker.com/)のレジストリから取得。

```bash
docker pull <リポジトリ名>:<タグ>
```

※ `<TAG>`を省略すると`latest`を取得。

<details>

```bash
$ docker pull hello-world
```
```bash
$ docker pull hello-world:linux
```

</details>

<br>

<span id='rmi'></span>
### rmi

Dockerイメージを削除。

```bash
docker rmi <リポジトリ名>
docker rmi <イメージID>
```

<details>

```bash
$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
nginx         latest    d1a364dc548d   2 weeks ago    133MB
hello-world   latest    d1165f221234   3 months ago   13.3kB
hello-world   linux     d1165f221234   3 months ago   13.3kB
```

```bash
$ docker rmi hello-world
Untagged: hello-world:latest

$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
nginx         latest    d1a364dc548d   2 weeks ago    133MB
hello-world   linux     d1165f221234   3 months ago   13.3kB
```

</details>

<br>

<span id='build'></span>
### build

`Dockerfile`からイメージを作成する。

```bash
docker build <Dockerfileのあるパス>
```

| オプション | 意味 |
|:----------:|:-----|
| [-f <ファイル名>](#build_file) | Dockerfileの指定 |
| [-t <リポジトリ>:<タグ>](#build_tag) | リポジトリ名とタグを指定 |

<details>

カレントディレクトリに`Dockerfile`がある場合

```bash
$ ls
Dockerfile

$ docker build .
```

<br>

<span id='build_file'></span>
#### -f (--file)

`Dockerfile`を指定できる。<br>
デフォルトは`Dockerfile`

```bash
$ ls
Dockerfile  Dockerfile_httpd

$ cat Dockerfile
FROM nginx

$ cat Dockerfile_httpd
FROM httpd

$ docker build .
[+] Building 0.2s (5/5) FINISHED
 => [internal] load build definition from Dockerfile
 .
 .
 .

$ docker build -f Dockerfile_httpd .
[+] Building 0.2s (5/5) FINISHED
 => [internal] load build definition from Dockerfile_httpd
 .
 .
 .
```

<br>

<span id='build_tag'></span>
#### -t (--tag)

`build`時に、リポジトリ名やタグを指定する。

```bash
$ docker build .
.
.
.

$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
<none>       <none>    1e80f1d15656   7 days ago   133MB
```

```bash
$ docker build -t tag_test .
.
.
.

$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
tag_test     latest    1e80f1d15656   7 days ago   133MB
```

</details>

<br>

<span id='container'></span>
## Dockerコンテナ

<span id='run'></span>
### run

Dockerコンテナを作成し、起動する。<br>
`create` + `start` と同じ。

```bash
docker run <オプション> <イメージ>
```

| オプション | 意味 |
|:----------:|:-----|
| [**-it**](#run-it) | 擬似ターミナルで標準入力可能に (-i + -t) |
| [**--rm**](#run-rm) | コンテナ終了時、自動削除 |
| [**--name** <名前>](#run-name) | コンテナ名を付ける |
| [**-p** <ホスト側>**:**<コンテナ側>](#run-p) | ポートを繋ぐ |

<details>

```bash
$ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
.
.
.
```

<br>

<span id='run-it'></span>
#### -it (-i -t)

擬似ターミナルで標準入力を可能にする。<br>
コンテナ内に入る際などに使用。<br>
`-i (--interactive)`と`-t (--tty)`の同時指定。

```bash
$ docker run nginx bash

$ docker run -it nginx bash
root@1cf3db35c7ce:/#
```

<br>

<span id='run-rm'></span>
#### --rm

コンテナが停止するとそのまま削除される。<br>
このオプションを指定しないと、`run`コマンドをするたび、新しいコンテナが作成されてしまう。

```bash
$ docker ps -a -f "ancestor=nginx"
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

$ docker run nginx echo "Hello"
Hello

$ docker ps -a -f "ancestor=nginx"
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS                     PORTS     NAMES
4195fc0e6062   nginx     "/docker-entrypoint.…"   2 seconds ago   Exited (0) 2 seconds ago             jolly_cerf

$ docker run nginx echo "Hello"
Hello

$ docker ps -a -f "ancestor=nginx"
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS                     PORTS     NAMES
15ae29993e69   nginx     "/docker-entrypoint.…"   3 seconds ago   Exited (0) 2 seconds ago             sharp_lewin
4195fc0e6062   nginx     "/docker-entrypoint.…"   9 seconds ago   Exited (0) 8 seconds ago             jolly_cerf

$ docker run --rm nginx echo "Hello"
Hello

$ docker ps -a -f "ancestor=nginx"
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS     NAMES
15ae29993e69   nginx     "/docker-entrypoint.…"   12 seconds ago   Exited (0) 11 seconds ago             sharp_lewin
4195fc0e6062   nginx     "/docker-entrypoint.…"   18 seconds ago   Exited (0) 17 seconds ago             jolly_cerf
```

<br>

<span id='run-name'></span>
#### --name

コンテナに任意の名前を付ける。<br>
このオプションがない場合、自動でつけられる。

```bash
$ docker run --name hello_nginx nginx echo "Hello"
Hello

$ docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS                     PORTS     NAMES
15ce4430a102   nginx     "/docker-entrypoint.…"   3 seconds ago   Exited (0) 2 seconds ago             hello_nginx
```

<br>

<span id='run-p'></span>
#### -p

ポートを公開しバインド。

```bash
$ docker run nginx

$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
cbd4c750c398   nginx     "/docker-entrypoint.…"   3 seconds ago   Up 3 seconds   80/tcp    pensive_mcclintock

# localhost:80 => このサイトにアクセスできません
```

```bash
$ docker run -p 80:80

$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                               NAMES
ca60a8675a0a   nginx     "/docker-entrypoint.…"   6 seconds ago   Up 4 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   unruffled_meninsky

# localhost:80 => Welcome to nginx!
```

</details>

<br>

<span id='ps'></span>
### ps

実行中のコンテナの一覧を表示。

```bash
docker ps
```

| オプション | 意味 |
|:----------:|:-----|
| [-a](#ps-a) | 全て表示 |
| [-f <フィルタ>=<値>](#ps-f) | フィルタリング |
| [--format "{{.<出力するフォーマット>}}"](#ps-format) | 出力整形 |

| フィルタ | 値 | 意味 |
|:--------:|:---|:-----|
| name | コンテナ名 |
| ancestor | イメージ名(:タグ)、イメージID |
| before | コンテナ名、コンテナID | 値のコンテナよりも**前**に作成されたもの |
| since | コンテナ名、コンテナID | 値のコンテナよりも**後**に作成されたもの |

| フォーマット | 意味 |
|:------------:|:----:|
| ID | コンテナID |
| Image | イメージID |
| Names | コンテナ名 |

<details>

```bash
$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
e84f4f752daf   ruby      "irb"                    6 seconds ago   Up 6 seconds             kind_leavitt
3067f9179fab   nginx     "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   80/tcp    infallible_volhard
```

<br>

<span id='ps-a'></span>
#### -a (--all)

通常の`ps`コマンドは実行中のコンテナしか見ることができない。<br>
`-a`(`--all`)オプションで停止中のコンテナも見ることができる。

```bash
$ docker ps
CONTAINER ID   IMAGE     COMMAND              CREATED              STATUS              PORTS                               NAMES
0c0f6434bf7f   httpd     "httpd-foreground"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, :::80->80/tcp   apache_test

$ docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS                               NAMES
0c0f6434bf7f   httpd     "httpd-foreground"       4 minutes ago    Up 4 minutes                0.0.0.0:80->80/tcp, :::80->80/tcp   apache_test
e619307928ac   nginx     "/docker-entrypoint.…"   11 minutes ago   Exited (0) 10 minutes ago                                       nginx_test
```

<br>

<span id='ps-f'></span>
#### -f (--filter)

`-f`(`--filter`)オプションで、表示結果のフィルタリングが可能

```bash
docker ps -f "<フィルタ><値>" -f "<フィルタ><値>" ...
```

複数フィルタリング可。`"`の省略可。

```bash
$ docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                          PORTS     NAMES
24405ab922e5   ruby      "irb"                    47 seconds ago   Exited (0) 46 seconds ago                 ruby_test
0c0f6434bf7f   httpd     "httpd-foreground"       7 minutes ago    Exited (0) About a minute ago             apache_test
e619307928ac   nginx     "/docker-entrypoint.…"   13 minutes ago   Exited (0) 13 minutes ago                 nginx_test

$ docker ps -a -f "name=nginx_test"
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS     NAMES
e619307928ac   nginx     "/docker-entrypoint.…"   13 minutes ago   Exited (0) 13 minutes ago             nginx_test

$ docker -a -f name=nginx_test -f name=ruby_test
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS     NAMES
24405ab922e5   ruby      "irb"                    12 minutes ago   Exited (0) 12 minutes ago             ruby_test
e619307928ac   nginx     "/docker-entrypoint.…"   25 minutes ago   Exited (0) 25 minutes ago             nginx_test

```

<br>

<span id='ps-format'></span>
#### --format

Goテンプレートで出力結果のフォーマットを指定。

```bash
$ docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED        STATUS                    PORTS     NAMES
15ce4430a102   nginx     "/docker-entrypoint.…"   24 hours ago   Exited (0) 24 hours ago             nginx_test
68eccedc2f88   ruby      "irb"                    24 hours ago   Exited (0) 24 hours ago             hello_ruby
0c0f6434bf7f   httpd     "httpd-foreground"       25 hours ago   Exited (0) 25 hours ago             apache_test

$ docker ps -a --format "{{.Names}}"
nginx_test
hello_ruby
apache_test
```

</details>

<br>

<span id='rm'></span>
### rm

コンテナの削除。

```bash
docker rm <コンテナ>
```

<br>

<span id='prune'></span>
## 全削除

<span id='system_prune'></span>
### system prune

- イメージ（未参照・タグ付けなし）
- コンテナ（停止中）
- ネットワーク（未使用）

を削除する。

```bash
docker system prune
```

| オプション | 意味 |
|:----------:|:-----|
| --volumes | ボリュームも削除 |

<br>

<span id='image_prune'></span>
### image prune

タグがなく、コンテナから参照されていないイメージを全削除。

```bash
docker image prune
```
