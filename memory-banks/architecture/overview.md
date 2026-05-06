# Task Board Lab - Architecture Overview

## 1. Purpose

This document gives AI assistants a concrete architectural map of Task Board Lab so generated output stays aligned with the real project direction.

It exists to prevent generic or off-scope suggestions such as adding backend APIs, databases, or authentication, which are explicitly out of scope for this lab project.

Primary use:
- Guide implementation decisions for a frontend-only personal task board
- Keep generated artifacts aligned with PRD, Epics, Stories, and project conventions
- Ensure architectural consistency when code and docs are created incrementally

---

## 2. Project Summary

Task Board Lab is a single-user, frontend-only personal task management application for solo developers handling 2-3 concurrent projects.

Product shape defined in the current specs:
- Kanban-style board with exactly three workflow columns: `To Do`, `In Progress`, `Done`
- Multiple projects, each with its own board state
- Task CRUD, project CRUD, priority (`Low`/`Medium`/`High`), tags, descriptions
- Drag-and-drop between columns and reorder within a column
- Keyboard-first workflows (for example `Cmd/Ctrl+N`, column movement shortcuts)
- localStorage persistence with export/import JSON
- Accessibility and responsive behavior as first-class requirements

This is explicitly a React + Vite + TypeScript architecture with browser-only persistence.

---

## 3. System Architecture

### Architectural Scope

Current architecture is a browser-executed Single Page Application (SPA):
- Client rendering only
- No backend runtime
- No server-side data layer
- No user authentication boundary

### Runtime Boundaries

1. Presentation layer
- Board UI, project switcher UI, task cards, dialogs/forms, keyboard/focus states

2. Application/state layer
- Project/task state transitions
- Active project selection
- Undo/redo scope (if included per stories)
- Validation and error state

3. Persistence layer (browser localStorage)
- Save board snapshot after mutations
- Restore state at startup
- Handle parse/storage failures gracefully
- Export/import serialization boundary

### External Dependencies Boundary

Allowed:
- Browser APIs (localStorage, file download/upload)
- Frontend npm packages used in React app setup

Not allowed unless future scope explicitly changes:
- REST/GraphQL APIs
- Databases
- Cloud sync services
- Authentication providers

---

## 4. Architecture Pattern

Primary pattern: component-driven SPA with unidirectional state updates.

Recommended implementation model (consistent with project conventions):
- React function components
- React Hooks for local behavior
- React Context + Hooks for shared board state (upgrade path to Redux only if complexity justifies it)
- Event-driven state transitions for user actions (create, edit, move, delete)
- Persistence adapter module that isolates localStorage read/write and schema versioning

Why this pattern fits this lab:
- Small/medium feature set with high UI interaction density
- Fast iteration and low setup overhead required by lab scope
- Keeps cognitive load low for solo and assistant-driven development

---

## 5. Key Components and Responsibilities

The exact code modules are not scaffolded in this repository yet, but required responsibilities are clear from specs.

1. App Shell
- Bootstraps application
- Hydrates initial state from persistence layer
- Provides global providers (state, theme if added later, keyboard manager)

2. Project Navigation Panel
- List projects
- Show per-project counts (To Do / In Progress / Done)
- Create/rename/delete project entry points
- Set active project

3. Board View
- Render three fixed columns for active project
- Route task cards to columns by `status`
- Show column task counts
- Handle empty-state messaging

4. Column Component
- Render column metadata and ordered task list
- Accept drag/drop targets for cross-column and in-column ordering

5. Task Card + Task Editor
- Display title, optional description, priority, tags, timestamps
- Trigger edit/delete actions
- Expose keyboard focus/selection affordances

6. Workflow Interaction Layer
- Drag-and-drop handlers and validation
- Keyboard shortcuts for task create/move
- Optional undo/redo action stack hooks

7. Persistence Adapter
- Serialize canonical board state to localStorage
- Deserialize and validate loaded state
- Handle malformed payloads and storage exceptions
- Support schema version key for forward compatibility

8. Import/Export Module
- Export full board snapshot as JSON
- Validate and import JSON without partial corruption
- Merge/replace behavior as defined by future implementation decisions

9. Accessibility/Feedback Utilities
- Focus management helpers
- ARIA live announcements for critical status changes
- Non-blocking notifications for errors (e.g., storage write failure)

