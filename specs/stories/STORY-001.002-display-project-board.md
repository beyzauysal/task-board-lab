# User Story: Display Active Project Board

**Story ID:** STORY-001.002  
**Epic:** Task and Project Management Foundation / EPIC-001  
**Status:** BACKLOG  
**Created Date:** May 5, 2026  
**Last Updated:** May 5, 2026  
**Assignee:** [To Be Assigned]  

---

## 1. Story ID and Title

**Story ID:** STORY-001.002

**Title:** Display Active Project Board

Example format: `STORY-001.002: Display Active Project Board`

---

## 2. User Story

As a solo developer, I want to see the active project's Kanban board with To Do, In Progress, and Done columns so that I can understand task status at a glance.

### Context

Once a project exists, the primary value of the app is the board view. This story focuses on rendering the core three-column experience for the selected project.

---

## 3. Acceptance Criteria

### Criterion 1

**Given** at least one project exists  
**When** the user selects a project from the project list  
**Then** the app displays that project as the active project with exactly three columns named `To Do`, `In Progress`, and `Done`

### Criterion 2

**Given** the active project has no tasks yet  
**When** the board is rendered  
**Then** all three columns are visible in an empty state with column headers still shown

### Criterion 3

**Given** the active project contains tasks in one or more statuses  
**When** the board is rendered  
**Then** each task appears only in the column that matches its status

### Criterion 4

**Given** the board is visible  
**When** the user views the column headers  
**Then** each header shows the current task count for that column

---

## 4. Technical Notes

### Constraints

- Must render correctly on standard desktop widths first
- Must use the fixed three-column workflow defined in the PRD
- Board render for a typical project should complete in under 100ms after project switch

### Dependencies

- [ ] STORY-001.001 Create a New Project
- [ ] Shared task and project data shape is defined in TypeScript
- [ ] localStorage persistence can be connected later in STORY-001.007

### Edge Cases & Error Handling

- Handle projects with zero tasks without collapsing layout
- Handle unknown task statuses by excluding invalid tasks from render and logging safely in development
- Handle missing active project by showing a guided empty state

### Implementation Notes (Optional)

Use a status-to-column mapping that keeps rendering deterministic and easy to test.

---

## 5. Estimation

### Effort Estimate

**Story Points:** 2 points  
**OR Estimated Days:** 1 day (1-3 days recommended)

### Estimation Rationale

This story is mostly UI composition and status-based rendering. Complexity is low because it relies on a fixed board structure and does not yet include drag-and-drop.

### Complexity Level

[X] Simple (Low risk, well-understood, straightforward) | [ ] Moderate (Some unknowns, moderate effort) | [ ] Complex (High risk, significant unknowns, requires spike/investigation)

---

## 6. INVEST Validation Checklist

### ✓ Independent
- [X] This story can be completed independently without blocking or being blocked by other stories
- [X] The story doesn't depend on another story being done first (except documented dependencies in Technical Notes)
- [X] This story could theoretically be done by a single team or person

**If not met:** Does this story need to be split? Should dependencies be clarified?

### ✓ Negotiable
- [X] The story focuses on WHAT the user wants, not HOW to build it
- [X] Implementation details are flexible and open to team discussion
- [X] The acceptance criteria define the outcome, not the implementation approach
- [X] There's room for the team to propose alternative solutions

**If not met:** Is the story too prescriptive? Can we remove implementation details and focus on user needs?

### ✓ Valuable
- [X] This story delivers clear value to the user or business
- [X] Completing this story moves us toward the Epic goal
- [X] The user benefit is explicitly stated in the user story
- [X] The story links back to a PRD goal or success metric

**If not met:** Why are we building this? What value does it create?

### ✓ Estimable
- [X] The team has enough information to estimate the effort
- [X] There are no major unknowns that would prevent estimation
- [X] The story is clear enough that different team members would estimate similarly
- [X] The story is small enough to estimate with confidence

**If not met:** Do we need to do a spike/investigation story first? Is the story too vague or too large?

### ✓ Small
- [X] This story can be completed in 1-3 days of work by one developer
- [X] The story is small enough to fit in a single sprint
- [X] Completing this story won't delay other work significantly
- [X] The story is not doing multiple things at once

**If not met:** Can we split this story into smaller stories?

### ✓ Testable
- [X] Acceptance criteria are clear and objective — not subjective
- [X] A QA team member could verify this story without clarification
- [X] We can measure whether the acceptance criteria are met
- [X] No criterion uses vague language like "works well," "is easy," or "looks good"

**If not met:** Do acceptance criteria need to be more specific and measurable?

### Summary

**Is this story INVEST-compliant?** [X] YES | [ ] NO

If NO, what needs to be refined?
- [ ] Story needs to be split into smaller stories
- [ ] Story needs clearer acceptance criteria
- [ ] Dependencies need to be documented
- [ ] Story needs to focus more on user value
- [ ] Other: [DESCRIBE]

---

## Acceptance Criteria Verification

| Criterion | Pass | Notes |
|-----------|------|-------|
| Criterion 1 | [ ] | [QA notes] |
| Criterion 2 | [ ] | [QA notes] |
| Criterion 3 | [ ] | [QA notes] |
| Criterion 4 | [ ] | [QA notes] |
| Criterion 5 | [ ] | N/A |

**Overall Status:** [ ] All criteria met (DONE) | [ ] Some criteria not met (NEEDS WORK)

---

## Common Mistakes to Avoid

### 1. **Mixing Interaction Modes**
- ❌ Mistake: Adding drag-and-drop into this story
- ✓ Fix: Keep this story focused on rendering and viewing the board only

### 2. **Hiding Empty Columns**
- ❌ Mistake: Only showing columns when they contain tasks
- ✓ Fix: Always show all three columns to preserve the workflow model

### 3. **Unclear Status Mapping**
- ❌ Mistake: Letting tasks appear in multiple columns
- ✓ Fix: Render each task in exactly one status column

---

## Definition of Done Checklist

- [ ] All acceptance criteria have been met and verified by QA
- [ ] Code has been peer reviewed and approved
- [ ] Tests have been written and are passing
- [ ] Documentation has been updated if needed
- [ ] No new bugs or issues have been introduced
- [ ] Code follows team standards and conventions
- [ ] Story can be merged and deployed to production

---

## Related Documents & Links

- **Epic:** [specs/epics/EPIC-001-task-and-project-management-foundation.md](../../specs/epics/EPIC-001-task-and-project-management-foundation.md)
- **Related Stories:** STORY-001.001, STORY-001.003, STORY-001.007
- **Design Doc/Mockup:** [To be added]
- **Technical Doc:** [To be added]
- **PR/Code Review:** [To be added]

---

## Discussion & Notes

**Key Decisions:**
- Three columns are fixed and always visible
- Task counts are shown in headers from the first release

**Questions/Clarifications:**
- Should empty columns include helper copy or only headers?
- Should the active project name appear above the board?

**Comment Thread:**
[Add comments here as the story progresses]
