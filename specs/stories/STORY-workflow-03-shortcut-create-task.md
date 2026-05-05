# User Story: Create Task with Keyboard Shortcut

**Story ID:** STORY-002.003  
**Epic:** Efficient Task Workflows with Keyboard Shortcuts and Drag-Drop / EPIC-002  
**Status:** BACKLOG  
**Created Date:** May 5, 2026  
**Last Updated:** May 5, 2026  

## 1. Story ID and Title

**Story ID:** STORY-002.003  
**Title:** Create Task with Keyboard Shortcut

## 2. User Story

As a developer, I want to press a keyboard shortcut to open task creation so that I can capture tasks without leaving the keyboard.

## 3. Acceptance Criteria

### Criterion 1
**Given** I am viewing an active project board  
**When** I press Ctrl+N (or Cmd+N on macOS)  
**Then** task input is focused and ready for typing in the To Do flow

### Criterion 2
**Given** shortcut-triggered input is focused  
**When** I enter a valid title and submit  
**Then** a new task is created successfully in To Do

### Criterion 3
**Given** no active project is selected  
**When** I press the shortcut  
**Then** the app shows a clear non-blocking message explaining why task creation cannot start

### Criterion 4
**Given** I am using the shortcut in a text field unrelated to task creation  
**When** I press Ctrl+N/Cmd+N  
**Then** existing text input behavior is not broken

## 4. Technical Notes

### Constraints
- Support Windows, Linux, and macOS key patterns
- Keep behavior frontend-only with no external dependencies
- Avoid conflict with browser defaults where possible

### Dependencies
- [ ] STORY-001.003 Create a Task in To Do
- [ ] STORY-001.002 Display Active Project Board

### Edge Cases & Error Handling
- Handle blocked keyboard events in certain browsers
- Prevent repeated keydown from opening multiple create states
- Preserve accessibility focus flow after shortcut use

## 5. Estimation

**Story Points:** 2  
**Estimated Days:** 1  
**Complexity:** Simple

**Rationale:** Small scoped enhancement around event handling and focus management tied to existing creation flow.

## 6. INVEST Validation Checklist

### Independent
- [X] Adds a standalone keyboard interaction

### Negotiable
- [X] Outcome-focused, implementation-flexible

### Valuable
- [X] Increases speed for power users

### Estimable
- [X] Limited and measurable behavior

### Small
- [X] Can be completed in 1-3 days

### Testable
- [X] Shortcut and fallback paths are testable

**Is this story INVEST-compliant?** [X] YES | [ ] NO
