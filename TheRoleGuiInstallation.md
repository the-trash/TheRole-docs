0. [[ Back to TheRole ]](https://github.com/the-teacher/the_role)
0. [[ Back to TheRole API ]](https://github.com/TheRole/the_role_api)
0. [[ Back to TheRole GUI ]](https://github.com/TheRole/the_role_management_panel)

<hr>

## TheRole GUI Installation

#### 0. Gemfile

```ruby
gem 'the_role', '~> 3.0.0'
```

or

```ruby
gem 'the_role_api',              '~> 3.0.0'
gem 'the_role_management_panel', '~> 3.0.0'
```

and after that

```sh
bundle
```

#### 1. Check TheRole initializer

<i>config/initializers/the_role.rb</i>

```ruby
TheRole.configure do |config|
  # [ Devise => :authenticate_user! | Sorcery => :require_login ]
  config.login_required_method = :authenticate_user!

  # layout for Management panel
  config.layout = :the_role_management_panel

  # ... code ...
end
```

#### 2. Add Routing mixin

<i>config/config/routes.rb</i>

```ruby
RailsApp::Application.routes.draw do
  # ... code ...

  TheRoleManagementPanel::Routes.mixin(self)
end
```

#### 3. Add link to TheRole Manage Panel

<i>HAML</i>

```ruby
- if current_user
  - if current_user.admin? || current_user.moderator?(:roles)
    = link_to 'TheRole Manage Panel',  admin_roles_path
```

<hr>

0. [[ Back to TheRole ]](https://github.com/the-teacher/the_role)
0. [[ Back to TheRole API ]](https://github.com/TheRole/the_role_api)
0. [[ Back to TheRole GUI ]](https://github.com/TheRole/the_role_management_panel)
