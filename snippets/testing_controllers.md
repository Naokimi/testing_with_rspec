# Testing Controllers
```ruby
# spec/controllers/tasks_controller_spec.rb

require 'rails_helper'

RSpec.describe TasksController, type: :controller do
  describe 'POST #create' do
    let(:description) { 'Description' }
  
    before do
      post :create, params: { task: { title: 'Title', description: description } }
    end

    context 'with correct params' do
      it 'creates a Task' do
        expect(Task.find_by(title: 'Title').description).to eq('Description')
      end

      it 'redirects to task_path' do
        expect(response).to redirect_to task_path(Task.last)
      end

      it 'renders a success notice' do
        expect(flash[:notice]).to eq('Task was successfully created.')
      end
    end
    
    context 'with incorrect params' do
      let(:description) { nil }
      
      it 'skips Task creation' do
        expect(Task.count).to eq(0)
      end

      it 'returns error status' do
        expect(response.status).to eq(:unprocessable_entity)
      end
    end
  end
end
```
