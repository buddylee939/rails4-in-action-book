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

- 