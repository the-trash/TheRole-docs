[[ Back to TheRole ]](https://github.com/the-teacher/the_role)

<hr>

## Contributing.md

#### 0. Prepare folder

```sh
mkdir -p ~/my/gems/TheRole
cd ~/my/gems/TheRole
```

#### 1. Clone projects

```sh
git clone git@github.com:TheRole/DummyApp.git
git clone https://github.com/TheRole/the_role_api
git clone https://github.com/TheRole/the_role_management_panel
```

You Editor file browser can looks like this

<p align="center" class='center' style="text-align:center">
  <img src="https://raw.githubusercontent.com/TheRole/docs/master/images/editor.png" alt="TheRole. Authorization gem for Ruby on Rails with Administrative interface">
</p>

#### 2. Move to DummyApp

```sh
cd ~/my/gems/TheRole/DummyApp
```

#### 3. Change Gemfile

Link DummyApp with local gems

```sh
gem 'the_role_api',
  path: '../the_role_api'

gem 'the_role_management_panel',
  path: '../the_role_management_panel'
```

#### 4. Bundle and test!

```sh
bundle
```

```sh
RAILS_ENV=test rake db:bootstrap
RAILS_ENV=test rspec --format documentation
```

#### 5. Move to gem which you want to improve

```sh
cd ~/my/gems/TheRole/the_role_api
```

#### 6. Create new branch with feature

```
git checkout -b "mongo_version"
```

#### 7. Create new branch with feature and make some magic

```
git checkout -b "mongo_version"
```

Write code, have fun!

You can see you results in DummyApp

#### 8. Test your feature

```sh
cd ~/my/gems/TheRole/DummyApp

RAILS_ENV=test rspec --format documentation
```

#### 9. Send a Pull Request

Send a Pull Request =)