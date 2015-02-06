[[ Back to TheRole ]](https://github.com/the-teacher/the_role)

<hr>

## For PostgresSQL users

If you are user of PostgresSQL, and you want to use native PSQL way to store json data, there is a way how it should to be:

Your migration file:

```ruby
class CreateRoles < ActiveRecord::Migration
  def self.up
    create_table :roles do |t|

      t.string :name,  default: ""
      t.string :title, default: ""
      t.text :description

      # MySQL, SQLite
      # t.text :the_role, null: false

      # PostgreSQL
      t.column :the_role, :json, null: false

      t.timestamps
    end
  end

  def self.down
    drop_table :roles
  end
end
```

Your TheRole class:

_app/models/role.rb_

```ruby
class Role < ActiveRecord::Base
  include TheRole::Api::Role

  def _jsonable val
    val.is_a?(Hash) ? val : JSON.load(val)
  end

  def to_hash
    begin the_role rescue {} end
  end

  def to_json
    the_role.is_a?(Hash) ? the_role.to_json : the_role
  end
end
```

My tests was green with this patch. I hope it will be useful and for you.

<hr>

[[ Back to TheRole ]](https://github.com/the-teacher/the_role)

