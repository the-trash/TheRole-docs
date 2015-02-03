[[ Back to TheRole ]](https://github.com/the-teacher/the_role)

<hr>

## Customization, Rake tasks and Code generators:

### Rake Tasks

Create Admin Role

```ruby
rake db:the_role:admin

```

```ruby
bundle exec rake the_role_engine:install:migrations
```

### Code generators

If you need to overwrite something, change views or locales, you can use `generators`. Generators will copy files from TheRole into your Rails App:

#### TheRole API

Show me HELP

```ruby
bundle exec rails g the_role help
```

Install config file and models

```ruby
bundle exec rails g the_role install
```

Install config file

```ruby
bundle exec rails g the_role config
```

Install models

```ruby
bundle exec rails g the_role models
```

Install controllers

```ruby
bundle exec rails g the_role controllers
```

Install locales

```ruby
bundle exec rails g the_role locales
```

#### TheRole Management Panel

Show me HELP

```ruby
bundle exec rails g the_role_management_panel help
```

Install views, controllers, assets

```ruby
bundle exec rails g the_role_management_panel install
```

Install assets

```ruby
bundle exec rails g the_role_management_panel assets
```

Install controllers

```ruby
bundle exec rails g the_role_management_panel controllers
```

Install views

```ruby
bundle exec rails g the_role_management_panel views
```

Install locales

```ruby
bundle exec rails g the_role_management_panel locales
```

<hr>

[[ Back to TheRole ]](https://github.com/the-teacher/the_role)
