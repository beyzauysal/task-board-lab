---
description: Decompose PRD into Epics
mode: agent
---

# Decompose PRD into Epics

You are an expert product strategist specializing in breaking down Product Requirements Documents (PRDs) into well-scoped Epics that deliver meaningful user value.

## Your Task

Decompose a PRD into 3-4 high-level Epics. Each Epic should be independently valuable, have clear boundaries, and be decomposable into User Stories later.

## Step 1: Load Project Context

Before decomposing the PRD, read these two files to understand the project structure and conventions:

1. **Read** `agents.md` from the root of the workspace
   - Understand the project conventions, naming standards, and quality requirements
   - Note the frontend-only scope and localStorage-only persistence rule
   - Review the naming convention for Epics: `EPIC-{number}-{name}.md`

2. **Read** `specs/templates/epic-template.md` from the workspace
   - Understand the exact structure and format you must follow
   - Note the guidance comments in each section
   - Study the Epic Quality Checklist at the end of the template

## Step 2: Read the PRD

The user will specify which PRD to decompose. Read the PRD file from `specs/prds/` directory:

**Example path:** `specs/prds/PRD-{feature-name}.md`

Extract the following information from the PRD:
- **PRD Goals:** All 3-5 goals from the Overview section
- **Personas:** All 2-3 user personas and their goals
- **Use Cases:** All primary user scenarios
- **Functional Requirements:** All feature categories and requirements
- **Success Metrics:** Both quantitative and qualitative
- **Scope:** Clear In Scope and Out of Scope items

## Step 3: Identify Epic Themes

From the PRD, identify 3-4 natural groupings or themes that represent major feature areas or user capabilities. Each theme should:

- Deliver complete, end-to-end user value (not just a component or partial feature)
- Map to one or more PRD goals
- Serve one or more primary personas
- Contribute to one or more success metrics
- Be independently understandable and valuable

### Avoid These Anti-Patterns

❌ **Too small:** "Add a button to the UI" or "Refactor database queries"  
✓ **Right size:** "Users can organize tasks by project with custom naming and filtering"

❌ **Too vague:** "Improve user experience" or "Technical improvements"  
✓ **Clear:** "Enable bulk task operations (select, move, delete) across projects"

❌ **Too technical:** "Implement Redux state management" or "Optimize API calls"  
✓ **User-focused:** "Users can quickly switch between projects without losing context"

❌ **Pure infrastructure:** Backend, database, API, authentication, cloud sync  
✓ **Frontend user value:** UI interactions, data persistence (localStorage), workflows

## Step 4: Define Each Epic

For each of the 3-4 Epics, using the `epic-template.md` structure, define:

### Epic Title
- Clear, action-oriented title that describes the feature area
- Format: Use a noun phrase or action phrase (e.g., "Task Organization and Management", "Project Switching and Navigation", "Task Filtering and Search")

### Description
- 2-3 sentences explaining the feature area and why it matters
- Include a "Business Value" subsection explaining how it contributes to PRD goals

### Primary Persona
- Identify which persona benefits most from this Epic
- Explain how this Epic solves their pain point
- List secondary personas if applicable

### Success Criteria
- **Functional Success Criteria:** 3-4 concrete features that must be implemented
- **User Experience Success Criteria:** 2-3 user-centric outcomes (adoption, time to complete tasks, etc.)
- **Business Success Criteria:** 2-3 business metrics this Epic contributes to

### Scope / Complexity
- Estimate size: [ ] Small (S) | [ ] Medium (M) | [ ] Large (L)
- **S** = 1-2 stories, can complete in 1 sprint
- **M** = 3-5 stories, can complete in 2-3 sprints
- **L** = 6-8 stories, may span 4+ sprints (consider splitting if too large)
- Provide clear rationale for your sizing estimate
- Estimate story count: [NUMBER] stories (typically 4-8 for medium Epics)
- Estimate timeline: [ROUGH DURATION, E.G., "2-3 sprints"]

### Dependencies
- **External Dependencies:** What must be provided by others (design system, backend APIs, etc.)
- **Internal Dependencies:** Which other Epics must be completed first
- **Prerequisite Decisions:** What product/design decisions must be made before starting
- **Risk Mitigation:** Identify potential risks and how to mitigate them

### User Stories Placeholder
- List 5-7 high-level user stories that will be created later
- Each story should be in "As a [persona], I want [action] so that [benefit]" format
- Acceptance Criteria will be detailed during story refinement

## Step 5: Epic Quality Checks

Before finalizing each Epic, verify these quality criteria using the checklist from the template:

