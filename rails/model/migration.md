# マイグレーション
[Railsガイド](#https://railsguides.jp/active_record_migrations.html)

- [モデルの作成(g model)](#g-model)
- [マイグレーションファイルの作成(g migration)](#g-migration)
    - [カラムの追加(add_column)](#add_column)
    - [カラムの削除(remove_column)](#remove_column)
    - [カラム名を変更(rename_column)](#rename_column)
    - [カラム情報の変更(change_column)](#change_column)
    - [インデックスを付与(add_index)](#add_index)
        - [一意性の付与(unique: true)](#unique)
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

[Railsドキュメント](https://railsdoc.com/page/add_column)

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

[Railsドキュメント](https://railsdoc.com/page/remove_column)

<br>

<span id='rename_column'></span>
### rename_column
カラム名の変更。

<span style='font-weight: bold; color: darkcyan;'>rails g migration Rename</span><span styel='color: gray;'>カラム名</span><span style='font-weight: bold; color: darkcyan;'>Of</span><span styel='color: gray;'>テーブル名

```bash
$ rails g migration RenameColumnNameOfTableName(s)
```

<span style='color: crimson;'>= 自己編集 =</span>

```ruby
class RenameColumnNameOfTableName < ActiveRecord::Migration[6.1]
  def change
    rename_column :table_name(s), :old_column_name, :new_column_name    # 追加
    rename_column :table_name(s), :old_column_name, :new_column_name    # 複数可
  end
end
```

<details>

```bash
$ rails g migration RenameFugaOfHoges
Running via Spring preloader in process 26
      invoke  active_record
      create    db/migrate/**************_rename_fuga_of_hoges.rb
```

```ruby
# db/migrate/**************_rename_fuga_of_hoges.rb

class RemoveFugaOfHoges < ActiveRecord::Migration[6.1]
  def change
    reneme_column :hoges, :fuga, :piyo    # 追加
  end
end
```

</details>

[Railsドキュメント](https://railsdoc.com/page/remove_column)

<br>

<span id='change_column'></span>
### change_column
カラムの情報(データ型)などを変更。

<span style='font-weight: bold; color: darkcyan;'>rails g migration Change</span><span styel='color: gray;'>カラム名</span><span style='font-weight: bold; color: darkcyan;'>Of</span><span styel='color: gray;'>テーブル名

```bash
$ rails g migration ChangeColumnNameOfTableName(s)
```

<span style='color: crimson;'>= 自己編集 =</span>

```ruby
class ChangeColumnNameOfTableNames < ActiveRecord::Migration[6.1]
  # def change     削除
  # end            削除

  # 以下を追加
  def up
    change_column :table_name(s), :column_name, :new_data_type
  end

  def down
    change_column :table_name(s), :column_name, :old_data_type
  end
end
```

`change_column`は`change`メソッドでサポートされていないため、`change`メソッドに記載するとロールバックができない。<br>
そのため、`up`・`down`メソッドを使用する。

<span style='color: crimson;'>**up**</span>: 変更する内容<br>
<span style='color: darkcyan;'>**down**</span>: 変更前の内容

<details>

```bash
$ rails g migration ChangeFugaOfHoges
Running via Spring preloader in process 27
      invoke  active_record
      create    db/migrate/**************_change_fuga_of_hoges.rb
```

```ruby
# db/migrate/**************_change_fuga_of_hoges.rb

class ChangeFugaOfHoges < ActiveRecord::Migration[6.1]
  def up
    change_column :hoges, :fuga, :string
  end

  def down
    change_column :hoges, :fuga, :integer
end
```

</details>

[Railsドキュメント](https://railsdoc.com/page/change_column)

<br>

<span id='add_index'></span>
### add_index
カラムにインデックスを付与。

<span style='font-weight: bold; color: darkcyan;'>rails g migration AddIndex</span><span styel='color: gray;'>カラム名</span><span style='font-weight: bold; color: darkcyan;'>Of</span><span styel='color: gray;'>テーブル名

```bash
$ rails g migration AddIndexColumnNameOfTableName(s)
```

<span style='color: crimson;'>= 自己編集 =</span>

```ruby
class AddIndexColumnNameOfTableNames < ActiveRecord::Migration[6.1]
  def change
    add_index :table_name(s), :column_name    # 追加
  end
end
```

<details>

```bash
$ rails g migration AddIndexNameOfUsers
Running via Spring preloader in process 27
      invoke  active_record
      create    db/migrate/**************_add_index_name_of_users.rb
```

```ruby
# db/migrate/**************_add_index_name_of_users.rb

class AddIndexNameOfUsers < ActiveRecord::Migration[6.1]
  def change
    add_index :users, :name
  end
end
```

</details>

<span id='unique'></span>
#### unique: true
オプションでカラムに一意性をつける。<br>
一意性をつけるときはインデックスが必要。(一意かどうかを検索するため)

<span style='font-weight: bold; color: darkcyan;'>rails g migration AddUniquness</span><span styel='color: gray;'>カラム名</span><span style='font-weight: bold; color: darkcyan;'>Of</span><span styel='color: gray;'>テーブル名

```bash
$ rails g migration AddUniqunessFugaOfHoges
```

<span style='color: crimson;'>= 自己編集 =</span>

```ruby
# db/migrate/**************_add_uniquness_fuga_of_hoges.rb

class AddUniqunessFugaOfHoges < ActiveRecord::Migration[6.1]
  def change
    add_index :hoges, :fuga, unique: true    # 追加
  end
end
```

<br>

複数の組み合わせの一意性を作るには、**カラムを配列**にする。

```ruby
# db/migrate/**************_add_uniquness_fuga_of_hoges.rb

class AddUniqunessFugaOfHoges < ActiveRecord::Migration[6.1]
  def change
    add_index :hoges, [:fuga, :piyo, :hogehoge], unique: true    # 追加
  end
end
```


[Railsドキュメント](https://railsdoc.com/page/add_index)

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

