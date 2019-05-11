# Things we did

- simple form, bootstrap, changed class for initializers span
- rspec testing
- styled buttons via extends in the scss, rather than adding the class straight to the buttons
- used dependent delete all instead of destroy

```
has_many :tickets, dependent: :delete_all
```

- pg. 140 gives the different examples

```
has_many :tickets, dependent: :delete_all
has_many :tickets, dependent: :destroy
has_many :tickets, dependent: :nullify
Finally, there are two options that work similarly—:restrict_with_error and :restrict_with_exception. Both options will prevent records from being deleted if the association isn’t empty; for example, in your projects and tickets scenario, you wouldn’t be able to delete projects if they had any tickets in them.
```

- while testing devise login, we had to add to the spec/rails helper, from page 157-158

```
  config.include Warden::Test::Helpers, type: :feature
  config.after(type: :feature) { Warden.test_reset! }
```

- used devise
- gave users an 'author' title, instead of user, in the user.rb

```
belongs_to :author, class_name: "User"
```

- then added a migration to add author references to the tickets

```
rails g migration add_author_to_tickets author:references
```

- then we changed the migration to change the author id

```
class AddAuthorToTickets < ActiveRecord::Migration[5.2]
  def change
    add_reference :tickets, :author, index: true
    add_foreign_key :tickets, :users, column: :author_id
  end
end
```

- the reason is

```
Why do you need to do this? Because Rails’ automatic inference will try to apply a for- eign key on your tickets table, pointing to an authors table—and you don’t have a ticket table. The author will be a User, living in the users table, so you need to spe- cifically tell Rails that the foreign key should point to the users table instead (but still use the author_id field to do so.)

```

- allowing users to be admins
- seeded the database
- generated namespaced controllers for admins: page 199

```
rails g controller admin/application index
```

- and the route, set to admin root

```
  namespace :admin do
    root "application#index"
  end
```

- testing the namespace

```
Feature specs are great for defining and testing a series of actions that a user can perform in your application, but control- ler specs are much better for quickly testing singular points, such as whether a user can go to a specific action in a controller.
```

- 