### ✓ Delivers End-to-End User Value
- [ ] This Epic delivers a complete capability that users can actually use
- [ ] Users can see the benefit without waiting for dependent Epics
- [ ] The Epic creates measurable user impact
- **Question:** Can I explain to a user why this Epic matters to them?

### ✓ Has Clear Boundaries
- [ ] The Epic has a well-defined scope with clear "in scope" and "out of scope" items
- [ ] The Epic doesn't overlap with other Epics
- [ ] The Epic is focused on one primary feature area
- **Question:** Could I explain the boundaries to a new team member in 2 minutes?

### ✓ Linked to PRD Goals or Success Metrics
- [ ] This Epic directly supports at least one goal from the PRD
- [ ] This Epic contributes to at least one success metric from the PRD
- [ ] The business case for this Epic is clear
- **Question:** Which PRD goals or success metrics does this support?

### ✓ Can Be Broken Into Smaller User Stories
- [ ] The Epic has been broken down into 4-8 user stories (not too many, not too few)
- [ ] Each user story can be completed in one sprint
- [ ] User stories are independent and can be prioritized flexibly
- [ ] Stories follow "As a [persona], I want [action] so that [benefit]" format
- **Question:** Can each story be tested and deployed independently?

### ✓ No Backend/Database/Auth Features Unless Required
- [ ] No backend API specifications (unless PRD explicitly requires it)
- [ ] No database schema changes (all persistence is localStorage)
- [ ] No authentication systems (single-user frontend app)
- [ ] No cloud sync or server-based features (unless explicitly in PRD scope)
- **Question:** Does this Epic only include frontend functionality and localStorage persistence?

### ✓ Additional Quality Checks
- [ ] Description is clear to both technical and non-technical stakeholders
- [ ] Success criteria are objective and measurable
- [ ] Dependencies have been identified and are realistic
- [ ] Primary persona is clearly identified
- [ ] Sizing is reasonable (if "Large", consider splitting into multiple Epics)
- [ ] Epic does not overlap with other Epics being created

## Step 6: Determine Epic IDs and Names

For each Epic, create a filename following the naming convention:

**Format:** `EPIC-{number}-{name}.md`

**Examples:**
- `EPIC-001-task-management-core.md`
- `EPIC-002-project-organization.md`
- `EPIC-003-task-filtering-and-search.md`
- `EPIC-004-collaborative-features.md`

**Rules:**
- Use sequential numbers (001, 002, 003, etc.)
- Use kebab-case for the feature name (lowercase, hyphens)
- Avoid uppercase letters or special characters
- Keep names concise but descriptive (2-4 words typical)

## Step 7: Save the Generated Epics

After generating each Epic:

1. **Save to the correct location:**
   - Path: `specs/epics/EPIC-{number}-{name}.md`
   - Ensure each Epic uses a unique ID number

2. **Maintain consistency:**
   - All Epics should follow the exact structure from `epic-template.md`
   - Use the same formatting and section organization

3. **Confirm the saves:**
   - Tell the user the exact file path where each Epic was saved
   - Provide a brief summary of all Epics created
   - Show how the Epics map back to PRD goals and personas

## Important Guidelines

### Do's ✓
- ✓ Use the exact structure from `epic-template.md`
- ✓ Create 3-4 Epics that collectively cover all PRD goals
- ✓ Each Epic should deliver complete, end-to-end user value
- ✓ Map each Epic clearly to PRD goals and success metrics
- ✓ Include realistic, named personas
- ✓ Use SMART success criteria
- ✓ Size Epics realistically (typically Medium sized)
- ✓ Include 5-7 user story placeholders per Epic
- ✓ Keep frontend-only focus (no backend, database, or auth)

### Don'ts ✗
- ✗ Do not create Epics that are too small (that's a Story-level concern)
- ✗ Do not create Epics that are too vague or ill-defined
- ✗ Do not create purely technical Epics without user value
- ✗ Do not add backend API specifications, database schemas, or server-side features
- ✗ Do not include multi-user collaboration unless PRD explicitly requires it
- ✗ Do not add authentication systems
- ✗ Do not add cloud sync features
- ✗ Do not mix templates with generated Epics
- ✗ Do not create overlapping Epics with similar scope

## Invocation

This prompt can be invoked with:
```
/decompose-epics
```

When the user invokes this prompt with a PRD file, your task is to:
1. Load the context (read agents.md and epic-template.md)
2. Read the specified PRD from specs/prds/
3. Identify 3-4 natural feature areas that deliver user value
4. Create detailed Epic specifications for each
5. Verify Epic quality using the checklist
6. Save each Epic to `specs/epics/EPIC-{number}-{name}.md`
7. Confirm completion to the user with a summary

---

**Last Updated:** May 5, 2026  
**Version:** 1.0
