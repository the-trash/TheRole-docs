[[ Back to TheRole ]](https://github.com/the-teacher/the_role)

<hr>

## TheRole. Installation

#### 0. Gemfile

```ruby
gem 'the_role', '~> 3.0.0'
```

or

```ruby
# only API
gem 'the_role_api', '~> 3.0.0'
```

and after that

```sh
bundle
```

#### 1. Change User migration file

Add a `role_id:integer` field to your User Model

```ruby
def self.up
  create_table :users do |t|
    t.string :login
    t.string :email
    t.string :crypted_password
    t.string :salt

    # !!! TheRole field !!!
    t.integer :role_id

    t.timestamps
  end
end
```

#### 2. Install TheRole migration file

```sh
bundle exec rake the_role_engine:install:migrations
```

#### 3. Invoke migrations

```sh
rake db:migrate
```

#### 4. Change User model

```ruby
class User < ActiveRecord::Base
  include TheRole::Api::User

  # ... code ...
end
```

#### 5. Create Role model

```sh
bundle exec rails g the_role install
```

#### 6. Setup TheRole gem

<i>config/initializers/the_role.rb</i>

```ruby
TheRole.configure do |config|
  # [ Devise => :authenticate_user! | Sorcery => :require_login ]
  config.login_required_method = :authenticate_user!

  # layout for Management panel
  config.layout = :the_role_management_panel

  # config.default_user_role          = nil
  # config.first_user_should_be_admin = false

  # config.access_denied_method       = :access_denied
  # config.destroy_strategy           = :restrict_with_exception # can be nil
end
```

#### 7. Create admin role

```sh
rake db:the_role:admin
```

Now you can make any user an Admin via `rails console`, for instance:

```ruby
User.first.update( role: Role.with_name(:admin) )
User.first.admin? # => true
```

<hr>

<p align="center" class='center' style="text-align:center">
  <b>
    You are in deal!<br>
    Thanks for using TheRole!
  </b>
</p>

<hr>

[[ Back to TheRole ]](https://github.com/the-teacher/the_role)
