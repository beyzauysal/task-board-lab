# Task Board Lab - Coding Standards for AI Assistants

## 1. Purpose

This document defines implementation standards for Task Board Lab so AI assistants generate consistent, reviewable, and in-scope code.

Task Board Lab is a frontend-only React 18 + Vite + TypeScript project for a single user, with browser localStorage persistence. Standards in this file prioritize:
- Fast iteration for a bootcamp lab
- Consistency with PRD/Epics/Stories
- Accessibility and keyboard-first workflows
- No accidental expansion into backend/database/auth scope

Scope note based on current repository state:
- This repository currently contains specs and memory-bank artifacts.
- App runtime files (for example `src/` and `package.json`) are not present yet.
- These standards apply immediately to documentation and should be used as implementation rules when app scaffolding is added.

---

## 2. Naming Conventions

### 2.1 Specification and Prompt Files (already active in repo)

- PRD files: `PRD-{feature-name}.md`
- Epic files: `EPIC-{number}-{name}.md`
- Story files: `STORY-{epic}.{story}-{name}.md`
- Template files: lowercase kebab-case, `.md`
- Prompt files: lowercase kebab-case, `.prompt.md`

Rules:
- Keep required uppercase prefixes exactly: `PRD-`, `EPIC-`, `STORY-`
- Use kebab-case descriptive segments
- Do not use spaces, underscores, or mixed-case suffixes

### 2.2 Future Source Code Naming (when `src/` exists)

- Components: `PascalCase` file names (example: `TaskCard.tsx`)
- Hooks: `useCamelCase` (example: `useBoardState.ts`)
- Utilities/services: `camelCase` or domain-based noun phrases (example: `localStorageAdapter.ts`)
- Types/interfaces: `PascalCase` type names (example: `BoardState`, `TaskStatus`)
- Constants: `UPPER_SNAKE_CASE` for shared compile-time constants
- Test files: `{module}.test.ts` or `{component}.test.tsx`

Domain naming rules:
- Use status vocabulary exactly: `todo`, `in-progress`, `done`
- Use priority vocabulary exactly: `low`, `medium`, `high`
- Use `projectId` and `taskId` consistently; avoid synonyms like `projId` or `itemId`

---

## 3. File Structure

### 3.1 Current Repository Structure (must be respected)

- `specs/templates/` for reusable templates only
- `specs/prds/` for generated PRDs
- `specs/epics/` for generated Epics
- `specs/stories/` for generated Stories
- `.github/prompts/` for prompt files
- `memory-banks/` for assistant memory documents
- `agents.md` for cross-project conventions

Do not place generated specification files outside `specs/`.

### 3.2 Target Source Layout (once app code is scaffolded)

Recommended:
- `src/app/` application bootstrap and providers
- `src/features/projects/` project list/create/rename/delete
- `src/features/board/` columns, cards, drag/reorder, board view
- `src/features/persistence/` localStorage hydration/save/import/export
- `src/features/accessibility/` keyboard and aria behavior helpers
- `src/shared/` reusable UI and helpers
- `src/types/` canonical TypeScript models

Keep persistence logic outside UI components.

---

## 4. Code Organization

Organize code by feature/domain, not by large generic technical folders.

Required boundaries:
- UI components render state and dispatch intents; they should not implement storage internals.
- State modules own business transitions (create task, move task, delete project).
- Persistence adapter owns serialization/deserialization and storage error handling.
- Accessibility helpers own focus/announcement mechanics for keyboard and screen reader flows.

Preferred module style:
- Small files with single responsibilities
- Export one primary component/hook per file where practical
- Keep side effects centralized (hydration, save, keyboard listeners)

Do not create premature abstractions for features not present in PRD/Epics/Stories.

---

## 5. TypeScript Rules

1. Enable strict typing mindset from day one.
- No `any` unless temporary and justified with a TODO
- Prefer precise unions for domain values

