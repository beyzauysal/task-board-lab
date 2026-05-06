# Development Workflow: Task Board Lab

## Purpose

This document defines how work should move from requirements to reviewed output in Task Board Lab, with special focus on helping AI assistants produce correct, scoped, and reviewable contributions.

AI assistants should use this workflow together with:
- `memory-banks/architecture/overview.md`
- `memory-banks/conventions/coding-standards.md`
- `memory-banks/domain/glossary.md`
- `specs/prds/PRD-personal-task-board.md`
- `specs/epics/*`
- `specs/stories/*`
- `agents.md`

Project reality this workflow assumes:
- Frontend-only React/Vite/TypeScript product direction
- Single-user scope
- localStorage persistence
- No backend/database/authentication systems
- Current repository is spec-first (no `src/` and no `package.json` yet)

## Development Process

### From Idea to Working Implementation

1. Start from PRD requirements
- Read `specs/prds/PRD-personal-task-board.md` first.
- Identify exact functional and non-functional requirements relevant to the requested change.

2. Break requirements into Epics
- Map requirement area to the correct epic in `specs/epics/`.
- Example mapping:
	- Core board/task/project behavior -> EPIC-001
	- Drag-drop/shortcuts -> EPIC-002
	- Persistence/import/export/privacy -> EPIC-003
	- Accessibility/responsive behavior -> EPIC-004

3. Break Epics into User Stories
- Use existing stories under `specs/stories/` when available.
- If a story is missing, draft one using the project story template before implementation.

4. Select one User Story
- Implement one story at a time for small, reviewable increments.
- Avoid mixing unrelated stories in a single change.

5. Review acceptance criteria
- Treat Given/When/Then acceptance criteria as the source of truth.
- Highlight edge cases (empty title, localStorage errors, invalid drops, keyboard/focus behavior).

6. Plan implementation
- Align plan with architecture boundaries:
	- UI concerns in components
	- state transitions in state layer
	- persistence in localStorage adapter
- Confirm no backend/auth/database additions are needed.

7. Implement the feature
- Keep changes minimal and traceable to the selected story.
- Preserve domain invariants:
	- three statuses only (`todo`, `in-progress`, `done`)
	- one task in one column at a time
	- stable task identity on edit

8. Test locally
- Run available checks if configured (tests/lint/type-check/build).
- If tooling is not configured yet, run explicit manual checks against acceptance criteria.

9. Self-review against coding standards and business rules
- Validate against:
	- `memory-banks/conventions/coding-standards.md`
	- `memory-banks/domain/glossary.md`
- Confirm no scope drift and no unrelated refactors.

10. Update documentation if needed
- Update spec/memory-bank files if behavior, rules, or assumptions changed.
- Keep architecture/coding/domain/workflow docs synchronized with reality.

11. Commit changes
- Use focused, single-purpose commits.
- Message should include story or scope intent.

12. Push to GitHub
- Push feature branch to remote.

13. Create Pull Request if required
- Open PR against `main` using template/checklist from this document.

14. Review and merge
- Address review feedback.
- Merge only when acceptance criteria, checks, and documentation requirements are met.

## Branching Strategy

Use GitHub Flow.

This strategy was selected because Task Board Lab is a solo or small-team bootcamp project. GitHub Flow keeps the process simple: one active branch per change, merged quickly back to `main`. There is no need for long-running release branches or environment-specific branches given the single-user, static-hosted scope of this project. Short-lived feature branches reduce the risk of merge conflicts and keep code review focused.

- Pattern: short-lived topic branches from `main`, one focused change per branch, merge via PR.
- Main branch: `main`
- Branch naming format:
	- `feature/<short-kebab-name>`
	- `bugfix/<short-kebab-name>`
	- `docs/<short-kebab-name>`

Examples of valid branch names:
- `feature/add-task-form`
- `feature/task-drag-and-drop`
- `bugfix/fix-empty-task-validation`
- `docs/update-memory-bank`

Ideal protection rules for `main` (if repository settings allow):
- Require pull request before merge
- Require at least one review (self-review acceptable only for solo bootcamp projects if policy allows)
- Require status checks to pass (build/test/lint when configured)
- Disallow force-push to `main`

## Pull Request Process

### Before Creating PR Checklist

- Story scope is clear and limited
- Acceptance criteria are explicitly checked
- No unrelated features or refactors added
- Local checks completed (automated or manual)
- Documentation updated when behavior/rules changed

### PR Requirements

- Title uses clear scope, for example: `feat: implement STORY-001.003 task creation in To Do`
- Description links relevant PRD/Epic/Story files
- PR explains what changed, why, and how it was validated
- Include screenshots/GIF for UI changes when applicable

### PR Description Template

```md
## Summary
- What changed?
- Why this change?

## Traceability
- PRD: specs/prds/PRD-personal-task-board.md
- Epic: specs/epics/EPIC-xxx-....md
- Story: specs/stories/STORY-xxx-....md

## Acceptance Criteria Verification
- [ ] Criterion 1 ...
- [ ] Criterion 2 ...
- [ ] Criterion 3 ...

## Testing
- Automated:
	- [ ] unit/component tests passed
	- [ ] lint/type-check/build passed
- Manual:
	- [ ] scenario A
	- [ ] scenario B

## Scope Check
- [ ] No backend/database/auth additions
- [ ] No unrelated feature work

## Docs Updated
- [ ] Not needed
- [ ] Updated: <file paths>
```

