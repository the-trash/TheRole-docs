[[ Back to TheRole ]](https://github.com/the-teacher/the_role)

<hr>

## TheRole. FAQ


0. [Why TheRole was created?](#why-therole-was-created)
0. [Who is Administrator?](#who-is-administrator)
0. [Who is Moderator?](#who-is-moderator)
0. [Who is Owner?](#who-is-owner)
0. [Virtual sections and rules](#virtual-sections-and-rules)

#### Why TheRole was created?

Proof-of-concept of TheRole was created in 2007, when I implemented my first MVC framework on `PHP`. I knew nothing about the other authorization solutions at this time. That's why you shouldn't compare TheRole with other gems like **CanCan**, **Pundit** etc. TheRole is different.

I became rails developer in 2008 and I dreamed to re-implement my simple and effective idea about authorization module in Ruby. But I did it later, just in 2011.

First of all TheRole designed for end-point users, and provide GUI to manage access policies. It means that programmer have to put restriction methods into code just once, and after that site administrator might change access rules independently with simple GUI.

If you are looking for user-oriented authorization gem for Rails - TheRole can be suitable solution for you.

#### Who is Administrator?

Administrator is the user who can access any section and rules of your application.

Administrator is the owner of any objects in your application.

Administrator is the user, who has a virtual section **system** and a rule **administrator** in the role-hash.


```ruby
admin_role_fragment = {
  :system => {
    :administrator => true
  }
}
```

#### Who is Moderator?

Moderator is the user, who has access to any actions of some section(s).

Moderator is the owner of any objects of some class.

Moderator is the user, who has a virtual section **moderator**, with **section name** as rule name.

An example of a Moderator of Pages (controller) and Twitter (virtual section)

```ruby
moderator_role_fragment = {
  :moderator => {
    :pages   => true,
    :blogs   => false,
    :twitter => true
  }
}
```

#### Who is Owner?

Administrator is owner of any object in system.

Moderator of pages is owner of any page.

User is owner of objects, when **Object#user_id == User#id**.

#### Virtual sections and rules

Usually, we use real names of controllers and actions for names of sections and rules:

```ruby
@user.has_role?(:pages, :show)
```

But, also, you can use virtual names of sections, and virtual names of section's rules.

```ruby
@user.has_role?(:twitter, :button)
@user.has_role?(:facebook, :like)
```

And you can use them as well as other access rules.

<hr>

[[ Back to TheRole ]](https://github.com/the-teacher/the_role)