2. Model core domain explicitly.
- `TaskStatus = "todo" | "in-progress" | "done"`
- `TaskPriority = "low" | "medium" | "high"`
- `BoardState`, `Project`, and `Task` types must be centralized in `src/types/`

3. Validate persisted data at boundaries.
- Treat localStorage payload as unknown input
- Parse and validate before using in app state
- Fail to safe empty state on malformed payload

4. Prefer immutability for state transitions.
- Do not mutate task/project arrays in-place in reducers or state updaters

5. Keep function contracts explicit.
- Annotate exported function input/output types
- Use discriminated unions or typed action objects for complex transitions

---

## 6. React Component Rules

1. Component responsibility
- One component should have one primary rendering concern
- Split very large components into presentational + behavior wrappers

2. Props and state
- Type all props explicitly
- Keep local state close to component only when shared state is unnecessary

3. Performance
- Avoid unnecessary re-renders in board-heavy lists
- Use stable keys (task/project IDs), never array indexes for reorderable lists

4. Accessibility defaults
- Keyboard focus must be visible
- Interactive controls must be reachable by keyboard
- Use semantic elements before ARIA workarounds

5. Events and shortcuts
- Keep keyboard shortcut handlers centralized and documented
- Prevent shortcut collisions where possible, and provide fallback interactions

6. No backend assumptions
- Components must not call API clients or server endpoints in this project scope

---

## 7. State Management Rules

Baseline strategy:
- React Context + Hooks for shared board state
- Local component state for UI-local concerns (open/closed, temporary input text)

State shape expectations:
- Canonical state contains projects, tasks, activeProjectId, and metadata needed by stories
- Keep one source of truth for task status and ordering

Transition rules:
- Every domain action should be deterministic and testable
- Save to localStorage after successful mutations
- Do not partially persist state slices that can create corruption

Persistence rules:
- Use one versioned root object in storage (as described in story constraints)
- On hydrate failure, start safe and show non-blocking message

---

## 8. Comments

Comment policy for this lab:
- Write comments for intent and non-obvious decisions, not trivial operations
- Keep comments short and current; remove stale comments during edits
- Prefer doc comments on exported utilities and complex state transition logic

Required comment cases:
- Why a shortcut behavior differs by OS/browser
- Why a storage fallback path exists
- Why an accessibility workaround is necessary

Avoid:
- Restating code line-by-line
- Large narrative blocks that drift from implementation

---

## 9. Domain Dictionary

- **Project**: A user-created workspace that groups related tasks.
- **Task**: A single work item placed in one Kanban column.
- **Board**: The main task management view with three columns.
- **Column**: One of the fixed Kanban statuses: To Do, In Progress, Done.
- **Task Status**: The current workflow state of a task: todo, in-progress, or done.
- **Task Priority**: The importance level of a task: low, medium, or high.
- **localStorage**: Browser storage used to persist the board state in MVP scope.
- **Import/Export**: JSON-based data portability feature for saving or restoring board data.

---

## 10. Testing Requirements

Testing level should match bootcamp scope but still enforce quality on critical behavior.

Minimum required automated coverage (once tests exist):
1. State logic
- Create/edit/delete project
- Create/edit/delete/move/reorder task
- Active project switching

2. Persistence behavior
- Save after mutation
- Hydrate success path
- Hydrate malformed payload fallback

3. Keyboard and accessibility behavior
- Core shortcuts (`Cmd/Ctrl+N`, movement shortcuts)
- Keyboard navigation between interactive elements
- Focus return behavior for dialogs/modals

4. Import/export paths
- JSON export contains required entities
- Invalid import data is rejected without state corruption

Manual QA checklist per story:
- Acceptance criteria from the story file are executed and checked
- Empty state and error state are verified
- Browser refresh persistence behavior is verified

---

## 11. Error Handling

Principles:
- Fail safely; never crash the whole board for recoverable issues
- Keep user edits in memory when persistence fails
- Show clear, non-blocking user feedback

