# Docker コマンド

- [イメージ](#image)
    - [images《一覧表示》](#images) 
    - [pull 《取得》](#pull)
    - [rmi 《削除》](#rmi)
- [コンテナ](#container)
    - [run](#run)

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
