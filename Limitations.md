[[ Back to TheRole ]](https://github.com/the-teacher/the_role)

<hr>

## TheRole Limitations

TheRole uses few conventions over configuration.
It gives simplicity of code, but also some limitations.
You have to know about them before using of TheRole:

0. [User has only one Role](https://github.com/TheRole/docs/blob/master/Limitations.md#user-has-only-one-role)
0. [Only `User` model supported](https://github.com/TheRole/docs/blob/master/Limitations.md#only-user-model-supported)
0. [Based on `curent_user` method](https://github.com/TheRole/docs/blob/master/Limitations.md#based-on-curent_user-method)
0. [Role stored in database as a JSON String](https://github.com/TheRole/docs/blob/master/Limitations.md#role-stored-in-database-as-a-json-string)
0. [Few words about Ownership](https://github.com/TheRole/docs/blob/master/Ownership.md)

### `User` **has only one** `Role`

My practice showed, using of many roles for one user is very, very bad approach. In reality, usually, no one needs it.

Many roles for one user is a reason of many logical mistakes. Calculation of permitted actions for user becomes difficult.

It's difficult to imagine how to create simple and usable interface to manage and to control roles for a user.

TheRole provide only one role for one user. It's most simple, logical and effective approach.

### Only `User` model supported

Right now TheRole works only with model `User`.
You can't use it with `Account`, `Manager`, `Employer` etc.

You can improve TheRole with beauty patch.
If it be really great, I'll add this feature into The Role.

### Based on `curent_user` method

`curent_user` is a most popular name of method associated with logged user. TheRole uses it by default.
There is no ways to use something else. Sorry.

### Role stored in database as a JSON string

There are many databases which provide special native ways to work with JSON data.

But TheRole convert hashes into JSON string and store it into database with plain TEXT value.

TheRole uses this approach because it requires less of code. And it makes maintaining simpler.

### Few words about Ownership

[Few words about Ownership](https://github.com/TheRole/docs/blob/master/Ownership.md)

<hr>

[[ Back to TheRole ]](https://github.com/the-teacher/the_role)