### Code Review Checklist

- All tests passing locally (or manual checks documented if tests not configured yet)
- Project builds successfully (when build tooling exists)
- Code follows `memory-banks/conventions/coding-standards.md`
- Domain rules in `memory-banks/domain/glossary.md` are respected
- Acceptance criteria are fully satisfied
- No unrelated features added
- Documentation updated if needed
- Accessibility and keyboard behavior not regressed
- localStorage behavior validated for state-changing features

## Testing Strategy

Testing should be realistic for an individual bootcamp project while still protecting core flows.

### Unit Tests

Prioritize logic-heavy areas:
- Task/project state transitions (create/edit/delete/move/reorder)
- Status lifecycle rules (`todo`, `in-progress`, `done`)
- localStorage serialization/hydration and malformed-data fallback

### Component Tests (if tools are configured)

Prioritize user-visible behavior:
- Task creation form validation (empty title rejected)
- Column rendering by status
- Drag-drop state updates (or equivalent handlers)
- Keyboard shortcut interactions and focus behavior

### Manual Testing

Always run manual scenarios for changed behavior:
- Task creation in `To Do`
- Task editing preserves identity
- Task deletion removes from board
- Status change updates correct column only
- localStorage persistence across refresh
- Error behavior for invalid persisted data/import failures

### What to Test for Core Features

1. Task creation
- Valid title creates task in correct column
- Empty/whitespace title blocked with clear validation

2. Task editing
- Title/description/priority/tags update correctly
- Task id remains unchanged

3. Task deletion
- Confirmation works
- Task disappears from board and state

4. Task status change
- Move between columns updates status accurately
- Task appears in exactly one column

5. localStorage persistence (if used)
- Save after mutation
- Hydration on reload
- Safe fallback on malformed storage payload

### Coverage Expectations (Bootcamp Realistic)

- Focus on critical workflow paths, not exhaustive edge-case matrix
- Target practical confidence over perfect percentages
- As a guideline: cover high-risk logic and at least one happy-path + one failure-path per core feature
- This project prioritizes meaningful coverage of critical flows (task creation, status change, localStorage persistence) over hitting a strict percentage target. A well-tested persistence adapter and state transition layer is more valuable than artificially padding coverage numbers.

### When to Write Tests

- Write or update tests during implementation of each story
- Do not postpone all tests to the end of a module
- Add regression tests when fixing bugs

## Deployment Process

Current repo status:
- Implementation runtime and deployment config are not yet present.
- Use this process once app scaffold/build scripts exist.

### Local Development Steps

1. Pull latest `main`
2. Create branch via GitHub Flow
3. Implement one story scope
4. Run local checks (tests/lint/type-check/build when available)
5. Run manual verification scenarios

### Production Build Steps

When scripts are available:
1. Install dependencies
2. Run build command
3. Verify generated static artifacts

### Optional Static Hosting Deployment

Valid hosting approaches for this project:
- GitHub Pages
- Netlify
- Vercel

Use one static host only; do not introduce server infrastructure.

### Manual Deployment Steps

1. Build static assets
2. Upload/publish to chosen static host
3. Confirm application loads correctly
4. Verify board interactions and localStorage hydration

### Automated CI/CD Steps (configured or ideal)

If CI is configured later, recommended minimal pipeline:
1. On pull request: lint + type-check + tests
2. On merge to `main`: build and deploy static assets
3. Post-deploy: smoke test app load and persistence hydration

### Verification After Deployment

- App loads without crash
- Board displays three columns correctly
- Task creation/edit/delete/move works
- localStorage persistence survives refresh
- Keyboard and focus behavior remains functional

### Rollback Procedure

1. Re-deploy previous known-good static build
2. Re-verify critical flows (create/move/delete/persist)
3. If issue is data-shape related, apply safe fallback/migration handling in next patch

Notes:
- User data is browser-local, so rollback focuses on static asset version restoration
- Keep schema evolution additive to reduce break risk

## AI Assistant Workflow Rules

1. Always check architecture, coding standards, domain glossary, and workflow files before generating code.

2. Do not invent backend/database/auth/deployment complexity unless it exists in this repository.

3. Preserve working code and existing behavior unless the story explicitly changes it.

4. Implement one story at a time.

5. Use story acceptance criteria as the definition of success.

6. Keep changes small, focused, and reviewable.

7. Maintain traceability in outputs:
- PRD -> Epic -> Story mapping must be clear.

8. Respect core domain/business rules:
- Non-empty task titles
- Single valid status per task
- Task appears in one column only
- localStorage persistence for state changes

9. Report what was validated.
- If automation is unavailable, explicitly list manual checks performed.

10. Do not silently introduce scope changes.
- If a requested change conflicts with project scope, call it out and propose in-scope alternatives.

11. Prefer existing project patterns over introducing new abstractions.
- If the codebase already handles a concern in a particular way (for example state transitions, persistence calls, or focus management), extend that pattern rather than introducing a parallel solution.

---

**Last Updated:** May 6, 2026
