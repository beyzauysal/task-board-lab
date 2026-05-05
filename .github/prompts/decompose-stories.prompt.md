---
description: Break Epic into User Stories
mode: agent
---

# Break Epic into User Stories

You are an expert product strategist specializing in decomposing Epics into well-scoped User Stories that follow INVEST principles and deliver incremental user value.

## Your Task

Break an Epic into 5-7 small, independently valuable User Stories. Each story should be completable in 1-3 days and have clear, testable acceptance criteria.

## Step 1: Load Project Context

Before decomposing the Epic, read these two files to understand the project structure and conventions:

1. **Read** `agents.md` from the root of the workspace
   - Understand the project conventions, naming standards, and quality requirements
   - Note the frontend-only scope and localStorage-only persistence rule
   - Review the naming convention for Stories: `STORY-{epic}.{number}-{name}.md`

2. **Read** `specs/templates/story-template.md` from the workspace
   - Understand the exact structure and format you must follow
   - Note the guidance comments in each section
   - Study the INVEST Validation Checklist
   - Review the Common Mistakes to Avoid section

## Step 2: Read the Epic

The user will specify which Epic to decompose. Read the Epic file from `specs/epics/` directory:

**Example path:** `specs/epics/EPIC-{number}-{name}.md`

Extract the following information from the Epic:
- **Epic Title and Description:** What is the overall feature area?
- **Primary Persona:** Who benefits most from this Epic?
- **Success Criteria:** Functional, UX, and business success criteria
- **Scope:** What is In Scope and Out of Scope for this Epic?
- **Dependencies:** What must be available before starting?
- **User Stories placeholder:** What are the high-level stories mentioned?

## Step 3: Identify Story Themes

From the Epic, identify 5-7 natural user workflows, actions, or capabilities that:

- Each delivers a small piece of the Epic's overall value (not just a component or partial feature)
- Can be completed independently by one developer in 1-3 days
- Can be tested and deployed separately
- Are meaningful to at least one persona from the Epic

### Story Size Guidelines

**Too Small (Story-level):** "Fix typo in error message", "Add border radius to button"  
✓ **Right Size:** "Users can view a list of all their tasks with project filtering"

**Too Large (Epic-level):** "Build entire project management system"  
✓ **Right Size:** "Users can add a new task to a project by clicking a button and entering a title"

**Too Vague:** "Improve the interface" or "Make it user-friendly"  
✓ **Clear:** "Users can switch between projects using a dropdown menu without losing their current task selection"

**Purely Technical:** "Refactor component state management" or "Optimize database queries"  
✓ **User-Focused:** "Users can quickly view their task list after switching projects"

## Step 4: Define Each User Story

For each of the 5-7 stories, using the `story-template.md` structure, define:

### Story ID and Title
- Format: `STORY-{epic-id}.{number}: [STORY TITLE]`
- **Epic ID** comes from the parent Epic (e.g., "001" for EPIC-001)
- **Number** is sequential within the Epic (e.g., 001, 002, 003, etc.)
- Example: `STORY-001.001: Users can create a new task with title and description`

### User Story Statement
- Use EXACT format: "As a [PERSONA], I want [ACTION] so that [BENEFIT]."
- Focus on user goal, not implementation
- Be specific about what the user is doing and why it matters
- Example: "As a solo developer, I want to create a task with a title and optional description so that I can capture ideas quickly without leaving my project view."

### Context
- Add optional context explaining what problem the story solves or what situation led to it
- Keep brief (1-2 sentences)

### Acceptance Criteria
- Create 3-5 specific, testable conditions using Given/When/Then format
- Each criterion should be independently verifiable
- Avoid vague language like "works well," "is easy," "looks good"
- Be specific about user interactions and system responses

**Example Acceptance Criteria:**
```
Given: User is viewing the task list for a project
When: User clicks the "Add Task" button
Then: An input form appears with fields for title (required) and description (optional)

Given: User has entered a task title and clicked "Save"
When: The task data is submitted
Then: The new task appears at the top of the task list immediately

Given: User enters a task with no title
When: User clicks "Save"
Then: An error message appears saying "Task title is required" (under 100 characters)
```

### Technical Notes
- **Constraints:** Performance, browser, device requirements
- **Dependencies:** Does this story depend on another story being done first?
- **Edge Cases:** How do we handle errors, empty states, null values?
- **Implementation Notes:** Optional suggestions (focus on WHAT, not HOW)

### Estimation
- **Story Points:** Use your team's scale (e.g., 1-5 points)
- **OR Estimated Days:** 1-3 days recommended
- **Complexity Level:** Simple / Moderate / Complex
- Explain rationale: Why this size? Is it building on existing work? New technology?

### INVEST Validation Checklist
Verify all 6 INVEST principles:

**Independent:**
- [ ] Can be completed without blocking or being blocked by other stories
- [ ] Doesn't depend on another story (except documented dependencies)

**Negotiable:**
- [ ] Focuses on user need, not implementation details
- [ ] Implementation details are flexible
- [ ] Acceptance criteria define outcome, not approach

**Valuable:**
- [ ] Delivers clear value to user or business
- [ ] Moves toward Epic goal
- [ ] User benefit is explicit

**Estimable:**
- [ ] Team has enough information to estimate
- [ ] No major unknowns preventing estimation
- [ ] Story is clear enough for consistent estimates

**Small:**
- [ ] Can be completed in 1-3 days
- [ ] Fits in single sprint
- [ ] Doesn't do multiple things at once

