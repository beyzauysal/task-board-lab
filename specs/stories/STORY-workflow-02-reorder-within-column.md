# User Story: Reorder Tasks Within a Column

**Story ID:** STORY-002.002  
**Epic:** Efficient Task Workflows with Keyboard Shortcuts and Drag-Drop / EPIC-002  
**Status:** BACKLOG  
**Created Date:** May 5, 2026  
**Last Updated:** May 5, 2026  

## 1. Story ID and Title

**Story ID:** STORY-002.002  
**Title:** Reorder Tasks Within a Column

## 2. User Story

As a power user, I want to reorder tasks inside the same column so that I can prioritize what I work on next.

## 3. Acceptance Criteria

### Criterion 1
**Given** a column has at least two tasks  
**When** I drag one task above or below another task in that column  
**Then** the new order is reflected immediately in the UI

### Criterion 2
**Given** I reorder tasks in a column  
**When** the reorder completes  
**Then** the resulting order is stored in application state

### Criterion 3
**Given** I refresh the page after reorder  
**When** board data is restored from localStorage  
**Then** the same task order is preserved

### Criterion 4
**Given** I attempt to reorder in an empty or single-item column  
**When** I interact with drag behavior  
**Then** no error occurs and layout remains stable

## 4. Technical Notes

### Constraints
- Works only inside one column for this story
- No filtering/sorting logic added here
- Must not affect task status values

### Dependencies
- [ ] STORY-workflow-01-drag-between-columns.md
- [ ] STORY-001.007 Persist Projects and Tasks to localStorage

### Edge Cases & Error Handling
- Avoid index corruption after rapid drag operations
- Preserve scroll position while reordering long columns
- Handle duplicate task IDs defensively in development mode

## 5. Estimation

**Story Points:** 2  
**Estimated Days:** 1.5  
**Complexity:** Moderate

**Rationale:** Extends existing drag behavior with ordering persistence and column-local constraints.

## 6. INVEST Validation Checklist

### Independent
- [X] Delivers a distinct prioritization capability

### Negotiable
- [X] No forced implementation details

### Valuable
- [X] Improves day-to-day planning and focus

### Estimable
- [X] Inputs/outputs are clearly defined

### Small
- [X] Bounded to one interaction type

### Testable
- [X] Order changes are deterministic and testable

**Is this story INVEST-compliant?** [X] YES | [ ] NO
