# マイグレーション
[Railsガイド](#https://railsguides.jp/active_record_migrations.html)

- [モデルの作成(g model)](#g-model)
- [マイグレーションファイルの作成(g maigration)](#g-maigration)
    - [カラムの追加(add_column)](#add_column)
- [実行(db:migrate)](#db-migrate)
- [状態確認(status)](#status)
- [戻す(rollback)](#rollback)

<span id='g-model'>
## g model
モデルを作成する。

```bash
rails g model <モデル名> <カラム名>:<データ型> <カラム名>:<データ型>
```
<span style='padding: 0 .5rem; border: thin solid;'>モデル名</span> 先頭大文字・キャメルケース・<u>**単数形**</u> (先頭小文字・スネークケースでも可)

<details>

```bash
$ rails g model User name:string
Running via Spring preloader in process 20
      invoke  active_record
      create    db/migrate/**************_create_users.rb
      create    app/models/user.rb
```

```ruby
# db/migrate/**************_create_users.rb

class CreateUsers < ActiveRecord::Migration[6.1]
  def change
    create_table :users do |t|
      t.string :name

      t.timestamps
    end
  end
end
```
</details>

<br>

<span id='g-maigration'></span>
## g maigrate
マイグレーションファイルを作成。

```bahs
rails g maigration <マイグレーション名> <カラム名>:<データ型> <カラム名>:<データ型>
```

<br>

<span id='add_column'></span>
### add_column
カラムを追加する。

```bash
rails g maigration Add<カラム名>To<テーブル名>
```
```ruby
# db/migrate/**************_add_<カラム名>_to_<テーブル名>.rb

class <マイグレーション名> < ActiveRecord::Migration[6.1]
  def change
    add_column :<テーブル名>, :<カラム名>, :<カラム型>
  end
end
```

<details>

```bash
$ rails g migration AddBirthdayToUsers birthday:date
Running via Spring preloader in process 20
      invoke  active_record
      create    db/migrate/**************_add_birthday_to_users.rb
```
```ruby
# db/migrate/**************_add_birthday_to_users.rb

class AddBirthdayToUsers < ActiveRecord::Migration[6.1]
  def change
    add_column :users, :birthday, :date
  end
end
```

</details>

<br>

<span id='db-migrate'></span>
## db:migrate
マイグレーションファイルの実行。

```bash
rails db:migrate
```

<details>

```bash
$ rails db:migrate
== ************** AddBirthdayToUsers: migrating ===============================
-- add_column(:users, :birthday, :date)
   -> 0.0483s
== ************** AddBirthdayToUsers: migrated (0.0504s) ======================
```

</details>

<span id='status'></span>
## db:migrate:status
マイグレーションファイルの状態確認。

```bash
rails db:migrate:status
```

<details>

```bash
$ rails db:migrate:status

database: myapp_development

 Status   Migration ID    Migration Name
--------------------------------------------------
   up     **************  Create users
   up     **************  Add birthday to users

```

</details>

<br>

<span id='rollback'></span>
## db:rollback
マイグレーションファイルを戻す。<br>
`Status`が`up`から`down`になる。

```bash
rails db:rollback STEP=n
```
<span style='padding: 0 .5rem; border: thin solid;'>STEP</span> **n**個前のマイグレーションファイルまで戻す。デフォルトは**1**。

<details>

```bash
$ rails db:migrate:status

database: myapp_development

 Status   Migration ID    Migration Name
--------------------------------------------------
   up     **************  Create users
   up     **************  Add birthday to users


$ rails db:rollback
== ************** AddBirthdayToUsers: reverting ===============================
-- remove_column(:users, :birthday, :date)
   -> 0.0345s
== ************** AddBirthdayToUsers: reverted (0.0466s) ======================


$ rails db:migrate:status

database: myapp_development

 Status   Migration ID    Migration Name
--------------------------------------------------
   up     **************  Create users
  down    **************  Add birthday to users

```

</details>