---

## 6. Data Model

Data model below is inferred directly from PRD/Epics/Stories and should be treated as the canonical assistant target until code defines exact types.

### Core Entities

1. Project
- `id: string`
- `name: string`
- `createdAt: string` (ISO)
- `updatedAt: string` (ISO)

2. Task
- `id: string`
- `projectId: string`
- `title: string`
- `description?: string`
- `status: "todo" | "in-progress" | "done"`
- `priority: "low" | "medium" | "high"`
- `tags: string[]`
- `orderIndex: number` (for stable in-column ordering)
- `createdAt: string` (ISO)
- `updatedAt: string` (ISO)

3. BoardState (root persisted object)
- `version: number`
- `projects: Project[]`
- `tasks: Task[]`
- `activeProjectId: string | null`
- `lastSavedAt: string` (ISO)

Optional extension fields (only if stories require):
- `uiStateByProject` for preserved scroll/expanded card context
- `history` for undo/redo snapshots or action stack metadata

### Invariants

- Every task must belong to an existing `projectId`
- Status must be one of the three fixed columns
- Priority must be one of `low/medium/high`
- Tags are plain text labels, normalized by trim/case rules if adopted

---

## 7. Data Flow

### Startup (Hydration)

1. App shell loads
2. Persistence adapter reads localStorage key
3. Data is parsed + schema-validated
4. On success: state initializes from persisted snapshot
5. On failure: state initializes to safe empty board and surfaces non-blocking warning

### Mutation Flow (Create/Edit/Move/Delete)

1. User action from UI (button, drag/drop, keyboard shortcut)
2. Action validated against model constraints
3. In-memory state updates immutably
4. Board re-renders derived column/task views
5. Persistence adapter writes full or minimal consistent snapshot
6. Success/failure feedback emitted (silent success, visible warning on failure)

### Export Flow

1. User triggers export
2. Current canonical state serialized
3. Browser download generated JSON file
4. No mutation to board state

### Import Flow

1. User selects JSON file
2. Parse + validate schema/version
3. If valid, replace current board state (or merge if future decision)
4. Persist imported state and refresh derived UI
5. On invalid file, show clear error and retain existing state

---

## 8. Communication Patterns

Because there is no backend, all communication is in-process within the browser.

1. UI -> State actions
- Components dispatch intent (`createTask`, `moveTask`, `deleteProject`, etc.)

2. State -> Persistence
- Post-mutation persistence call writes to localStorage

3. Persistence -> UI feedback
- Exceptions produce non-blocking UX signal (toast/inline status)

4. Accessibility announcements
- Significant changes (e.g., task moved column) should emit ARIA-live updates

5. No network communication path
- Any assistant-generated code that introduces HTTP clients, API services, or auth token flows is architecturally incorrect for current scope

---

## 9. Tech Stack

Project-standard stack from conventions and specs:
- React 18
- Vite
- TypeScript
- Styling approach to be finalized (`CSS`, `TailwindCSS`, or `styled-components`)
- State management: React Context + Hooks (Redux only if complexity outgrows baseline)
- Persistence: browser localStorage
- Hosting target: static hosting (for example Vercel, Netlify, GitHub Pages)

Important current repository state:
- This workspace currently contains spec and memory-bank artifacts
- Application runtime files such as `src/` and `package.json` are not present yet
- AI outputs should therefore align to the planned stack above without inventing backend infrastructure

---

## 10. Folder Structure Guidance

Current documented structure:

- `specs/templates/` -> PRD/Epic/Story templates
- `specs/prds/` -> generated PRD documents
- `specs/epics/` -> generated Epic documents
- `specs/stories/` -> generated Story documents
- `.github/prompts/` -> reusable Copilot prompt files
- `memory-banks/` -> persistent project context for assistants
- `agents.md` -> project conventions and assistant guardrails

When app source is scaffolded, follow this frontend-oriented shape:

- `src/app/` -> app bootstrap and global providers
- `src/features/projects/` -> project CRUD and project list
- `src/features/board/` -> board/columns/task-card interactions
- `src/features/persistence/` -> localStorage adapter + import/export services
- `src/features/accessibility/` -> focus and announcement helpers
- `src/shared/` -> reusable UI and utility modules
- `src/types/` -> canonical TypeScript domain models

