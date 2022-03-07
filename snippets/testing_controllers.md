# Testing Controllers
```ruby
# spec/controllers/tasks_controller_spec.rb

require 'rails_helper'

RSpec.describe TasksController, type: :controller do
  let!(:task1) { Task.create(title: 'Task', details: 'Once upon a time I had to invent a task') }
  let!(:task2) { Task.create(title: 'Task 2', details: 'Task 2') }

  describe 'GET #index' do
    before do
      get :index
    end

    it 'renders index' do
      expect(response).to render_template(:index)
    end

    it 'assigns 2 tasks' do
      expect(assigns(:tasks).count).to eq(2)
    end
  end

  describe 'POST #create' do
    before do
      post :create, params: { task: { title: 'Title', details: 'Details' } }
    end

    it 'creates a Task' do
      expect(Task.find_by(title: 'Title').details).to eq('Details')
    end

    it 'redirects to task_path' do
      expect(response).to redirect_to task_path(Task.last)
    end

    it 'assigns a task' do
      expect(assigns(:task).class).to eq(Task)
    end
  end
end
```