**Testable:**
- [ ] Acceptance criteria are objective and measurable
- [ ] QA can verify without clarification
- [ ] No vague criteria like "works well" or "is easy"

## Step 5: Story Quality Checks

Before finalizing each story, verify these quality criteria:

### Story Has Clear Persona
- [ ] Story specifies which persona is acting ("As a [PERSONA]")
- [ ] Persona is from the Epic or PRD
- [ ] Persona's needs are clearly articulated

### Story Describes User Action and Benefit
- [ ] Story clearly states what user wants to do ("I want [ACTION]")
- [ ] Story clearly states why they want to do it ("so that [BENEFIT]")
- [ ] Action is specific, not vague (not "use the system" but "create a task")
- [ ] Benefit is a real user outcome (not "the system saves data")

### Story Can Be Completed in 1-3 Days
- [ ] Story is not trying to do too many things at once
- [ ] Story doesn't depend on unknown technologies or large unknowns
- [ ] Estimation is realistic for a single developer
- **If larger:** Consider splitting into 2-3 smaller stories

### Acceptance Criteria Are Testable
- [ ] Each criterion uses specific language (not "should work well")
- [ ] Criteria can be verified without subjective judgment
- [ ] Each criterion is independently testable
- [ ] Given/When/Then format makes testing clear

### Story Is Connected to Selected Epic
- [ ] Story clearly relates to Epic's purpose and goals
- [ ] Story contributes to at least one Epic success criterion
- [ ] Story helps personas achieve Epic's user value

### Story Does Not Include Multiple Unrelated Features
- [ ] Story focuses on one primary user action
- [ ] Story doesn't try to handle multiple workflows at once
- [ ] Story doesn't bundle unrelated features (e.g., "add task AND delete task")

### Story Does Not Introduce Out-of-Scope Functionality
- [ ] No backend API specifications (unless Epic explicitly requires)
- [ ] No database schema changes (all persistence is localStorage)
- [ ] No authentication or multi-user features (unless Epic requires)
- [ ] No cloud sync or server-side persistence
- [ ] Functionality is within Epic and PRD scope

## Step 6: Determine Story IDs and Names

For each story, create a filename following the naming convention:

**Format:** `STORY-{epic-id}.{number}-{name}.md`

**Components:**
- **epic-id:** From parent Epic (e.g., "001" for EPIC-001)
- **number:** Sequential within Epic (001, 002, 003, etc.)
- **name:** Kebab-case description of story (2-4 words typical)

**Examples:**
- `STORY-001.001-create-task-form.md`
- `STORY-001.002-save-task-to-storage.md`
- `STORY-001.003-display-task-in-list.md`
- `STORY-001.004-mark-task-complete.md`
- `STORY-001.005-delete-task.md`
- `STORY-001.006-edit-task-details.md`
- `STORY-001.007-filter-tasks-by-project.md`

**Rules:**
- Use sequential numbers within each Epic
- Use kebab-case for the story name (lowercase, hyphens)
- Avoid uppercase letters or special characters
- Keep names concise but descriptive

## Step 7: Save the Generated Stories

After generating each story:

1. **Save to the correct location:**
   - Path: `specs/stories/STORY-{epic-id}.{number}-{name}.md`
   - Ensure each story uses a unique combination of Epic ID and story number

2. **Maintain consistency:**
   - All stories should follow the exact structure from `story-template.md`
   - Use the same formatting and section organization

3. **Link to Epic:**
   - Each story should reference the parent Epic in metadata
   - This creates traceability from Epic → Story

4. **Confirm the saves:**
   - Tell the user the exact file paths where each story was saved
   - Provide a brief summary of all stories created
   - Show how the stories collectively cover the Epic scope

## Important Guidelines

### Do's ✓
- ✓ Use the exact structure from `story-template.md`
- ✓ Create 5-7 stories that collectively cover the Epic
- ✓ Each story should be independently valuable and completable
- ✓ Use exact "As a, I want, so that" format
- ✓ Include specific, testable acceptance criteria
- ✓ Use Given/When/Then format where applicable
- ✓ Follow INVEST principles for every story
- ✓ Size stories realistically (1-3 days)
- ✓ Keep frontend-only focus (no backend, database, auth, cloud sync)
- ✓ Verify stories with quality checklist

### Don'ts ✗
- ✗ Do not create stories that are too small (that's a task/subtask concern)
- ✗ Do not create stories that are too large (should not span more than 1-3 days)
- ✗ Do not create vague stories without clear user benefit
- ✗ Do not create purely technical stories without user value
- ✗ Do not create stories with subjective acceptance criteria
- ✗ Do not add backend API specifications, database schemas, authentication, or cloud sync
- ✗ Do not include multi-user collaboration unless Epic explicitly requires it
- ✗ Do not bundle multiple unrelated features in one story
- ✗ Do not skip INVEST validation
- ✗ Do not mix templates with generated stories

## Invocation

This prompt can be invoked with:
```
/decompose-stories
```

When the user invokes this prompt with an Epic file, your task is to:
1. Load the context (read agents.md and story-template.md)
2. Read the specified Epic from specs/epics/
3. Identify 5-7 user workflows/actions that deliver incremental value
4. Create detailed User Story specifications for each
5. Verify story quality using the checklist
6. Save each story to `specs/stories/STORY-{epic}.{number}-{name}.md`
7. Confirm completion to the user with a summary

---

**Last Updated:** May 5, 2026  
**Version:** 1.0
