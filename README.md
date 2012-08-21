Inbox
=====


Description
-----------

* Preview send emails in development and test mode.

* Test them using your standard Capybara matchers or
any other testing framework that you prefer.


Installation
------------

In your `Gemfile` add:

```ruby
gem 'inbox'
```

And run:

```
bundle install
```


Setup
-----

Mount engine in `config/routes.rb`

```ruby
Rails.application.routes.draw do
  mount Inbox::Engine => "/inbox"
end
```


Usage
-----

### Manual

Navigate to `/inbox/<email>/emails` ex.: `/inbox/robert.pankowecki@gmail.com/emails`
to see a list of emails that would be delivered to the user.

Click subject of the email to see its content

### Testing framework

In [capybara](https://github.com/jnicklas/capybara/) or [bbq](https://github.com/drugpl/bbq)

```ruby
visit("/inbox/robert.pankowecki@gmail.com/emails")
click_link("Subject of the email")
has_content?("This should be in email")
click_link("Some link in the email ex. account activation link")
```

The nice thing is that this is just HTML page displaying email content so you can use
your favorite testing framework (`BBQ`, `Capybara`, `Test::Unit`, `Spinach`, `Cucumber`, `RSpec`, whatever)
for checking the content of page. And you can reuse your matchers.


### Sending

Navigate to `/inbox/<email>/emails/new` ex.: `/inbox/robert.pankowecki@gmail.com/emails/new`
to see un ugly form for sending emails that you can use to play around and see if everything
works fine.


Async (distributed / queue)
---------------------------

In case you want to have acceptance tests of emails that are sent using external process (resque, sidekiq, ...) just set

```ruby
config.action_mailer.delivery_method = :inbox
```

in `config/environments/test.rb` and create `tmp/mails` directory.


If you send emails from your Rails models, controllers, services or use-cases you can stick with:

```ruby
config.action_mailer.delivery_method = :test
```


Look & Feel
-----------

http://img832.imageshack.us/img832/1333/screenshotinboxgooglech.png


License
-------

MIT-LICENSE