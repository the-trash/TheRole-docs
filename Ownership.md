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

#### `owner_required` method and controllers

Method <a href="https://github.com/TheRole/the_role_api/blob/master/app/controllers/concerns/the_role/controller.rb#L20">owner_required</a> based on method `owner?(object)` and variable `@owner_check_object`

If you want to use your own ownership checking method, you should to overwrite method `owner_required` to meet your needs.

You can do something like this:

Model

```ruby
class User < ActiveRecord::Base
  include TheRole::Api::User

  def is_owner_of?(object)
    # code
  end

  has_many :pages
end
```

Application controller

```ruby
class ApplicationController < ActionController::Base
  include TheRole::Controller

  private

  def for_ownership_check obj
    @owner_check_object = obj
  end

  def my_special_ownership_check
    role_access_denied unless current_user.try(:is_owner_of?, @owner_check_object)
  end
end
```

and after in Pages controller

```ruby
class PagesController < ApplicationController
  before_action :login_required, except: [:index, :show]
  before_action :role_required,  except: [:index, :show]

  before_action :set_page,                   only: [:edit, :update, :destroy]
  before_action :my_special_ownership_check, only: [:edit, :update, :destroy]

  # ... code ...

  private

  def set_page
    @page = Page.find params[:id]
    for_ownership_check(@page)
  end
end
```

<hr>

[[ Back to TheRole ]](https://github.com/the-teacher/the_role)
