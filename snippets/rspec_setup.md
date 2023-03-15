# RSpec Setup

Add to your Gemfile the following code:

```ruby
group :development, :test do
  gem 'rspec-rails', '~> 6.0.0'
end
```

Then in your terminal run the following commands:

```zsh
bundle install
rails generate rspec:install
```

For more details check the [gem's page](https://github.com/rspec/rspec-rails).
