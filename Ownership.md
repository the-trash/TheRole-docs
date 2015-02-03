[[ Back to TheRole ]](https://github.com/the-teacher/the_role)

<hr>

## Few words about Ownership

#### `owner?(object)` - default method for ownership checking

In fact, checking for ownership is not a task of TheRole, because relations between objects in Rails App sometimes can be confusing.

It's impossible to create universal method for ownership checking. But TheRole provide `owner?(object)` method for simple ownership checking. How does it works?

`@user.owner?(object)` just compare `@user.id` with `object.user_id`, if they are equal method will return `true`

It means, that `object` have to provide `user_id` field or method.

If you want to use default ownership method from TheRole, usually, you have to add `user_id` field into migration file.

This is a case, when `@user.owner?(@page)` will works correctly:

```ruby
class CreatePages < ActiveRecord::Migration
  def change
    create_table :pages do |t|
      # Field for ownership checking
      t.integer :user_id

      t.string :title
      t.text   :content
    end
  end
end
```

```ruby
class User < ActiveRecord::Base
  include TheRole::Api::User

  has_many :pages
end
```

```ruby
class Page < ActiveRecord::Base
  belongs_to :user
end
```

Now you can check something, for instance:

```ruby
@user.owner?(@page) #=> true | false
```

or

```ruby
@user.owner?(@page) && @user.has_role?(:pages, :edit) #=> true | false
```

#### Default method for ownership checking is not suitable for me

If default method for ownership checking is not suitable for you, you can overwrite it or create your own


```ruby
class User < ActiveRecord::Base
  include TheRole::Api::User

  # Just overwrite default `owner?(object)`
  def owner?(object)
    if object.is_a?(Article)
      # code for ownership checking
    else
      # or call default version
      super
    end
  end

  def is_owner_of?(object)
    # code
  end

  has_many :pages
end
```

Now you can check something, for instance:

```ruby
@user.owner?(@article) #=> true | false
@user.owner?(@page)    #=> true | false
```

or

```ruby
@user.is_owner_of?(@page)    && @user.has_role?(:pages, :edit)    #=> true | false
@user.is_owner_of?(@article) && @user.has_role?(:articles, :edit) #=> true | false
```

<hr>

[[ Back to TheRole ]](https://github.com/the-teacher/the_role)
