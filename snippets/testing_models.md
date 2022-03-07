# Testing Models
```ruby
# spec/models/task_spec.rb

require 'rails_helper'

RSpec.describe Task, type: :model do
  let(:task) { Task.new(title: 'Task', details: 'Once upon a time I had to invent a task') }

  describe '#initialize' do
    context 'when valid' do
      it 'generates a valid task with all columns' do
        expect(task.valid?).to eq(true)
      end
    end

    context 'when invalid' do
      context 'without title' do
        before do
          task.title = nil
        end

        it 'generates an invalid task' do
          expect(task.valid?).to eq(false)
        end

        it 'generates an error message' do
          task.valid?
          expect(task.errors.messages).to eq({ title: ["can't be blank"] })
        end
      end
    end
  end

  describe '#truncated_details' do
    it 'returns truncated details' do
      expect(task.truncated_details).to eq('Once upon a...')
    end
  end
end
```
