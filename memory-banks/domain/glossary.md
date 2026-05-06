# Domain Glossary: Task Board Lab

## Purpose

This glossary defines project-specific language used across Task Board Lab so AI assistants do not misinterpret core concepts when generating code, specifications, or reviews.

AI assistants should use this file together with:
- `specs/prds/PRD-personal-task-board.md`
- `specs/epics/*`
- `specs/stories/*`
- `agents.md`
- `memory-banks/architecture/overview.md`
- `memory-banks/conventions/coding-standards.md`

Why this matters in this project:
- Task Board Lab is frontend-only, single-user, and localStorage-based.
- The product uses a fixed three-column Kanban workflow (`To Do`, `In Progress`, `Done`).
- Using generic PM terminology or introducing backend/auth assumptions causes incorrect output.

## Terms

### 1) Task

- Definition: A single actionable work item within one project on the board.
- Context: In specs, tasks are created quickly in `To Do`, then updated, moved, reordered, or deleted.
- Example: "Fix login page redirect bug" created in `To Do` for "Side Project: SaaS App".
- Relationships:
	- Belongs to exactly one Project.
	- Has exactly one Task Status at a time.
	- Rendered as a Task Card in one Task Column.

### 2) Task Board

- Definition: The active project’s Kanban-style visual workspace containing three fixed columns.
- Context: The PRD requires exactly three columns and emphasizes at-a-glance workflow visibility.
- Example: Opening "Client Project A" shows columns `To Do`, `In Progress`, and `Done` with task counts.
- Relationships:
	- Displays Tasks grouped by Task Status.
	- Scoped to the currently active Project.

### 3) Task Column

- Definition: One lane on the Task Board representing a single status bucket.
- Context: Columns are fixed in MVP and must not be replaced with custom workflow stages unless scope changes.
- Example: A task moved from `In Progress` to `Done` leaves the source column and appears in target column.
- Relationships:
	- Column identity is driven by Task Status value.
	- A Task can appear in only one column at any moment.

### 4) Task Card

- Definition: The UI representation of a Task inside a column list.
- Context: Card displays title and may include description, priority, tags, and timestamps depending on story scope.
- Example: Card shows `High` priority and tags `Bug`, `Auth` while remaining in `In Progress`.
- Relationships:
	- Visual wrapper around Task data.
	- Moves between columns via drag and drop or keyboard actions.

### 5) Task Status

- Definition: The canonical workflow state assigned to a Task.
- Context: Status values are constrained by project rules and should match implementation vocabulary exactly.
- Example: Internal values from architecture/coding standards: `todo`, `in-progress`, `done` (mapped to UI labels `To Do`, `In Progress`, `Done`).
- Relationships:
	- Determines which Task Column renders the Task.
	- Changes through drag-drop or shortcut movement actions.

### 6) Task Status Lifecycle

- Definition: Allowed movement path between statuses during normal workflow.
- Context: The PRD and workflow stories center on movement across `To Do -> In Progress -> Done` and reverse movement with shortcuts.
- Example: New task starts in `To Do`, moves to `In Progress`, then to `Done`; user can move backward if needed.
- Relationships:
	- Implemented by drag-and-drop and keyboard shortcuts.
	- Must preserve a single valid status at all times.

### 7) User Story

- Definition: A small, testable requirement unit in `specs/stories/` written in "As a..., I want..., so that..." format.
- Context: Stories drive implementation sequencing for Module 02 outputs and future code tasks.
- Example: `STORY-001.003-create-task.md` defines creating a task in `To Do` with validation for empty title.
- Relationships:
	- Belongs to one Epic.
	- Includes Acceptance Criteria and Definition of Done checks.

### 8) Acceptance Criteria

- Definition: Objective Given/When/Then conditions that define when a story is complete.
- Context: Every story in this repo uses explicit criteria to support consistent QA and assistant output.
- Example: "Given empty or whitespace-only title, when submit, then task is not created and inline validation appears."
- Relationships:
	- Used in testing requirements and code review validation.
	- Forms part of Definition of Done evidence.

### 9) PRD

- Definition: Product Requirements Document that defines product goals, functional/non-functional requirements, scope, and metrics.
- Context: `PRD-personal-task-board.md` is the top-level source for product intent.
- Example: PRD requires frontend-only architecture, keyboard support, localStorage persistence, and fixed three-column board.
- Relationships:
	- Parent artifact for Epics.
	- Primary source of business constraints for AI assistants.

### 10) Epic

- Definition: A larger feature capability grouped into multiple User Stories, tracked in `specs/epics/`.
- Context: Current epics cover foundation, workflow efficiency, data/privacy portability, and accessibility/responsiveness.
- Example: `EPIC-002-efficient-task-workflows.md` covers drag-drop, shortcuts, and context preservation.
- Relationships:
	- Derived from PRD goals.
	- Decomposed into 4-8 stories (target pattern in project conventions).

### 11) LocalStorage Persistence

- Definition: Browser-based storage mechanism used to save and restore board state without backend services.
- Context: Core project promise is privacy + reliability with data stored on-device only.
- Example: After creating/editing/moving/deleting a task, board state is saved; on reload, state hydrates from localStorage.
- Relationships:
	- Persistence adapter in architecture handles serialization, validation, and fallback behavior.
	- Linked to import/export JSON portability stories.

### 12) Drag and Drop

- Definition: Direct manipulation interaction for moving tasks across columns and reordering within a column.
- Context: Defined in workflow epic/stories as a speed feature for power users.
- Example: Drag task from `To Do` to `In Progress`; if drop target invalid, task returns to original position.
- Relationships:
	- Updates Task Status and ordering state.
	- Must preserve accessibility and not break keyboard/focus behavior.

## Key Business Rules

1. Task title cannot be empty.
- Empty or whitespace-only titles must fail validation and must not create a task.

2. A task must have exactly one valid status.
- A task cannot be status-less and cannot hold multiple statuses.

3. Valid statuses must match project implementation.
- Canonical status set: `todo`, `in-progress`, `done`.
- UI labels: `To Do`, `In Progress`, `Done`.

4. A task should appear in only one column at a time.
- Rendering in multiple columns indicates state corruption.

5. Editing a task should preserve its identity.
- Task `id` remains stable when title/description/priority/tags are edited.

6. Deleting a task removes it from the board.
- After confirmed deletion, task must not appear in any column.

7. If localStorage is used, task changes should be persisted.
- Create/edit/move/delete actions should trigger persistence.
- On reload, valid saved state should be restored.

8. localStorage failures must not crash the app.
- On malformed or unavailable storage, app falls back to safe state with non-blocking user feedback.

9. New tasks are created in `To Do` by default.
- This is explicit in story and epic flow for fast capture.

10. AI assistants must not invent backend/database/user authentication rules unless they exist in the project.
- Task Board Lab is frontend-only, single-user, localStorage-based.
- No API server, database, or auth model should be introduced without explicit project changes.

---

**Last Updated:** May 6, 2026
