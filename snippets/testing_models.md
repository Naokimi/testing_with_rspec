# Testing Models
```ruby
# spec/models/task_spec.rb

require 'rails_helper'

RSpec.describe Task, type: :model do
  let(:task) { Task.new(title: 'Task', description: 'Once upon a time I had to invent a task') }

  describe '#initialize' do
    context 'when valid' do
      it 'returns true on #valid?' do
        expect(task.valid?).to eq(true)
      end
    end

    context 'without title' do
      before do
        task.title = nil
      end

      it 'returns false on #valid?' do
        expect(task.valid?).to eq(false)
      end

      it 'returns an error message' do
        task.valid?
        expect(task.errors.messages).to eq({ title: ["can't be blank"] })
      end
    end
    
    context 'without description' do
      before do
        task.description = nil
      end

      it 'returns false on #valid?' do
        expect(task.valid?).to eq(false)
      end

      it 'returns an error message' do
        task.valid?
        expect(task.errors.messages).to eq({ description: ["can't be blank"] })
      end
    end
  end

  describe '#truncated_description' do
    it 'returns truncated description' do
      expect(task.truncated_description).to eq('Once upon a...')
    end
  end
end
```
