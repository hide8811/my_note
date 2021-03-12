# マイグレーション
[Railsガイド](#https://railsguides.jp/active_record_migrations.html)

- [モデルの作成(g model)](#g-model)
- [マイグレーションファイルの作成(g migration)](#g-migration)
    - [カラムの追加(add_column)](#add_column)
    - [カラムの削除(remove_column)](#remove_column)
- [実行(db:migrate)](#db-migrate)
- [状態確認(status)](#status)
- [戻す(rollback)](#rollback)

<span id='g-model'></span>
## g model
モデルを作成する。

<span style='font-weight: bold; color: darkcyan;'>rails g model</span> <span style='color: gray;'>モデル名 カラム名</span><span style='font-weight: bold; color: darkcyan;'>:</span><span style='color: gray;'>データ型 カラム名</span><span style='font-weight: bold; color: darkcyan;'>:</span><span style='color: gray;'>データ型</span>

```bash
$ rails g model ModelName column_name:data_type column_name:data_type
```

<span style='padding: 0 .5rem; border: thin solid;'>モデル名</span> 先頭大文字・キャメルケース・<u>**単数形**</u> (先頭小文字・スネークケースでも可)

<span style='color: forestgreen;'>= 自動生成 =</span>

```ruby
# db/migrate/**************_create_model_name.rb

class CreateModelName < ActiveRecord::Migration[6.1]
  def change
    create_table :model_name do |t|
      t.data_type :column_name

      t.timestamps
    end
  end
end
```

```ruby
# app/models/model_name.rb

class ModelName < ApplicationRecord
end
```

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

<span id='g-migration'></span>
## g migrate
マイグレーションファイルを作成。

<span style='font-weight: bold; color: darkcyan;'>raisl g migration</span> <span styel='color: gray;'>マイグレーション名
 カラム名</span><span style='font-weight: bold; color: darkcyan;'>:</span><span styel='color: gray;'>データ型
 カラム名</span><span style='font-weight: bold; color: darkcyan;'>:</span><span styel='color: gray;'>データ型</span>

```bash
$ rails g migration MigrationName column_name:data_type column_name:data_type
```

<br>

<span id='add_column'></span>
### add_column
カラムを追加する。

<span style='font-weight: bold; color: darkcyan;'>rails g migration Add</span><span styel='color: gray;'>Columns</span><span style='font-weight: bold; color: darkcyan;'>To</span><span styel='color: gray;'>テーブル名
 カラム名</span><span style='font-weight: bold; color: darkcyan;'>:</span><span styel='color: gray;'>データ型
 カラム名</span><span style='font-weight: bold; color: darkcyan;'>:</span><span styel='color: gray;'>データ型</span>

```bash
$ rails g migration AddColumnNameToTableName(s) column_name:data_type
```

<span style='color: forestgreen;'>= 自動生成 =</span>

```ruby
# db/migrate/**************_add_column_name_to_table_names.rb

class AddColumnNameToTableName < ActiveRecord::Migration[6.1]
  def change
    add_column :table_name, :column_name, :data_type
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

<span style='color: forestgreen;'>= 自動生成 =</span>

```ruby
# db/migrate/**************_add_birthday_to_users.rb

class AddBirthdayToUsers < ActiveRecord::Migration[6.1]
  def change
    add_column :users, :birthday, :date
  end
end
```

<br>

【複数カラム】

```bash
$ rails g migration AddColumnsToUsers birthday:date sex:integer
```

<span style='color: forestgreen;'>= 自動生成 =</span>

```ruby
# db/migrate/**************_add_columns_to_users.rb

class AddColumnsToUsers < ActiveRecord::Migration[6.1]
  def change
    add_column :users, :birthday, :date
    add_column :users, :sex, :integer
  end
end
```
</details>

<br>

<span id='remove_column'></span>
### remove_column
カラムの削除。

<span style='font-weight: bold; color: darkcyan;'>rails g migration Remove</span><span styel='color: gray;'>カラム名</span><span style='font-weight: bold; color: darkcyan;'>From</span><span styel='color: gray;'>テーブル名 カラム名</span><span style='font-weight: bold; color: darkcyan;'>:</span><span styel='color: gray;'>データ型</span>

<span style='border-bottom: thin solid crimson'>データ型を指定しないとロールバックできなくなる。</span>

```bash
$ rails g migration RemoveColumnNameFromTableName(s) column_name:data_type
```

<span style='color: forestgreen;'>= 自動生成 =</span>

```ruby
# db/migrate/**************_remove_column_name_from_table_names.rb

class RemoveColumnNameFromTableNames < ActiveRecord::Migration[6.1]
  def change
    remove_column :table_name, :column_name, :data_type
  end
end
```

<details>

```bash
$ rails g migration RemoveBirthdayFromUsers birthday:date
Running via Spring preloader in process 26
      invoke  active_record
      create    db/migrate/**************_remove_birthday_from_users.rb
```
```ruby
# db/migrate/**************_remove_birthday_from_users.rb

class RemoveBirthdayFromUsers < ActiveRecord::Migration[6.1]
  def change
    remove_column :users, :birthday, :date
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

