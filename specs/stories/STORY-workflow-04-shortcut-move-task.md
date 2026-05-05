# User Story: Move Selected Task with Keyboard Shortcut

**Story ID:** STORY-002.004  
**Epic:** Efficient Task Workflows with Keyboard Shortcuts and Drag-Drop / EPIC-002  
**Status:** BACKLOG  
**Created Date:** May 5, 2026  
**Last Updated:** May 5, 2026  

## 1. Story ID and Title

**Story ID:** STORY-002.004  
**Title:** Move Selected Task with Keyboard Shortcut

## 2. User Story

As a power user, I want to move a selected task left or right with keyboard shortcuts so that I can update status quickly without dragging.

## 3. Acceptance Criteria

### Criterion 1
**Given** a task card is selected  
**When** I press Ctrl+Shift+Right  
**Then** the task moves to the next workflow column if one exists

### Criterion 2
**Given** a task card is selected  
**When** I press Ctrl+Shift+Left  
**Then** the task moves to the previous workflow column if one exists

### Criterion 3
**Given** a task is already in the left-most or right-most column  
**When** I use the move shortcut toward an invalid direction  
**Then** no status change occurs and UI remains stable

### Criterion 4
**Given** a valid keyboard move occurs  
**When** the status update completes  
**Then** the task position and status persist after refresh

## 4. Technical Notes

### Constraints
- Applies only to the currently selected task
- Uses fixed three-column workflow order
- Must not require mouse interaction

### Dependencies
- [ ] STORY-workflow-03-shortcut-create-task.md
- [ ] STORY-workflow-01-drag-between-columns.md
- [ ] STORY-001.007 Persist Projects and Tasks to localStorage

### Edge Cases & Error Handling
- Handle no-selection state with clear feedback
- Prevent shortcut actions while modal dialogs are open
- Preserve keyboard focus on moved task where possible

## 5. Estimation

**Story Points:** 3  
**Estimated Days:** 2  
**Complexity:** Moderate

**Rationale:** Adds keyboard status transitions, boundary logic, selection state, and persistence checks.

## 6. INVEST Validation Checklist

### Independent
- [X] Adds a discrete keyboard movement feature

### Negotiable
- [X] No strict coupling to specific event framework

### Valuable
- [X] Supports speed-focused workflow management

### Estimable
- [X] Logic paths are explicit and bounded

### Small
- [X] Fits 1-3 days with clear scope

### Testable
- [X] Directional transitions and boundaries are testable

**Is this story INVEST-compliant?** [X] YES | [ ] NO
