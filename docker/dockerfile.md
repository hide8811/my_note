# Dockerfile

- [FROM](#from)
- [RUN](#run)
- [ARG](#arg)
- [ENV](#env)

Dockerイメージの設計図。<br>
Dockerfileを元にDockerイメージが構築(build)される。

<span id="from"></span>
## FROM

ベースイメージの指定。

```docker
FROM <イメージ>
```

<span id="run"></span>
## RUN

`docker build`時に実行するコマンドを指定。

```docker
RUN <コマンド>
```

<span id="arg"></span>
## ARG

`build`で使用する変数を**外部から受け取る**。<br>
`Dockerfile`内でのみ使用可。<br>
コンテナ内では使用できない。

```docker
ARG <変数>
```

<details>

```docker
# ARG なし
FORM nginx
RUN echo $HELLO
```

```bash
$ docker buld --build-arg HELLO="World" .
...
# 略
...
=> CACHED [2/2] RUN echo ${HELLO}
...
# 略
...

```

<br>

```docker
# ARG あり
FORM nginx
ARG HELLO
RUN echo $HELLO
```

```bash
$ docker buld --build-arg HELLO="World" .
...
# 略
...
=> CACHED [2/2] RUN echo World
...
# 略
...

```

</details>

<br>

<span id="env"></span>
## ENV

コンテナ内で使用する環境変数を指定。

```docker
ENV <変数>:<値>
```

<details>

```docker
FORM nginx

ENV HELLO="World"
```

```bash
$ docker build -t env_test .
# 略

$ docker run -it env_test bash
root@b9f2cbb47393:/# echo $HELLO
World
```

</details>