Required handled cases:
1. localStorage unavailable/quota exceeded
- Catch write/read exceptions
- Keep in-memory state alive
- Surface actionable message

2. Malformed persisted JSON
- Catch parse/shape errors
- Reset to safe empty board state
- Do not enter crash loops

3. Invalid import file
- Reject with clear explanation
- Preserve existing state unchanged

4. Unsupported interaction edge cases
- Drag cancel should restore original position cleanly
- Keyboard action on invalid selection should no-op safely

---

## 12. Quality Criteria

A change is considered quality-compliant when:
- It stays within frontend-only scope (no backend/auth/database additions)
- It maps to a PRD requirement and at least one Epic/Story expectation
- It preserves three-column Kanban invariants
- It maintains localStorage persistence reliability and fallback behavior
- It maintains keyboard accessibility and visible focus behavior
- It avoids obvious performance regressions on typical board sizes
- It uses consistent naming and file placement conventions

For specs/docs contributions:
- Must be specific, measurable, and traceable
- Must include in-scope / out-of-scope clarity when relevant

---

## 13. Definition of Done

A task/story is done only when all are true:
1. Implementation satisfies story acceptance criteria
2. Code follows naming, typing, and organization standards in this file
3. Related tests are added/updated and pass
4. Error and edge-case paths are handled
5. Accessibility checks for changed UI paths are completed
6. Persistence behavior is verified when state logic changes
7. Documentation/spec links are updated if behavior changed
8. PR/review checklist items are resolved

---

## 14. Code Review Checklist

Reviewers (human or AI) should verify:

1. Scope alignment
- Does this change stay within frontend + localStorage boundaries?

2. Spec alignment
- Is there clear linkage to PRD/Epic/Story goals?

3. Correctness
- Are task/project transitions correct and deterministic?
- Are Kanban status and ordering invariants preserved?

4. Type safety
- Any `any` introduced without justification?
- Are exported contracts typed clearly?

5. Accessibility
- Keyboard flow still valid?
- Focus indicators and semantics preserved?

6. Error handling
- Storage/import failures handled without crash?

7. Test adequacy
- Are critical paths covered by tests or explicit manual validation notes?

8. Maintainability
- Is code readable, modular, and free of speculative abstraction?

---

## 15. Rules AI Assistants Must Follow

Mandatory assistant rules for this project:

1. Respect architecture boundaries
- Do not introduce backend APIs, server logic, database schemas, auth flows, or cloud sync.

2. Respect domain invariants
- Board must remain three columns (`To Do`, `In Progress`, `Done`) unless requirements explicitly change.

3. Respect persistence strategy
- localStorage is the persistence mechanism for MVP scope.

4. Respect repository conventions
- Keep file names and locations aligned with `agents.md` and `specs/` structure.

5. Keep output specific
- Reference actual project context (PRD, Epics, Stories), not generic boilerplate.

6. Keep changes minimal and traceable
- Do not refactor unrelated areas during targeted tasks.

7. Validate before finalizing
- Run available checks (lint/types/tests if present) and report what was verified.

8. Document assumptions when codebase is incomplete
- If `src/` or `package.json` is missing, state that clearly and provide standards aligned to current and planned structure.

9. Preserve accessibility and keyboard requirements
- Do not ship changes that break keyboard-only navigation or focus clarity.

10. Do not invent hidden infrastructure
- No references to message brokers, microservices, background workers, or server jobs in this lab scope.

---

## References

- `agents.md`
- `specs/prds/PRD-personal-task-board.md`
- `specs/epics/EPIC-001-task-and-project-management-foundation.md`
- `specs/epics/EPIC-002-efficient-task-workflows.md`
- `specs/epics/EPIC-003-data-management-privacy-portability.md`
- `specs/epics/EPIC-004-accessibility-responsive-design.md`
- `specs/stories/STORY-001.007-persist-data-localstorage.md`
- Other related story files under `specs/stories/`

**Last Updated:** May 6, 2026
