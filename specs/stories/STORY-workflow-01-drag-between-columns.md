# User Story: Drag Tasks Between Columns

**Story ID:** STORY-002.001  
**Epic:** Efficient Task Workflows with Keyboard Shortcuts and Drag-Drop / EPIC-002  
**Status:** BACKLOG  
**Created Date:** May 5, 2026  
**Last Updated:** May 5, 2026  

## 1. Story ID and Title

**Story ID:** STORY-002.001  
**Title:** Drag Tasks Between Columns

## 2. User Story

As a freelance developer, I want to drag tasks between To Do, In Progress, and Done so that I can update status quickly without extra clicks.

## 3. Acceptance Criteria

### Criterion 1
**Given** I have tasks visible on the board  
**When** I drag a task from one column to another  
**Then** the task appears in the target column immediately

### Criterion 2
**Given** I drop a task into a new column  
**When** the drop action completes  
**Then** the task status value is updated in application state

### Criterion 3
**Given** I start dragging a task  
**When** I hover over valid drop zones  
**Then** the UI shows visual feedback for allowed drop targets

### Criterion 4
**Given** I cancel drag or drop outside valid targets  
**When** the interaction ends  
**Then** the task returns to its original position with no status change

## 4. Technical Notes

### Constraints
- Frontend only in React + TypeScript
- No server calls or cloud sync
- Drag action should feel responsive under typical board size

### Dependencies
- [ ] STORY-001.002 Display Active Project Board
- [ ] STORY-001.003 Create a Task in To Do
- [ ] STORY-001.007 Persist Projects and Tasks to localStorage

### Edge Cases & Error Handling
- Handle fast repeated drag operations without duplicate tasks
- Prevent drag interaction from breaking keyboard focus state
- Ensure unsupported browsers degrade gracefully to non-drag behavior

## 5. Estimation

**Story Points:** 3  
**Estimated Days:** 2  
**Complexity:** Moderate

**Rationale:** Includes drag interaction handling, status updates, and visual feedback but remains limited to cross-column movement only.

## 6. INVEST Validation Checklist

### Independent
- [X] Can be developed and tested independently

### Negotiable
- [X] Defines outcome, not implementation library

### Valuable
- [X] Directly improves task workflow speed

### Estimable
- [X] Scope is clear and bounded

### Small
- [X] Fits 1-3 days for one developer

### Testable
- [X] Acceptance criteria are objective and verifiable

**Is this story INVEST-compliant?** [X] YES | [ ] NO
