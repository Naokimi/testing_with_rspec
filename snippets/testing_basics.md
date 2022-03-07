# Testing Basics

File naming conventions: `spec/FOLDER/CLASS_NAME_spec.rb` (eg.: `spec/models/task_spec.rb`, `spec/controllers/tasks_controller_spec.rb`)

The basic contents of a testing file are as follow:
```ruby
require 'rails_helper'

RSpec.describe Class, type: :mvc_type do
  describe '#method' do
    it 'description of test' do
      expect(value).to eq(expected_result)
    end
  end
end
```
