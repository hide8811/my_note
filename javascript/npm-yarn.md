# npm yarn コマンド

| npm | yarn | 機能 |
|:----|:-----|:-----|
| init | init | `package.json`の作成 |
| install<br>i | install | `package.json`をもとにパッケージのインストール |
| install [パッケージ]<br>i [パッケージ] | add [パッケージ] | パッケージを指定してインストール |
| ls | list | インストールしたパッケージの一覧 |
| uninstall [パッケージ] | remove [パッケージ] | パッケージの削除 |
|  | yarn set varsion latest | パッケージマネージャー自身のアップデート |

## npm

### npm init

#### -y

全て`yes`で実行

```
npm init -y
```

### npm install

dependencies: 本番環境<br>
devDependencies: 開発環境<br>
optionalDependencies: インストールが失敗してもnpmは止まらない

#### -P (--save-prod)

デフォルト `dependencies`に保存。

#### -D (--save-dev)

`devDependencies`に保存。

### `package.json`のアップデート

`npx -p npm-check-updates ncu -u`

## yarn
