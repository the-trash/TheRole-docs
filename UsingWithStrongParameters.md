[[ Back to TheRole ]](https://github.com/the-teacher/the_role)

<hr>

## Using with Strong Parameters

```ruby
class PagesController < ApplicationController
  # .. code ...

  private

  def page_params
    permitted_keys = [:title, :intro, :content]

    permitted_keys.push(:tags)       if current_user.has_role?(:pages, :tags)
    permitted_keys.push(:top_secret) if current_user.admin?

    params.require(:page).permit(permitted_keys)
  end
end
```

<hr>

[[ Back to TheRole ]](https://github.com/the-teacher/the_role)
