[[ Back to TheRole ]](https://github.com/the-teacher/the_role)

<hr>

## Migration form TheRole 2 to TheRole 3

#### Gemfile

BEFORE

```ruby
gem 'the_role', '~> 2.X'
```

or

```ruby
gem 'the_role', '~> 2.X'
gem 'the_role_bootstrap3_ui'
```

AFTER

```ruby
gem 'the_role', '~> 3.0'
```

or

```ruby
gem 'the_role_api', '~> 3.0'
gem 'the_role_management_panel', '~> 3.0'
```

#### Change routing

_config/routes.rb_

before

```ruby
  namespace :admin do
    TheRole::Routes.mixin(self)
  end
```

after

```ruby
  TheRoleManagementPanel::Routes.mixin(self)
```

#### Change `User` model

before

```ruby
class User < ActiveRecord::Base
  include TheRole::User
end
```

after

```ruby
class User < ActiveRecord::Base
  include TheRole::Api::User
end
```

#### Change `Role` model

```ruby
class Role < ActiveRecord::Base
  include TheRole::Role
end
```

after

```ruby
class Role < ActiveRecord::Base
  include TheRole::Api::Role
end
```

#### Initializer

_config/initializers/the_role.rb_

before

```ruby
TheRole.configure do |config|
  config.destroy_strategy  = nil
  config.default_user_role = :blogger
  config.layout            = :application
  config.first_user_should_be_admin = true
end
```

after

```ruby
TheRole.configure do |config|
  # [ Devise => :authenticate_user! | Sorcery => :require_login ]
  config.login_required_method = :authenticate_user!

  # layout for Management panel
  config.layout = :the_role_management_panel

  config.default_user_role          = :blogger
  config.first_user_should_be_admin = true

  # config.access_denied_method       = :access_denied
  # config.destroy_strategy           = :nil
end
```

<hr>

### For PostgresSQL users

[how to use native :json column](https://github.com/TheRole/docs/blob/master/forPostgresSQLusers.md)

<hr>


#### Bundle && restart

```sh
bundle
```

```sh
rails s
```

<hr>

[[ Back to TheRole ]](https://github.com/the-teacher/the_role)