Guidance intent:
- Keep boundaries feature-first, not layer-spaghetti
- Isolate persistence logic from UI components
- Keep domain model types centralized and reused

---

## 11. Deployment

Deployment model is static frontend hosting:

1. Build React/Vite bundle
2. Publish static assets to host (Vercel/Netlify/GitHub Pages equivalent)
3. Serve as SPA with client routing fallback if routing is introduced

Why this fits:
- No backend services to provision
- Low operational overhead (aligned with solo-developer use case)
- Fast and inexpensive hosting for personal tooling

Runtime behavior after deploy:
- User data remains on each browser via localStorage
- Deployments do not migrate remote data because no remote data exists

---

## 12. CI/CD

CI/CD is not fully defined in existing files yet, but architecture-consistent minimum pipeline should be:

1. On PR:
- Lint + type-check + tests
- Validate no backend dependencies were introduced accidentally

2. On merge to main:
- Build static bundle
- Deploy to static hosting target

3. Post-deploy checks:
- Smoke-test board load
- Verify hydration from existing localStorage does not crash on older snapshots

Assistant constraint:
- Do not assume complex multi-environment backend pipelines (none exist in this architecture)

---

## 13. Rollback Approach

For this frontend-only architecture, rollback has two dimensions.

1. Application artifact rollback
- Re-deploy prior known-good static build
- Fast because only static assets change

2. Client data compatibility rollback
- Persisted data lives in localStorage per user device
- Use schema version field in `BoardState` to protect against incompatible releases
- If schema changes are introduced in future, include migration and safe fallback path

Recommended rollback-safe practice:
- Prefer additive schema evolution
- Keep import/export available so users can self-backup before disruptive updates
- Fail safely to readable empty-state + guidance, never white-screen crash

---

## 14. Architectural Constraints for AI Assistants

These are mandatory constraints for generated code/docs:

1. Frontend-only boundary
- Do not add backend APIs, server runtimes, message queues, or database layers

2. Persistence boundary
- Use browser localStorage as primary persistence for MVP scope

3. Workflow boundary
- Preserve fixed three-column Kanban workflow: To Do, In Progress, Done

4. User model boundary
- Single-user model only; no authentication, roles, or collaboration features

5. Quality boundary
- Respect accessibility requirements (WCAG 2.1 AA intent) and keyboard-first interactions

6. Performance boundary
- Keep interaction loops responsive for typical board sizes

7. Repository boundary
- Follow naming and placement rules from `agents.md` and existing `specs/` conventions

8. Spec alignment boundary
- PRD -> Epic -> Story traceability must be maintained in generated outputs

If a request conflicts with these constraints, assistants should call out the conflict and propose an in-scope alternative.

---

## 15. Key Architectural Decisions

1. Decision: React + Vite + TypeScript frontend architecture
- Why: Matches project conventions, supports fast feedback loops, and keeps implementation maintainable for solo development.

2. Decision: Browser-only persistence via localStorage
- Why: Core value proposition includes privacy, offline behavior, and zero backend operations.

3. Decision: Fixed three-column Kanban model in MVP
- Why: Prevents scope creep and aligns with requirements for quick visual workflow clarity.

4. Decision: Component-driven UI with centralized shared state (Context + Hooks)
- Why: Sufficient for current complexity while remaining simpler than introducing heavyweight state tooling too early.

5. Decision: Import/export JSON as portability mechanism
- Why: Provides backup and migration path without introducing cloud sync complexity.

6. Decision: Accessibility and keyboard support as architectural requirements, not polish
- Why: Directly tied to PRD goals and ensures the app is usable for keyboard-first and assistive technology users.

7. Decision: Static hosting deployment model
- Why: Fits zero-backend architecture and minimizes operational burden.

8. Decision: Schema versioning in persisted root state
- Why: Enables safe evolution and rollback in a client-stored data architecture.

---

**Last Updated:** May 6, 2026  
**Source Inputs:** `agents.md`, `memory-banks/README.md`, `specs/prds/PRD-personal-task-board.md`, `specs/epics/EPIC-001..004`, selected `specs/stories/*` documents
