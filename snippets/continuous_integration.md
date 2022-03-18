# Continuous Integration

Create a file `.github/workflows/ruby.yml` and copy the code snippet below

Remember to swap RUBY_VERSION and PSQL_VERSION in the code below for the versions in your machine

Commands to get the data:
- `ruby -v`
- `psql --version`

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
# This workflow will download a prebuilt Ruby version, install dependencies and run tests with Rake
# For more information see: https://github.com/marketplace/actions/setup-ruby-jruby-and-truffleruby

name: Ruby

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  test:

    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:PSQL_VERSION
        env:
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: postgres
          POSTGRES_DB: postgres
        ports:
          - 5432:5432
        # needed because the postgres container does not provide a healthcheck
        # tmpfs makes DB faster by using RAM
        options: >-
          --mount type=tmpfs,destination=/var/lib/postgresql/data
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
    env:
      PGHOST: localhost
      PGUSER: postgres
      PGPORT: 5432
      PGPASSWORD: postgres
      RAILS_ENV: test

    steps:
      - uses: actions/checkout@v2
      - name: Set up Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: 'RUBY_VERSION' # needs to be inside quotes
      - name: Install dependencies
        run: bundle install
      - name: Create DB
        run: bin/rails db:create db:migrate
      - name: Run tests
        run: bundle exec rake
```
