# Output Without Memory Banks

## Test Task

Generate a React + TypeScript TaskForm component for creating a new task with validation.

## Prompt Used

Generate a React + TypeScript TaskForm component for a Task Board app.

The component should allow the user to create a new task with:
- title
- optional description
- status

Add basic validation so the title cannot be empty.

Return the code and briefly explain where it should be placed.

## Generated Output

```tsx
import React, { useState } from 'react';

interface Task {
  title: string;
  description?: string;
  status: 'todo' | 'in-progress' | 'done';
}

interface TaskFormProps {
  onSubmit: (task: Task) => void;
}

export const TaskForm: React.FC<TaskFormProps> = ({ onSubmit }) => {
  const [title, setTitle] = useState('');
  const [description, setDescription] = useState('');
  const [status, setStatus] = useState<'todo' | 'in-progress' | 'done'>('todo');
  const [error, setError] = useState('');

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    
    // Validation
    if (!title.trim()) {
      setError('Title is required');
      return;
    }

    onSubmit({
      title: title.trim(),
      description: description.trim() || undefined,
      status,
    });

    // Reset form
    setTitle('');
    setDescription('');
    setStatus('todo');
    setError('');
  };

  return (
    <form onSubmit={handleSubmit} className="task-form">
      <div className="form-group">
        <label htmlFor="title">Title *</label>
        <input
          id="title"
          type="text"
          value={title}
          onChange={(e) => {
            setTitle(e.target.value);
            setError('');
          }}
          placeholder="Enter task title"
        />
      </div>

      <div className="form-group">
        <label htmlFor="description">Description</label>
        <textarea
          id="description"
          value={description}
          onChange={(e) => setDescription(e.target.value)}
          placeholder="Enter task description (optional)"
          rows={3}
        />
      </div>

      <div className="form-group">
        <label htmlFor="status">Status</label>
        <select
          id="status"
          value={status}
          onChange={(e) => setStatus(e.target.value as 'todo' | 'in-progress' | 'done')}
        >
          <option value="todo">To Do</option>
          <option value="in-progress">In Progress</option>
          <option value="done">Done</option>
        </select>
      </div>

      {error && <div className="error-message">{error}</div>}

      <button type="submit">Create Task</button>
    </form>
  );
};
```

## Initial Observations

- The output uses React and TypeScript.
- The component includes basic title validation.
- The output is generic because it was generated without memory bank context.
- The task status values are lowercase: `todo`, `in-progress`, `done`.
- The output does not confirm whether these status values match the project domain glossary.
- The `Task` interface is defined inside the component instead of using a centralized task type.
- The generated task does not include `id`, `createdAt`, or `updatedAt`.
- The output does not clearly explain the exact project file location.
- The output does not mention `src/components/TaskForm.tsx`.
- The output does not mention localStorage or persistence behavior.
- The output does not reference architecture, coding standards, domain glossary, or workflow rules.
