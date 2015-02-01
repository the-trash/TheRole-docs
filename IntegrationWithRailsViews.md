0. [[ Back to TheRole ]](https://github.com/the-teacher/the_role)
0. [[ Back to TheRole API ]](https://github.com/TheRole/the_role_api)
0. [[ Back to TheRole GUI ]](https://github.com/TheRole/the_role_management_panel)

## Integration with Rails views

HAML views:

__case 1__

```haml
- if current_user

  - # if you are owner and has role
  - if current_user.owner?(@page) && current_user.has_role?(:pages, :edit)
    = link_to "Edit this Page", edit_page_path(@page)
```

__case 2__

```haml
- if current_user

  - if current_user.any_role?(social_networks: [:twitter_share_button, :facebook_share_button])
    %h3 You can share this content with Social Networks:

    - if current_user.has_role?(:social_networks, :twitter_share_button)
      = link_to 'Share with Twitter', '#'

    - if current_user.has_role?(:social_networks, :facebook_share_button)
      = link_to 'Share with Facebook', '#'

  - if current_user.moderator?(:pages)
    = link_to 'Manage Pages', admin_pages_path

  - if current_user.admin?
    = link_to 'Admin Panel', admin_path
```

0. [[ Back to TheRole ]](https://github.com/the-teacher/the_role)
0. [[ Back to TheRole API ]](https://github.com/TheRole/the_role_api)
0. [[ Back to TheRole GUI ]](https://github.com/TheRole/the_role_management_panel)
