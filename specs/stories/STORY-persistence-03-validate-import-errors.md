# User Story: Validate Import File and Show Clear Errors

**Story ID:** STORY-003.003  
**Epic:** Data Management, Privacy, and Portability / EPIC-003  
**Status:** BACKLOG  
**Created Date:** May 5, 2026  
**Last Updated:** May 5, 2026  

## 1. Story ID and Title

**Story ID:** STORY-003.003  
**Title:** Validate Import File and Show Clear Errors

## 2. User Story

As a user, I want clear import validation errors so that I can fix problems and safely retry without losing current data.

## 3. Acceptance Criteria

### Criterion 1
**Given** I select a malformed or non-JSON file  
**When** the app validates import input  
**Then** import is rejected with a specific error message

### Criterion 2
**Given** I select JSON that does not match expected board schema  
**When** validation runs  
**Then** import is blocked and schema mismatch guidance is displayed

### Criterion 3
**Given** import validation fails  
**When** the error state is shown  
**Then** existing board data remains unchanged

### Criterion 4
**Given** an import error message is displayed  
**When** I retry with a valid file  
**Then** import proceeds successfully without requiring page reload

## 4. Technical Notes

### Constraints
- Validation must occur client-side only
- No destructive write before validation passes
- Error copy should be actionable and concise

### Dependencies
- [ ] STORY-persistence-02-import-json.md

### Edge Cases & Error Handling
- Handle unknown schema version values
- Handle empty file uploads
- Handle partial parse success with missing required fields

## 5. Estimation

**Story Points:** 2  
**Estimated Days:** 1.5  
**Complexity:** Moderate

**Rationale:** Focused validation and error UX story, bounded to import safety and retry behavior.

## 6. INVEST Validation Checklist

### Independent
- [X] Adds a standalone reliability improvement

### Negotiable
- [X] Message style and validation implementation can vary

### Valuable
- [X] Protects users from accidental data loss

### Estimable
- [X] Validation rules and outcomes are clear

### Small
- [X] Can be completed in 1-3 days

### Testable
- [X] Failure and retry scenarios are deterministic

**Is this story INVEST-compliant?** [X] YES | [ ] NO
