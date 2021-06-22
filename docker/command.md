# Docker コマンド

- [イメージ](#image)
    - [images《一覧表示》](#images) 
    - [pull 《取得》](#pull)
    - [rmi 《削除》](#rmi)
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

<span id='container'></span>
## Dockerコンテナ

<span id='run'></span>
### run

Dockerコンテナを作成し、起動する。<br>
`create` + `start` と同じ。

```bash
docker run <オプション> <イメージ>
```

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
| -a | 全て表示 |

<details>

```bash
$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
e84f4f752daf   ruby      "irb"                    6 seconds ago   Up 6 seconds             kind_leavitt
3067f9179fab   nginx     "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   80/tcp    infallible_volhard
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
