Tested on ghost version 3.38

[Reference](https://github.com/TryGhost/Ghost/issues/5227)

When you don't have smtp set up via mailgun but you want to create an author user, insert the user contents directly into the sql database.

Make sure the id and user_id fulfill the regex `/^[a-f\d]{24}$|^1$|me/i` and replace the password hash with a known password hash.

Run the sql queries:
`insert into users (id, name, slug, password, email, status, visibility, created_at, created_by) values ('example_id', 'example_username', 'example_user_slug', '$password_hash', 'example_email', 'active', 'public', '2020-11-29 14:12:20', '2020-11-29 13:55:44');`

`5fc3d6798fb4817aa7924b4e` is the role_id for an author user.

`insert into roles_users (id, role_id, user_id) values ('another_example_id', '5fc3d6798fb4817aa7924b4e', 'example_id');`

Now, the user's password can be changed in the web app's admin panel.
